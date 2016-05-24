Bi-Directional Forwarding Detection(BFD)
========================================
BFD is a lightweight protocol that runs on UDP and notifies registered applications about the state of the connectivity to remote IP address. It acheives the same by send/receiving periodic control packets and timing out as per the configuration.

BFD in FlexSwitch is implemented to support RFC-5880 (BFD Asynchronous and Demand modes with Authentication) and RFC-7130 (Bfd over LAG links). BFD runs a seperate daemon, named bfdd.

Architecture
============

.. image:: images/BFD_Design.png

Design
======


Work In Progress
================
1. BFD authentication is not tested for inter-operability with any other implementation.
2. BFD over LAG links is not tested for inter-operability with any other implementation.
3. Echo functionality is yet to be supported in FlexSwitch.
