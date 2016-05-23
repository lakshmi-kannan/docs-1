

.. FlexSwitch documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Whitebox networking in WAN
============================
This page describes how whitebox switch with Snaproute networking protocol suite (FlexSwitch) can be deployed in WAN topology. Service Provider network can be intercahngeably used as WAN. Below diagram depicts different router types in a Service Provider network where FlexSwitch can be deployed.




.. image:: images/WAN_Topology.png


As shown above, FlexSwitch can be deployed as a P-Router, PE-Router, as well as a CE-Router.
Feature requirements in PE and CE Routers in SP network are most complex.
These Routers need to perform intra- and inter-VPN routing of traffic originated from Customer sites. As carrier grade Routers, they need to support Redundancy, Resiliency, and Restartabality for every feature enabled. For P-Routers, even though requirement of features set is smaller compared to PE-Routers, scale and performance requirement is very high. Most of the Whitebox sulution available today (including FlexSwitch) are 1-RU switches with limited number of ports. Hence, deploying these devices as P-Router may not be feasible for Service Providers. Here we will focus on FlexSwitch deployment as PE and CE Routers.

Capabilities Required
_____________________



Technologies Required
_____________________


Current Support and Plan
________________________




