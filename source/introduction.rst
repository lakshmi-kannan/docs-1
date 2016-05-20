.. FlexSwitchSDK documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Introduction
============
FlexSwitch is the first open source network protocol suite offering complete layer2/layer3 functionality for accelerating development and deployment of whitebox networking gear

**FlexSwitch offers the following :**                                                                                       
    - Fully programmable network protocol stack 
    - RESTful APIs at every level 
    - Highly customizable behavior
    - Works on variety of switching silicon like Broadcom, Mellonox, Cavium, Barefoot                                   
    - Portable architecture to work on hardware from variety of vendors like Acton, Celestica, Alpha Networks, Facebook Wedge
    - Highly instrumented to help the Network operators troubleshoot issues

Use cases
----------
FlexSwitch is well suited for the following use cases:
    - Building whitebox networking devices like Datacenter switch, Router, Metro Transport element
    - Building custom networking devices with off the shelf ethernet silicon
    - Building Network Function Virtulaization elements

Architecture
^^^^^^^^^^^^


System Architecture
"""""""""""""""""""

.. image:: images/Software_Architecture.png


System Components
^^^^^^^^^^^^^^^^^

GoLang
""""""

Golang has become the modern programming language for systems and infrastructure programming.  Benefits of using GoLang:

	- **Statically typed and Compiled** - All the type safety issues are caught during compile time, unlike at run time like Python, Java Script
	- **Built In Garbage Collection**  - Programmer does not have to manage memory for allocation and frees. This eliminates many system crashes that are way too familiar for systems programmers.
	- **Built In  concurrency** - Golang's concurrency patterns are very powerful and easy to use. 
	- **Built in multi core support** - Golang's concurrency patterns are very powerful and easy to use.
 
FlexSwitch utilizes golang as the base language for all our development. This brings agility into our development and also quality into our software

Python
""""""

RPC tools
"""""""""

Most modern software needs to interact with other software modules in some fashion.  Using RPC is one of very well known mechanisms to achieve this
Thanks to the opensource community. There are a few comprehensive solutions available 

Thrift RPC
++++++++++

Apache Thrift has been very stable and scalable solution for Inter Process Communication (IPC)/Remote Procedure Calls (RPC)

	- **Cross language, Multi language support** - Thrift supports multiple languages( golang, python, C** etc). Clients and servers can be developed in  different languages.  
	- **Simple Interface Definition Language** - IDL defined by Thrift is very simple to use. 
	- **Compiler to generate Client and Server** - Thrift compiler generates client and server in various languages.
	- **Best performance among other choices** - Thrift offers better performance than other RPC tools including gRPC, Protobuf3

FlexSwitch utilizes Thrift for internal communication among our daemons. Thrift RPC is used only from top to down (i.e.) clients to servers.
FlexSwitch ensures not to use RPC from a server to client allowing daemons to remain agnostic of their clients thus eliminating spaghetti dependencies. 


Pub/Sub Mechanisms 
""""""""""""""""""

FlexSwitch software uses non-persistent pub/sub mechanism for notifying its internal components. We need a lightweight and efficient Pub/sub mechanism 

Nano Message
++++++++++++
    
Nano-Message offers clean posix compliant APIs. Performance numbers against Nano Message are much better than its counterparts like ZeroMQ, D-Bus etc
We use Nano Message library in ASICd to notify other protocol daemons about possible events like interface creation, deletion link up/down

Linux
"""""

FlexSwitch software runs on linux in userspace, keeping with the portability and flexibility mantra engrained into our code. 
Due to stability, security and wide spread adoption, Linux has become the defacto standard for all the networking equipment. 


Configuration and State Database
""""""""""""""""""""""""""""""""
FlexSwitch software stores its configuration and state in database to facilitate restoring configuration after restart and to make it easy for the customer applications to read the state of the system. We needed a database that is very efficient. 

Redis
+++++
   
Redis was written in ANSI C and very scaleable database. It also several other features.

	- **In-Memory database** - Redis works primarily as In-Memory database with the option of synchronising the data to disk when needed. This is ideal for storing large state data like MAC Tables, Route tables, Statistics etc
	- **Pub/Sub mechanism** - In addition to working as a database Redis offers pub/sub mechanism. So it can be used as a message broker as well.
	- **High-availability** - Redis provides high-availability by supporting clusters. This would also help in Chassis based systems very well.

FlexSwitch utilizes Redis for storing system state, configuration, and externally visible events like link down, link up etc. 


Infrastructure Daemons
^^^^^^^^^^^^^^^^^^^^^^

Configuration Manager
"""""""""""""""""""""

The front-end to our RestBased API's.  Confd acts as a router to direct the API call to the correct Daemon or Database to the collect the appropriate information. 

System Daemon 
"""""""""""""

Monitors other system components and reports on their health. 

Routing Information Base
"""""""""""""""""""""""""


This is a implementation of Routing Information Base (RIB) in Go. Summary of functionality implemented by this module is as follows:

Handle all network route based configuration (route create, route delete, route update) from either users or other applications (e.g., BGP, OSPF)

Handle all routing policy based configuration : a. policy conditions create/delete/updates b. policy statements create/delete/updates c. policy definitions create/delete/updates

Implement policy engine a. Based on the policy objects configured and applied on the device, the policy engine filter will match on the conditions provisioned and implement actions based on the application location. For instance, the policy engine filter may result in redistributing certain (route type based/ network prefix based) routes into other applications (BGP,OSPF, etc.,)

Responsible for calling ASICd thrift APIs to program the routes in the FIB.

 Architecture
************

.. image:: images/RIB_Architecture.png



ASIC Daemon
"""""""""""

ASICd abstracts away hardware differences across ASIC vendors.  This allows for our protocol stack to be easily be ported to any ASIC from any Vendor.  


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

This module supports the following spanning tree versions:

 - STP IEEE 802.1D
 - RSTP IEEE 802.1W
 - Rapid-PVST+

	

Architecture
************

.. image:: images/STP_Architecture.png

LACP Daemon
+++++++++++

This code base is to handle the LACP protocol according to 802.1ax-2014. This implemention currently only supports functionality related to version 1 of the protocol.

The protocol is a standalone Process Daemon, with current dependencies with a configuration daemon CONFD and programability of HW ASIC and/or Linux Kernel via ASICD.

The LACP protocol will have an instance running per interface. Each LACP represented state machine represented as part of the protocol will be running as a seperate go routine.

Architecture
************

.. image:: images/LACPArchitectureOverview.png

LLDP Daemon
+++++++++++

Module implements IEEE 802.1AB Link Layer Discovery Protocol.

Architecture
************
.. image:: images/VRRP_Architecture.png


**Support**

 - Chassis Id TLV
 - Port Id TLV
 - TTL Tlv
 - Marshalling/Un-Marshalling of Mandatory TLV's

VXLAN Daemon
++++++++++++

.. image:: images/VXLAN_Architecture.png





How to use it?
^^^^^^^^^^^^^^

FlexSwitch comes supplied with a configuration manager which supplies the FrontEnd to our system and acts as a light-weight director of RESTful API calls.  This is the portion of the system, that will direct a configuration item to the appropriate daemon or database call.  In order to simplify how these calls are segmented for the user, the API calls are organized into two categories. +State+ and +Config+ operations.  Every object in the system has both a State and Config operation that can be performed against it.  

On the Config portion, this means when you supply the data you want in JSON format and sent to the associated API to have the configuration applied.  These operations can be done in 3 ways:

 - Directly calling the RestFul API
 - Utilizing the supplied Python SDK
 - Utilizing Ansible to push a configuration file. 

Utilizing the Rest API
""""""""""""""""""""""

Below will be an example of how to utilize the RestFul API to adjust the ARP global timeout value. 

In order to perform this operation with the Restful API, you would create the JSON and send to the ArpConfig REST API:

::

        root@5b5a8d783113:/# curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ArpConfigKey":"1", "Timeout":1000}' http://localhost:8080/public/v1/config/ArpConfig
        {"ObjectId":"a97b920d-8b10-47b1-7ea9-890b07f6e712","Error":""}
  
As you can see This is a 1:1 mapping of config to a specifc Object, in this case Timeout value of 1000 to ARP.


On the State side, this is more invovled, since you can have multiple items, that could potentially have thousand of different states.  Think the prefixes/next-hop entries` in the routing table or multiple IP/MAC mappings with an ARP table.  Due to this variance in data supplied, State operations are broken down into GetBulk, which supplies information from the entire object OR just an indiviual Get, which returns, just the parameters requested from an object.  The way in which these calls are made is based on the pluralization of the object itself.  

Lets use ARP again as an example.  If you wished to grab all entry's from the ARP table, you would query the "+ArpEntry+" state object. However, in order to dictate you wanted all entires, rather than a specific value, you would add a trailing "+s+" to make the operation plural, resulting in a call of "+ArpEntrys+", see below:

::

        root@5c3bca6fb77e:/# curl -X GET --header 'Content-Type: application/json' 'http://localhost:8080/public/v1/state/ArpEntrys' | python -m json.tool
          % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                         Dload  Upload   Total   Spent    Left  Speed
        100   213  100   213    0     0  44654      0 --:--:-- --:--:-- --:--:-- 53250
        {
            "CurrentMarker": 0,
            "MoreExist": false,
            "NextMarker": 0,
            "ObjCount": 1,
            "Objects": [
                {
                    "Object": {
                        "ExpiryTimeLeft": "9m57.74904463s",
                        "Intf": "eth1",
                        "IpAddr": "51.1.1.5",
                        "MacAddr": "4e:8c:3d:c8:d4:09",
                        "Vlan": "5"
                    },
                    "ObjectId": ""
                }
            ]
        }


If you attempted to make such a call to just "+ArpEntry+", you would be returned an error:

::

	root@5c3bca6fb77e:/# curl  -H "Accept: application/json" "http://localhost:8080/public/v1/state/ArpEntry" | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
					 Dload  Upload   Total   Spent    Left  Speed
	100   119  100   119    0     0  21715      0 --:--:-- --:--:-- --:--:-- 23800
	{
	    "Error": "Failed to find entry. Internal error processing GetArpEntryState: Unable to find Arp entry for given IP: \n"
	}

This is due to the fact, that configruation manager expected JSON data to be supplied requesting a specific parameter to search the ARP table on. 


In order to sucessfully, complete the "+ArpEntry+" query, we will supply JSON data for IP address 51.1.1.5:

::

        root@5c3bca6fb77e:/# curl -X GET --header 'Content-Type: application/json' -d '{"IpAddr":"51.1.1.5"}' 'http://localhost:8080/public/v1/state/ArpEntry' | python -m json.tool
          % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                         Dload  Upload   Total   Spent    Left  Speed
        100   157  100   136  100    21  25185   3888 --:--:-- --:--:-- --:--:-- 27200
        {
            "Object": {
                "ExpiryTimeLeft": "9m56.277773536s",
                "Intf": "eth1",
                "IpAddr": "51.1.1.5",
                "MacAddr": "4e:8c:3d:c8:d4:09",
                "Vlan": "5"
            },
            "ObjectId": ""
        }

The call now returns sucessfully with the requested data.  Also note, that returned data is no longer wrapped in GetBulk "+Objects+" header; I.E. the following is missing:
::

            "CurrentMarker": 0,
            "MoreExist": false,
            "NextMarker": 0,
            "ObjCount": 1,
            "Objects": [{}]



This is due to the fact, that only a single object of data was targeted, rather than a bulk operation. The extra object data is not required for a GetBulk operation. 

 

Utilizing the Python SDK 
""""""""""""""""""""""""

Below will be an example of how to utilize the Python SDK to adjust the ARP global timeout value. 

In order to perform this operation with the Python SDK API, you would utilize the following python methods:



::  

	>>>from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).createArpConfig("1", 1000)
	({u'ObjectId': u'45dff5a0-7dc1-441d-723d-ccf731186ece', u'Error': u''}, None)      

.. Note:: the ObjectID and UUID are the same.


As you can see This is a 1:1 mapping of config to a specifc Object, in this case Timeout value of 1000 to ARP.


On the State side, this is more invovled, since you can have multiple items, that could potentially have thousand of different states.  Think the prefixes/next-hop entries in the routing table or multiple IP/MAC mappings with an ARP table.  Due to this variance in data supplied, State operations are broken down into GetBulk, which supplies information from the entire object OR just an indiviual Get, which returns, just the parameters requested from an object.  The way in which these calls are made is performed by utilizing the method with "+getAll+" followed by the Object you wanted to grab; I.E. Arp, Bfd, BGP, etc.  

Lets use ARP again as an example.  If you wished to grab all state entry's from the ARP table, you would utilize the "+getAllArpEntryStates()+" method. With all Python SDK methods, see below:


::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).getAllArpEntryStates()
	[{u'Object': {u'ConfigObj': None, u'Intf': u'fpPort47', u'Vlan': u'Internal Vlan', u'IpAddr': u'172.16.0.14', u'ExpiryTimeLeft': u'9m24.869691096s', u'MacAddr': u'a8:9d:21:aa:8e:01'}, u'ObjectId': u''}, {u'Object': {u'ConfigObj': None, u'Intf': u'fpPort49', u'Vlan': u'Internal Vlan', u'IpAddr': u'172.16.0.20', u'ExpiryTimeLeft': u'9m43.991376701s', u'MacAddr': u'00:02:03:04:05:00'}, u'ObjectId': u''}]


If you wanted to make  a call to just grab a specific Arp Entry from the state table, you would utilize method, getArpEntryStates(), see below:

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).getArpEntryState("172.16.0.20")
	({u'Object': {u'ConfigObj': None, u'Intf': u'fpPort49', u'Vlan': u'Internal Vlan', u'IpAddr': u'172.16.0.20', u'ExpiryTimeLeft': u'16m38.505153914s', u'MacAddr': u'00:02:03:04:05:00'}, u'ObjectId': u''}, None)


The call now returns sucessfully with only the requested data. 

 