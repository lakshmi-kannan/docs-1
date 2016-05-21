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
RIBd installs and unistalls routes into ASIC via ASICd

RIBd code can be found `here <https://github.com/snaproute/l3`_

.. toctree::
   :maxdepth: 1

    Detailed RIB Daemon design <ribd>


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

.. image:: images/ARP.png

BFD Daemon
++++++++++

.. image:: images/BFD_Design.png

OSPF Daemon
+++++++++++

.. image:: images/OSPF_Architecture.png

BGP Daemon
++++++++++

.. image:: images/BGP_Module.png

VRRP Daemon
+++++++++++

.. image:: images/VRRP_Architecture.png

Layer 2 Daemons
"""""""""""""""

STP Daemon
++++++++++

.. image:: images/STP_Architecture.png

LACP Daemon
+++++++++++

.. image:: images/LACPArchitectureOverview.png

LLDP Daemon
+++++++++++

.. image:: images/VRRP_Architecture.png


VXLAN Daemon
++++++++++++

.. image:: images/VXLAN_Architecture.png

