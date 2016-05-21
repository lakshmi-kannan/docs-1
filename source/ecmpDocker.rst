ECMP
==============

Flexswitch supports configuration of ECMP for different protocols.

To configure the IPv4 Route following parameters would change based on protocol

- **Cost** =  Protocol based cost for the  route.

- **Protocol** = This could be STATIC/OSPF/BGP.

- **DestinationNw NetworkMask** = Destination n/w id and mask.

Here is the REST template for configuration

Static Route
^^^^^^^^^^^^^^^^^^^^^

:: 
   
    **Static route** 
    
   curl -H POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"DestinationNw":"61.1.1.0","NetworkMask":"255.255.255.0","NextHopIp":"51.1.1.6","Cost":0,"OutgoingIntfType":"VLAN","OutgoingInterface":"5","Protocol":"STATIC"}' 'http://localhost:8080/public/v1/config/IPv4Route'

    route -n 

    Kernel IP routing table

    Destination     Gateway         Genmask         Flags Metric Ref    Use Iface

    0.0.0.0         172.17.42.1     0.0.0.0         UG    0      0        0 eth0

    51.1.1.0        0.0.0.0         255.255.255.0   U     0      0        0 vlan5

    61.1.1.0        51.1.1.6        255.255.255.0   UG    0      0        0 vlan5 <-- ECMP route 

    61.1.1.0        71.1.1.6        255.255.255.0   UG    0      0        0 vlan6 <-- ECMP route

   71.1.1.0        0.0.0.0         255.255.255.0   U     0      0        0 vlan6

   172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 eth0

   root@364c318a3017:/# 
 
BGP
^^^^^^^^^^^^^^^^^^^^^

BGP has different parameters in Global object to configure ECMP 
    
    UseMultiplePath - to enable/disable ECMP

    EBGPMaxPaths - max number of ECMP to install from EBGP Peers

    IBGPMaxPaths - max number of ECMP to install from IBGP Peers

::

    **BGP with ECMP**
    
   curl -H "Content-Type: application/json" -d '{"ASNum": 500, "RouterId": "127.0.0.1", "UseMultiplePaths": true, "EBGPMaxPaths": 2, "IBGPMaxPaths": 2}' http://10.1.10.243:8080/public/v1/BGPGlobalConfig 

    
OSPF
^^^^^^^^^^^^^^^^^^^^^
    With current implementation ECMP is enabled by default for the OSPF. 
   
