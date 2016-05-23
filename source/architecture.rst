.. FlexSwitchSDK documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Detailed Architecture
=====================

FlexSwitch software is a collection of L2, L3 protocols and some infrastructure components.
All FlexSwitch daemons are designed like micro servers. Each protocol/infrastructure daemon 
provides APIs using RPC mechanism. Currently we use `ApacheThrift <https://thrift.apache.org/>`_ as RPC mechanism

FlexSwitch software uses database to store configuration, state and events information. Currently we use 
`Redis <http://redis.io/>`_ as our database. All components of FlexSwitch use `Nano Message <http://nanomsg.org/>`_ 
for notifying various events.

FlexSwitch also provides SDK for accessing all the REST APIs. The goal is to have SDK available in Java, Golang, Python
Currently we support only `Python SDK <https://github.com/snaproute/flexsdk/>`_ 


System Architecture
^^^^^^^^^^^^^^^^^^^
.. image:: images/Software_Architecture.png

System Components
^^^^^^^^^^^^^^^^^

Infrastructure Daemons
^^^^^^^^^^^^^^^^^^^^^^

Configuration Manager
"""""""""""""""""""""

Config Daemon is the entity that acts as an entry point into the system. Confd provides REST interface to a pool of objects.
These objects are defined in the `Model Repository <https://github.com/snaproute/models/>`_. Each object is owned by a single daemon 
in the system. Confd connects to all the daemons via RPC and relays the configuration.

Confd does not provide authentication by itself. Howevever Confd can be integrated with web servers like `Nginx <https://www.nginx.com/>`_ or `Apache Webserver <https://httpd.apache.org/>`_
for authentication.

Config daemon code can be found `here <https://github.com/snaproute/config>`_

.. toctree::
   :maxdepth: 1

    Detailed Config Daemon design <confd>


System Daemon 
"""""""""""""

System Daemon is responsible for monitoring the system health. It monitors all the protocol daemons and infrastructure daemons.
In addition to monitoring the daemons SysD is also responsible for handing various global configuration parameters like system name,
Router Id, Management IP etc.
System daemon code can be found `here <https://github.com/snaproute/infra`_

.. toctree::
   :maxdepth: 1

    Detailed System Daemon design <sysd>



Routing Information Base
"""""""""""""""""""""""""

RIB daemon is responsible for storing all IPv4, IPV6 routes and Policies that manage these routes. In addition to managing the routes
RIBd code can be found `here <https://github.com/snaproute/l3`_

.. toctree::
   :maxdepth: 1

    Detailed RIB Daemon design <rib/rib>

ASIC Daemon
"""""""""""
Snaproute's asic daemon serves as a hardware abstraction layer (HAL). A common northbound API interface is exposed to all protocol daemons. This interface allows provisioning a range of packet processing ASICs such as Broadcom, Mellanox, Cavium. Support for software simulation on a linux host OS is also provided.

Architecture
************

..image:: images/Asic_daemon.jpg

**Northbound interface:**

The asic daemons northbound interface is implemented using thrift RPC. This is the interface that is used by users/protocols to apply configuration.

**Core resource managers:**

The core infrastructure within Asicd is distributed across multiple resource managers, e.x. portMgr.go, routeMgr.go, neighborMgr.go etc. Each of these individual resource managers support Create/Retrieve/Update and Delete operations on the corresponding resource. These resource managers also maintain any relevant state data for each corresponding resource.

**Plugins:**

The asic daemon uses a plugin based approach to effectively abstract differences between ASICs from multiple vendors. The following plugins and asic vendors are currently supported

 - OpenNsl (Broadcom)
 - SAI (Mellanox, Barefoot)
 - Softswitch (Linux host)

**Events handling:**

The asicd daemon supports signaling/notification of asynchronous events. The notification engine employs a nano message based publisher. Notifications for the following events are supported

 - Port operational state changes
 - Vlan/Lag interface creation/deletion
 - IP interface operational state changes


Protocol Daemons
^^^^^^^^^^^^^^^^

FlexSwitch utilizes many different protocol daemons.  Each one is an independent structure that runs as a separate daemon independent of the system as a whole. 
This allows for any set of daemons to be run based on end-user preference.  This results in less code being executed and thus greater stability. 

Layer 3 Daemons
"""""""""""""""

ARP Daemon
++++++++++

The address resolution protocol (arp) is a protocol used by the Internet Protocol (IP) [RFC826], specifically IPv4, to map IP network addresses to the hardware addresses used by a data link protocol. The protocol operates below the network layer as a part of the interface between the OSI network and OSI link layer.

Architecture
************

.. image:: images/ARP.png

**Description**


ARP module listens to ASICD notification for L3 interface creation/deletion. It starts Rx/Tx go routines on all L3 interface.

	- When it receives any ARP request, ARP cache is updated with IP Address (source IP) to Mac Address (source MAC) in ARP request packet. Linux ARP stack replies to the ARP Request.
	- When it receives any ARP reply, ARP cache is updated with IP Address (destination IP) to Mac Address (destination MAC) in the ARP reply packet.
	- When it receives any IPv4 packet, ARP cache is updated with IP Address (source IP) to Mac Address (source MAC) in the IPv4 packet if source IP is in local subnet of the switch's L3 interface. And ARP module sends an ARP request packet for the destination IP address.
	- When RIB module receives a route, RIB daemon sends ARP daemon a message to resolve IP Address to Mac Address mapping for the nexthop IP Address.

BFD Daemon
++++++++++

Architecture
************

.. image:: images/BFD_Design.png

DHCP Relay
++++++++++
This module implements Dynamic Host Configuration Protocol Relay Agent. The protocol is standalone Process Daemon, with current dependencies with a configuration daemon CONFD and programability of HW Asic and/or Linux Kernel via ASICD

The Relay Agent will have an instance running per interface.

Architecture
************
.. image:: images/Dhcp_Relay_Agent.png

**Dhcp Relay has following state:**

Receive DISCOVER Packet
Relay client Packet to all servers (configured) updating Relay Agent Information in Dhcp Options
Receive OFFER Packet
Send Unicast OFFER to Client (if configured) else Broadcast OFFER Packet
Receive REQUEST Packet
Relay REQUEST Packet to Server
Receive ACK Packet
Relay ACK Packet to Client

**Configuration**

Detailed information for the object can be found in models package The objects are created keeping in mind the basic Relay Agent Design.

Global Config to enable/disable Relay Agent across all interfaces
Create/Delete Relay Agent per interface
Configure Server's for Relay Agent

OSPF Daemon
+++++++++++

Architecture
************

This module implements Open Shortest Path First.v2 RFC 2328

.. image:: images/OSPF_Architecture.png

**Modules**

OSPF has below components 1) Interface FSM - Handles per interfce OSPF config events,send hello packets, DR/BDR election . It signals Neighbor FSM whenenever new neighbor is detected.

2) Neighbor FSM - This component implements RX packets such as DB description , LSA Update/Request/Ack. Takes care of flooding. Inform LSDB for different events such as neighbor full, install LSA.

3) LSDB - LSA database. Stores 5 types of LSAs. Trigger SPF when new LSA is installed . Generate router/networks LSAs for neighbor full event. Generate summary LSA if ABR. Generate AS external if ASBR. Implements LSA ageing. Inform Neighbor FSM for flooding when new LSA is installed.

4)SPF - Takes care of shortest path calculation and install routes. Signal LSDB to generate summary LSA when ABR.

5) RIBd listener - Listens to RIBd updates when OSPF policy is configured. When router is acting as ASBR - RIbd listener will receive route updates as per the policy statement. It signals LSDB for AS external generation when router is configured as ASBR.


BGP Daemon
++++++++++

This is a implementation of Border Gateway Protocol (BGP-4) in Go.

The following RFCs have been implemented:

1. RFC-4271: Base BGP-4 RFC
2. RFC-4456: Route reflector
3. RFC-5492: Capabilities
4. RFC-4893: Four-octet AS Numbers
5. RFC-4760: Multiprotocol Extensions
6. https://tools.ietf.org/html/draft-ietf-idr-add-paths-14: Advertisement of Multiple Paths in BGP

Architecture
************
.. image:: images/BGP_Module.png

VRRP Daemon
+++++++++++
This module implement Virtual Router Redundancy Protocol RFC 5798

Architecture
************

.. image:: images/VRRP_Architecture.png

**Interfaces**

 - Create/Delete Virtual Router
 - Change timers for VRRP packet, for e.g: Advertisement Timer

**Configuration**

 - VRRP configuration is based of https://tools.ietf.org/html/rfc5798#section-5.2
 - Unless specified each instance of Virtual Router will use the default values specified in the RFC

Layer 2 Daemons
"""""""""""""""

STP Daemon
++++++++++

Spanning Tree Protocol (STP) is a network protocol that builds a logical loop-free topology for Ethernet Networks. Basic functionality is to prevent bridge loops.
This module supports the following spanning tree versions:

 - STP IEEE 802.1D
 - RSTP IEEE 802.1W
 - Rapid-PVST+

.. toctree::
    :maxdepth: 1
    
    Detailed Architecture <stpd>

LACP Daemon
+++++++++++

Link Layer Aggregation Control Protocol (LACP)  is based of IEEE 802.1ax-2014 (which can be found at http://standards.ieee.org/getieee802/download/802.1AX-2014.pdf). This implemention currently only supports functionality related to version 1 of the protocol.

LACP provides a method to control the bundling of several physical ports together to form a single logical channel. It allows a network device to negotiate an automatic bundling of links.

.. toctree::
    :maxdepth: 1
    
    Detailed Architecture <lacpd>

LLDP Daemon
+++++++++++
Module implements IEEE 802.1AB Link Layer Discovery Protocol. The protocol is a standalone Process Daemon. It will have an instance running per interface. Via this protocol, Flexswitch will advertise attached IEEE LAN major capabilites supported by local port.

.. toctree::
   :maxdepth: 1
    
   Detailed Architecture <lldpd>

VXLAN Daemon
++++++++++++

.. image:: images/VXLAN_Architecture.png

