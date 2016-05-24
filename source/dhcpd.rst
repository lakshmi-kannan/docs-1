Welcome to FlexSwitch DHCPd's documentation!
===================================================

Note: DHCP Daemon implementation is currently in progress.

.. image:: images/DHCP.png

DHCP Daemon Architecture
------------------

Introduction
^^^^^^^^^^^^^

Dynamic Host Configuration Protocol (DHCP) is a client/server protocol that automatically provides an Internet Protocol (IP) host with its IP address and other related configuration information such as the subnet mask and default gateway.


Design
^^^^^^^^

DHCP module implements Dynamic Host Configuration Protocol. Core design is implemented in server package which has multiple Go routines for various functionality which will be explain in below sections. DHCP module interacts with other daemons via RPC using `Thrift <https://thrift.apache.org/>`_ and PUB/SUB using `nanomsg <http://nanomsg.org/>`_.

Core
""""""
As part of initialization of DHCP daemon following functionalities are performed:

        - Connect to Asicd server
        - Subscribe to Asicd publisher
        - Start DHCP server 

Dhcp daemon connects to Asicd (thrift) server for building internal infrasturcture for future operations. These infrastructure data is stored in maps indexed by IfIndex.

- L3 Interface Property Map (l3IntfPropMap): which is keyed by IfIndex and value is data of type L3IntfProperty Structure

::

        type L3Property struct {
                IpAddr     uint32       // IPv4 Address
                Mask       uint32       // Subnet Mask
                DhcpIfKey  DhcpIntfKey  // Key to DHCP Interface configuration Map
                DhcpConfig bool         // True: DHCP Server is configured, False: No DHCP Server configured
        }


- Port Property Map (portPropertyMap): which is keyed by IfIndex and value is data of type PortProperty Structure

::


        type PortProperty struct {
                IfName     string         // Phy Port Name
                MacAddr    string         // MAC Address
                IpAddr     uint32         // IP Addresss of the L3 Interface of which this port is member.
                Mask       uint32         // Subnet mask Addresss of the L3 Interface of which this port is member.
                L3IfIndex  int32          // L3 IfIndex of which this port is member.
                CtrlCh     chan bool      // Channel for controlling Rx/Tx on this port
                PcapHdl    *pcap.Handle   // Pcap Handle for Rx/Tx DHCP packets
        }


- Vlan Property Map (vlanPropertyMap): which is keyed by IfIndex and value is data of type VlanProperty Structure

::


        type VlanProperty struct {
                UntagPortMap map[int32]bool       // Map containing list of un-tagged ports
        }


- Lag Property Map (lagPropertyMap): which is keyed by IfIndex and value is data of type LagProperty Structure

::


        type LagProperty struct {
                PortMap map[int32]bool            // Map containing list of member ports
        }


 
 When Dhcp daemon comes up it performs following calls to Asicd for building internal infrasturcture:

        - GetBulkPort(): To get the all the existing port configuration.
        - GetBulkPortState(): To get all the existing port state.
        - GetBulkVlan(): To get the list of existing Vlan configuration.
        - GetBulkVlanState(): To get the list of existing Vlan states.
        - GetBulkIPv4IntfState(): To get the list of existing L3 IPv4 interface details.

DHCP daemon subscribes to Asicd notification in order to maintain a syncronization of its infrastructure with the overall system state. As these infrastuctre will be used for Rx/Tx DHCP state machine. DHCP daemon listens to following notification from Asicd:

        - L2IntfState Notification
        - L3IntfState Notification
        - Vlan Notification
        - Lag Notification
        - IPv4Intf Notification


Once DHCP daemon is configured as DHCP server on a given L3 Interface. This daemon starts listening on given L3 Interface for various DHCP messages. And it internally maintains a map which is keyed by DhcpIntfKey and value is per L3 interface Dhcp Data (DhcpIntfData). 


::

        type DhcpIntfKey struct {
                subnet     uint32       // Network Address
                subnetMask uint32       // Subnet Mask
        }

        type DhcpOfferedData struct {
                LeaseTime     uint32            // Lease time offered
                MacAddr       string            // MAC Address of the host to which IP Address is offered
                TransactionId uint32            // Transaction ID used in DHCP Messages
                RefreshTimer  *time.Timer       // Refresh Timer
                StaleTimer    *time.Timer       // Stale Timer used to garbage collection
                State         uint8             // State: OFFERED
        }

        type DhcpIntfData struct {
                enable        bool              // True: Enabled, False: disabled
                l3IfIdx       int32             // L3 Interface IfIndex
                lowerIPBound  uint32            // Lower bound of IP Address Range that can be offered
                higherIPBound uint32            // Higher bound of IP Address Range that can be offered
                rtrAddr       uint32            // Configured Default Router Address that can be offered
                dnsAddr       uint32            // Configured DNS Address that can be offered
                domainName    string            // Configured Domain Name that can be offered
                usedIpPool    map[uint32]DhcpOfferedData        // Map of already offered Data keyed by offered IP Address
                usedIpToMac   map[string]uint32                 // Map of offered IP Address keyed by host's MAC Address
                dhcpMsg       []byte            // DHCP Packet data cached for refresh
        }


APIs (Thrift Interface)
"""""""""""""""""""""""""

Configuration Object Name:
**************************

**DhcpGlobalConfig**

::

        struct DhcpGlobalConfig {
                1 : string DhcpConfigKey        // [IN] Vrf Name
                2 : bool Enable                 // [IN] True: Enable, False: Disable
                3 : i32 DefaultLeaseTime        // [IN] Default Lease time
                4 : i32 MaxLeaseTime            // [IN] Max Lease time
        }


- Create Dhcp Global Configuration:

::

        bool CreateDhcpGlobalConfig(1: DhcpGlobalConfig config);


- Update Dhcp Global Configuration: (Not supported)

::

        bool UpdateDhcpGlobalConfig(1: DhcpGlobalConfig origconfig, 2: DhcpGlobalConfig newconfig, 3: list<bool> attrset);


- Delete Dhcp Global Configuration: (Not supported)

::

        bool DeleteDhcpGlobalConfig(1: DhcpGlobalConfig config);



**DhcpIntfConfig**

::

        struct DhcpIntfConfig {
                1 : string IntfRef              // [IN] Interface name or ifindex of L3 interface
                2 : string Subnet               // [IN] Network Address
                3 : string SubnetMask           // [IN] Subnet Mask
                4 : string IPAddrRange          // [IN] Range of IP Addresses 
                5 : string BroadcastAddr        // [IN] Broadcast Address 
                6 : string RouterAddr           // [IN] Router Address
                7 : string DNSServerAddr        // [IN] Comma seperated List of DNS Server Address
                8 : string DomainName           // [IN] Domain Name Address
                9 : bool Enable                 // [IN] True: Enable, False: Disable
        }



- Create Dhcp Interface Configuration:

::

        bool CreateDhcpIntfConfig(1: DhcpIntfConfig config);


- Update Dhcp Interface Configuration: (Not supported)

::

        bool UpdateDhcpIntfConfig(1: DhcpIntfConfig origconfig, 2: DhcpIntfConfig newconfig, 3: list<bool> attrset);


- Delete Dhcp Interface Configuration: (Not supported)

::

        bool DeleteDhcpIntfConfig(1: DhcpIntfConfig config);

