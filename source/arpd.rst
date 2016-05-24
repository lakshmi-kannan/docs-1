Welcome to FlexSwitch ARPd's documentation!
==============================================
.. image:: images/ARP.png

ARP Daemon Architecture
------------------

Introduction
^^^^^^^^^^^^^
The address resolution protocol (arp) is a protocol used by the Internet Protocol (IP) [RFC826], specifically IPv4, to map IP network addresses to the hardware addresses used by a data link protocol. The protocol operates below the network layer as a part of the interface between the OSI network and OSI link layer.

Design
^^^^^^^^
ARP module implements Address Resolution Protocol. Core design is implemented in server package which has multiple Go routines for various functionality which will be explain in below sections. ARP module interacts with other daemons via RPC using `Thrift <https://thrift.apache.org/>`_ and PUB/SUB using `nanomsg <http://nanomsg.org/>`_.

Core
""""""
As part of initialization of Arp daemon following functionalities are performed:

        - Connect to Asicd server
        - Subscribe to Asicd publisher
        - Start ARP server 

Arp daemon connects to Asicd (thrift) server for building internal infrasturcture for future operations. These infrastructure data is stored in maps indexed by IfIndex.

- L3 Interface Property Map (l3IntfPropMap): which is keyed by IfIndex and value is data of type L3IntfProperty Structure

::


        type L3IntfProperty struct {
                Netmask net.IPMask      // Subnet mask
                IpAddr  string          // IP Address
                IfName  string          // L3 Interface name
        }


- Port Property Map (portPropMap): which is keyed by IfIndex and value is data of type PortProperty Structure

::


        type PortProperty struct {
                IfName   string         // Phy Port Name
                MacAddr  string         // MAC Address
                IpAddr   string         // IP Addresss of the L3 Interface of which this port is member.
                Netmask  net.IPMask     // Subnet mask Addresss of the L3 Interface of which this port is member.
                L3IfIdx  int            // L3 IfIndex of which this port is member.
                LagIfIdx int            // Lag Ifindex of which this port is member.
                CtrlCh   chan bool      // Channel for controlling Rx/Tx on this port
                PcapHdl  *pcap.Handle   // Pcap Handle for Rx/Tx ARP packets
        }


- Vlan Property Map (vlanPropMap): which is keyed by IfIndex and value is data of type VlanProperty Structure

::


        type VlanProperty struct {
                IfName       string             // Vlan Interface name
                UntagPortMap map[int]bool       // Map containing list of un-tagged ports
        }


- Lag Property Map (lagPropMap): which is keyed by IfIndex and value is data of type LagProperty Structure

::


        type LagProperty struct {
                IfName  string                  // Lag Interface name
                PortMap map[int]bool            // Map containing list of member ports
        }


 
 When Arp daemon comes up it performs following calls to Asicd for building internal infrasturcture:

        - GetBulkPort(): To get the all the existing port configuration.
        - GetBulkPortState(): To get all the existing port state.
        - GetBulkVlan(): To get the list of existing Vlan configuration.
        - GetBulkVlanState(): To get the list of existing Vlan states.
        - GetBulkIPv4IntfState(): To get the list of existing L3 IPv4 interface details.

ARP daemon subscribes to Asicd notification in order to maintain a syncronization of its infrastructure with the overall system state. As these infrastuctre will be used for Rx/Tx Operations and also while programming Hardware ARP table. ARP daemon listens to following notification from Asicd:

        - L2IntfState Notification
        - L3IntfState Notification
        - Vlan Notification
        - Lag Notification
        - IPv4Intf Notification
        - IPv4NbrMacMove Notification
        

On each ports which are member of L3 IPv4 interface ARP daemon performs Rx/Tx functionaily. 

        - On creation of IPv4 L3 interface ARP daemon send ARP probe message on all the ports which are member of created IPv4 L3 Interface.
        - When it receives any ARP request, ARP cache is updated with IP Address (source IP) to Mac Address (source MAC) in ARP request packet. Linux ARP stack replies to the ARP Request.
        - When it receives any ARP reply, ARP cache is updated with IP Address (destination IP) to Mac Address (destination MAC) in the ARP reply packet.
        - When it receives any IPv4 packet, ARP cache is updated with IP Address (source IP) to Mac Address (source MAC) in the IPv4 packet if source IP is in local subnet of the switch's L3 interface. And ARP module sends an ARP request packet for the destination IP address.
        - When RIB module receives a route, RIB daemon sends ARP daemon a message to resolve IP Address to Mac Address mapping for the nexthop IP Address.


ARP daemon maintains ARP cache which is basically a mapping of IPv4 Address to corresponding MAC Address. ARP daemon stores Arp Cache in memory in form of a map data structure which is keyed by IPv4 Address and value is data of type ArpEntry.


::

        type ArpEntry struct {
                MacAddr   string        // MAC Address
                VlanId    int           // Vlan Id on which Arp is learned.
                IfName    string        // Interface name on which Arp is learned
                L3IfIdx   int           // L3 Interface IfIndex on which Arp Entry is learned
                Counter   int           // Counter value used to refresh the Arp Entry
                TimeStamp time.Time     // Time stamp at which Arp Entry is learned
                PortNum   int           // Physical Port on which Arp Entry is learned
                Type      bool          //True : RIB False: RX
        }


Everytime an IPv4 Address to MAC address is learned ARP daemon makes call to Asicd to create IPv4 Neighbor Entry in Hardware

        - CreateIPv4Neighbor()

Everytime an ARP cache entry is timeout, ARP daemon makes call to Asicd to delete IPv4 Neighbor Entry in Hardware

        - DeleteIPv4Neighbor()

APIs (Programming Thrift Interfaces)
"""""""""""""""""""""""""""""""

Configutation Object Name:
***************************

**ArpGlobal**



::

        struct ArpGlobal {
                1 : string Vrf 
                2 : i32 Timeout
        }

- Create ARP Global Config:

::

        bool CreateArpGlobal(1: ArpGlobal config);


 - Update ARP Gloabl Config:

::

        bool UpdateArpGlobal(1: ArpGlobal origconfig, 2: ArpGlobal newconfig, 3: list<bool> attrset);


- Delete ARP Global Config: 

::

        bool DeleteArpGlobal(1: ArpGlobal config);


State Object Name: 
*******************

**ArpEntryState** :

::

        struct ArpEntryState {
                1 : string IpAddr               // IPv4 Address
                2 : string MacAddr              // MAC Address
                3 : string Vlan                 // Vlan Id
                4 : string Intf                 // Physical Interface Name
                5 : string ExpiryTimeLeft       // Time left before expiry
        }

        struct ArpEntryStateGetInfo {
                1: int StartIdx                                 // [IN] Start Index
                2: int EndIdx                                   // [OUT] End Index
                3: int Count                                    // [OUT] Number of element in List
                4: bool More                                    // [OUT] True: if there are more. False: if there are no more elements
                5: list<ArpEntryState> ArpEntryStateList        // List of Arp Entries
        }


- Get the list of ARP Entries (Object Name: ArpEntryState):

::

        ArpEntryStateGetInfo GetBulkArpEntryState(1: int fromIndex, 2: int count);


- Get the ARP Entry corresponding to given IP Address:

::

        ArpEntryState GetArpEntryState(1: string IpAddr);

**ArpLinuxEntryState** :

::

        struct ArpLinuxEntryState {
                1 : string IpAddr       // IPv4 Address
                2 : string HWType       // Hardware Type
                3 : string MacAddr      // MAC Address
                4 : string IfName       // Interface Name
        }

        struct ArpLinuxEntryStateGetInfo {
                1: int StartIdx                                         // [IN] Start Index
                2: int EndIdx                                           // [OUT] End Index
                3: int Count                                            // [OUT] Number of element in List
                4: bool More                                            // [OUT] True: if there are more. False: if there are no more elements
                5: list<ArpLinuxEntryState> ArpLinuxEntryStateList      // [OUT] List of Linux Arp Entries
        }


- Get the list of linux ARP Entries (Object Name: ArpLinuxEntryState):

::

        ArpLinuxEntryStateGetInfo GetBulkArpLinuxEntryState(1: int fromIndex, 2: int count);


- Get the linux ARP Entry corresponding to given IP Address:

::

        ArpLinuxEntryState GetArpLinuxEntryState(1: string IpAddr);

Actions:
*********


- Delete all the ARP entries learnt on given interface name

::

        struct ArpRefreshByIfName {
                1 : string IfName       // [IN] L3 Interface Name
        }

::

        bool ExecuteActionArpDeleteByIfName(1: ArpDeleteByIfName config);


- Delete the ARP entry corresponding to given IPv4 address

::

        struct ArpDeleteByIPv4Addr {
                1 : string IpAddr       // [IN] IPv4 Address
        }

::

        bool ExecuteActionArpDeleteByIPv4Addr(1: ArpDeleteByIPv4Addr config);

Note: We can only delete Arp entries which are not the nexthop for any of the routes.


- Refresh all the ARP entries learnt on given interface name

::

        struct ArpDeleteByIfName {
                1 : string IfName       // [IN] L3 Interface Name
        }

::

        bool ExecuteActionArpRefreshByIfName(1: ArpRefreshByIfName config);


- Refresh the ARP entry corresponding to given IPv4 address

::

        struct ArpRefreshByIPv4Addr {
                1 : string IpAddr       // [IN] IPv4 Address
        }

::

        bool ExecuteActionArpRefreshByIPv4Addr(1: ArpRefreshByIPv4Addr config);

