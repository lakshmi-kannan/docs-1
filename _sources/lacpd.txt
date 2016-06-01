LACP
===================

The protocol is a standalone Process Daemon, with current dependencies with a configuration daemon CONFD and programability of HW ASIC and/or Linux Kernel via ASICD.

The LACP protocol will have an instance running per interface. Each LACP represented state machine represented as part of the protocol will be running as a seperate go routine.

Architecture
************

.. image:: images/LACPArchitectureOverview.png
