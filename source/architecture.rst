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
Currently we support only `Python SDK <https://github.com/opensnaproute/flexsdk/>`_


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
These objects are defined in the `Model Repository <https://github.com/opensnaproute/models/>`_. Each object is owned by a single daemon
in the system. Confd connects to all the daemons via RPC and relays the configuration.

Confd does not provide authentication by itself. Howevever Confd can be integrated with web servers like `Nginx <https://www.nginx.com/>`_ or `Apache Webserver <https://httpd.apache.org/>`_
for authentication.

Config daemon code can be found `here <https://github.com/opensnaproute/config>`_

.. toctree::
   :maxdepth: 1

    Detailed Config Daemon design <confd>


System Daemon 
"""""""""""""

System Daemon is responsible for monitoring the system health. It monitors all the protocol daemons and infrastructure daemons.
In addition to monitoring the daemons SysD is also responsible for handing various global configuration parameters like system name,
Router Id, Management IP etc.
System daemon code can be found `here <https://github.com/opensnaproute/infra>`_

.. toctree::
   :maxdepth: 1

    Detailed System Daemon design <sysd>



Routing Information Base
"""""""""""""""""""""""""

RIB daemon is responsible for storing all IPv4, IPV6 routes and Policies that manage these routes. In addition to managing the routes
RIBd installs and unistalls routes into ASIC via ASICd

RIBd code can be found `here <https://github.com/opensnaproute/l3>`_

.. toctree::
   :maxdepth: 1

    Detailed RIB Daemon design <rib/rib>


ASIC Daemon
"""""""""""
ASIC Daemon serves as a hardware abstraction layer (HAL). A common northbound API interface is exposed to all protocol daemons.
This interface allows provisioning of a range of packet processing ASICs.
Support for software simulation with docker instances is also provided.

ASICd binaries can be found `here <https://github.com/opensnaproute/asicd>`_

.. toctree::
   :maxdepth: 1

   Detailed ASIC Daemon design <asicd>


Protocol Daemons
^^^^^^^^^^^^^^^^

FlexSwitch utilizes many different protocol daemons.  Each one is an independent structure that runs as a separate daemon independent of the system as a whole. 
This allows for any set of daemons to be run based on end-user preference.  This results in less code being executed and thus greater stability. 

Layer 3 Daemons
"""""""""""""""

ARP Daemon
************

The address resolution protocol (arp) is a protocol used by the Internet Protocol (IP) [RFC826], specifically IPv4, to map IP network addresses to the hardware addresses used by a data link protocol. The protocol operates below the network layer as a part of the interface between the OSI network and OSI link layer.

ARPd source code can be found `here <https://github.com/opensnaproute/l3>`_

.. toctree::
   :maxdepth: 1

   Detailed ARP Daemon design <arpd>



BFD Daemon
++++++++++

.. toctree::
   :maxdepth: 1
    
   Detailed Architecture <bfd>



DHCP Daemon
************

Dynamic Host Configuration Protocol (DHCP) is a client/server protocol that automatically provides an Internet Protocol (IP) host with its IP address and other related configuration information such as the subnet mask and default gateway. 

DHCPd source code can be found `here <https://github.com/opensnaproute/l3>`_

.. toctree::
   :maxdepth: 1

   Detailed DHCP Daemon design <dhcpd>



DHCP Relay
++++++++++
This module implements Dynamic Host Configuration Protocol Relay Agent. `RFC-3046 <https://tools.ietf.org/html/rfc3046>`_ is used for implementation 

Relay Agent can be used in networks where a DHCP client is not directly connected to DHCP Server. On such networks relay agent will do the job for the client.

.. toctree::
   :maxdepth: 1
    
   Detailed Architecture <dhcprelayd>


OSPF Daemon
+++++++++++

Architecture
************

This module implements Open Shortest Path First.v2 RFC 2328

.. toctree::
   :maxdepth: 1
    
   Detailed Architecture <ospfArchitecture>


BGP Daemon
++++++++++

This is a implementation of Border Gateway Protocol (BGP-4) in Go.

.. toctree::
   :maxdepth: 1
    
   Detailed Architecture <bgpd>


VRRP Daemon
+++++++++++
This module implement Virtual Router Redundancy Protocol (VRRP) `RFC 5798 <https://tools.ietf.org/html/rfc5798>`_ VRRP increases the availability and relability of routing paths. Protocol achieves this by creating virtual routers on top of IPv4 intefaces which acts as master and backup routers (a group). Host is assigned Virtual Router IP address instead of physical router, so that on failure backup can take over master.

.. toctree::
   :maxdepth: 1
    
   Detailed Architecture & Description <vrrpd>


Layer 2 Daemons
"""""""""""""""

STP Daemon
**********
Spanning Tree Protocol (STP) is a network protocol that builds a logical loop-free topology for Ethernet Networks. Basic functionality is to prevent bridge loops.
This module supports the following spanning tree versions:

 - STP IEEE 802.1D
 - RSTP IEEE 802.1W
 - Rapid-PVST+

.. toctree::
    :maxdepth: 1
    
    Detailed Architecture <stpd>


LACP Daemon
***********
Link Layer Aggregation Control Protocol (LACP)  is based of IEEE 802.1ax-2014 (which can be found at http://standards.ieee.org/getieee802/download/802.1AX-2014.pdf). This implemention currently only supports functionality related to version 1 of the protocol.

LACP provides a method to control the bundling of several physical ports together to form a single logical channel. It allows a network device to negotiate an automatic bundling of links.

.. toctree::
    :maxdepth: 1
    
    Detailed Architecture <lacpd>


LLDP Daemon
***********

Module implements IEEE 802.1AB Link Layer Discovery Protocol. The protocol is a standalone Process Daemon. It will have an instance running per interface. Via this protocol, Flexswitch will advertise attached IEEE LAN major capabilites supported by local port.

.. toctree::
   :maxdepth: 1
    
   Detailed Architecture <lldpd>


VXLAN Daemon
************

.. toctree::
   :maxdepth: 1
    
   Detailed Architecture <vxland>
