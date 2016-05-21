OSPF
===============
This tutorial creates 2 docker containers with flexswitch - ospf1 and ospf2 

Create OSPF containers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  Start 2 docker instances named ospf1 and ospf2


::


   docker run -dt --privileged --log-driver=syslog --cap-add=ALL  --name ospf1 --ip 192.168.0.2 --net=clos-oob-network  -P libero18/ubuntu-14.04:Flexv43
    docker run -dt --privileged --log-driver=syslog --cap-add=ALL --name ospf2  --ip 192.168.0.4 --net=clos-oob-network  -P libero18/ubuntu-14.04:Flexv43

 
- Create interface eth10 on ospf1 and eth20 on ospf2 
 
:: 

    sudo ip link add eth10 type veth peer name eth20

    sudo ip link set eth10 netns $ospf1_pid
    sudo ip netns exec $ospf1_pid ip link set eth10 up

    sudo ip link set eth20 netns $ospf2_pid
    sudo ip netns exec $ospf2_pid ip link set eth20 up


   
 
-  Enter bash shell of ospf2

::
    
    sudo docker exec -it ospf1 bash
 

Configure ospf1 docker
^^^^^^^^^^^^^^^^^^^^^^^^^^
    
-Below commands start flexswitch , create SVI and create IPv4 Interface. ( These commands are similar to SVI creation and ping test)
 
:: 


       /etc/init.d/flexswitch start
 
    curl -X PATCH -H "Content-Type: application/json" -d '{"PortNum": 2, "AdminState":"UP", "Speed":1000, "Autoneg":"OFF"}'  http://localhost:8080/public/v1/config/Port
    (Above command sets the port speed with auto negotiation for the speed OFF)
 
    curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.1/24", "IntfRef": "eth10"}' http://localhost:8080/public/v1/config/IPv4Intf

- Below steps carry out OSPF specific configurations

OspfAreaEntry
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It will configure OSPF area specific params. 
If ospfArea Entry is not added by default area 0.0.0.0 is created. 

**AreaId** = Unique area id . Used as key.

::


    curl -H "Content-Type: application/json" -d '{"AreaId": "0.0.0.2", "AuthType":0, "ImportAsExtern":1, "AreaSummary":1, "AreaNssaTranslatorRole":2, "AreaNssaTranslatorStabilityInterval":40}' http://localhost:8080/public/v1/config/OspfAreaEntry

OspfIfEntry
^^^^^^^^^^^^^^^^^^^^^

IfEntry configures OSPF interface. 

**IfIpAddress** = Ip address of the interface 


**AddressLessIf** = Ip index . Used to configure unnumbered P2P links.


The default IfRtrDeadInterval is 40 s whereas HelloInterval is 10s.

::


    configure Ospf Interface with ip address 40.1.1.1 and area id 0.0.0.2

    curl -H "Content-Type: application/json" -d '{"IfIpAddress": "40.1.1.1", "AddressLessIf":0, "IfAreaId":"0.0.0.2", "IfType":1, "IfAdminStat":1, "IfRtrPriority":1, "IfTransitDelay":1, "IfRetransInterval":5, "IfHelloInterval":10, "IfRtrDeadInterval":40, "IfPollInterval":120, "IfAuthKey":"0.0.0.0.0.0.0.0", "IfMulticastForwarding":1, "IfDemand":false, "IfAuthType":0}' http://localhost:8080/public/v1/config/OspfIfEntry

OspfGlobal
^^^^^^^^^^^^^^
This object will enable the global ospf feature. Unless ospf global is enabled  ,OspfAreaEntry wont take effect. 

**RouterId** = OSPF router id. 

**ASBdrRtrStatus** = set to true if router acts as ASBR.

**TOSSupport** = OSPF TOS support. (Currently not supported.) 

**RestartSupport** = If the process restart is supported.

::


    curl -H "Content-Type: application/json" -d '{"RouterId": "10.1.1.2", "AdminStat":1, "ASBdrRtrStatus":true, "TOSSupport":true, "ExtLsdbLimit":100, "MulticastExtensions":2, "ExitOverflowInterval":1000, "DemandExtensions":true, "RFC1583Compatibility":false, "ReferenceBandwidth":1000, "RestartSupport":1, "RestartInterval":10, "RestartStrictLsaChecking":true, "StubRouterAdvertisement":1}' http://localhost:8080/public/v1/config/OspfGlobal
 


Configure ospf2 docker
^^^^^^^^^^^^^^^^^^^^^^^^^^

- enter bash shell for docker 

::


    sudo docker exec -it ospf1 bash

- Start flex package 

::
    
    /etc/init.d/flexswitch start

- Create Ipv4 interface and assign port speed 

::


    curl -X PATCH -H "Content-Type: application/json" -d '{"PortNum": 2, "AdminState":"UP", "Speed":1000, "Autoneg":"OFF"}'  http://localhost:8080/public/v1/config/Port

    curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.2/24", "IntfRef": "eth20"}' http://localhost:8080/public/v1/config/IPv4Intf
 
- Configure OSPF 

**Ospf Area config**

::


    curl -H "Content-Type: application/json" -d '{"AreaId": "0.0.0.2", "AuthType":0, "ImportAsExtern":1, "AreaSummary":1, "AreaNssaTranslatorRole":2, "AreaNssaTranslatorStabilityInterval":40}' http://localhost:8080/public/v1/config/OspfAreaEntry


**Ospf Interface config** 

::


    curl -H "Content-Type: application/json" -d '{"IfIpAddress": "40.1.1.2", "AddressLessIf":0, "IfAreaId":"0.0.0.2", "IfType":1, "IfAdminStat":1, "IfRtrPriority":1, "IfTransitDelay":1, "IfRetransInterval":5, "IfHelloInterval":10, "IfRtrDeadInterval":40, "IfPollInterval":120, "IfAuthKey":"0.0.0.0.0.0.0.0", "IfMulticastForwarding":1, "IfDemand":false, "IfAuthType":0}' http://localhost:8080/public/v1/config/OspfIfEntry

**Enable global OSPF parameters**

::
    

    curl -H "Content-Type: application/json" -d '{"RouterId": "10.1.1.3", "AdminStat":1, "ASBdrRtrStatus":true, "TOSSupport":true, "ExtLsdbLimit":100, "MulticastExtensions":2, "ExitOverflowInterval":1000, "DemandExtensions":true, "RFC1583Compatibility":false, "ReferenceBandwidth":1000, "RestartSupport":1, "RestartInterval":10, "RestartStrictLsaChecking":true, "StubRouterAdvertisement":1}' http://localhost:8080/public/v1/config/OspfGlobal

 
Show commands 
^^^^^^^^^^^^^^

- Check Ospf Neighbors

::


    curl -H "Accept: application/json" "http://localhost:8080/public/v1/state/OspfNbrEntrys?CurrentMarker=0&NextMarker=0&Count=10" | python -m json.tool
 
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
    100   367  100   367    0     0  58272      0 --:--:-- --:--:-- --:--:-- 61166
   {
    "CurrentMarker": 0,
    "MoreExist": false,
    "NextMarker": 0,
    "ObjCount": 1,
    "Objects": [
        {
            "Object": {
                "NbmaNbrPermanence": 0,
                "NbrAddressLessIndex": 0,
                "NbrEvents": 4,
                "NbrHelloSuppressed": false,
                "NbrIpAddr": "51.1.1.6",
                "NbrLsRetransQLen": 0,
                "NbrOptions": 0,
                "NbrRestartHelperAge": 0,
                "NbrRestartHelperExitReason": 0,
                "NbrRestartHelperStatus": 0,
                "NbrRtrId": "10.1.1.3",
                "NbrState": 7
            },
            "ObjectId": ""
        }
    ]
 }
 
- check LSA database

::

    curl -H "Accept: application/json" "http://localhost:8080/public/v1/state/OspfLsdbEntrys" | python -m json.tool
