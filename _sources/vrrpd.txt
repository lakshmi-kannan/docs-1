Virtual Router Redundancy Protocol
==================================

This is a standalone process daemon, with current dependancies with a configuration daemon (confd) and programability of HW Asic and/or Linux Kernel via ASICd.

There can be multiple VRID instances per interface.

Architecture
************

.. image:: images/Vrrp_Architecture.png

**Interfaces**

 - Create/Delete Virtual Router, with a uniqure VRID (Virtual Router ID)
 - Change timers for VRRP packet, for e.g: Advertisement Timer

**Configuration**

 - VRRP configuration is based of `RFC VRRP Field Description <https://tools.ietf.org/html/rfc5798#section-5.2>`_
 - Unless specified each instance of Virtual Router will use the default values specified in the RFC

**Support**
 - IPv4 address for virtual router i.e V2 of the RFC

**Future**
 - IPv6 support
