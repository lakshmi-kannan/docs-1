OSPF
===============

This tutorial sets up ospf adjacency between 2 interfaces on the docker containers
d_inst1 and d_inst2


Run the docker_startup script
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  Start 2 docker instances named d_inst1 and d_inst2


::


   sh docker_startup.sh
   Get the script here  - https://github.com/OpenSnaproute/test

 

   
 
-  Enter bash shell of d_inst1

::
    
    sudo docker exec -it d_inst1 bash
 

Configure d_inst1 docker
^^^^^^^^^^^^^^^^^^^^^^^^^^

::
      
      Configure IPv4 intf
      curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.1/24", "IntfRef": "eth25"}' http://localhost:8080/public/v1/config/IPv4Intf
   
- Below steps carry out OSPF specific configurations

Ospfv2AreaEntry
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

It will configure OSPF area specific params. 
If ospfArea Entry is not added by default area 0.0.0.0 is created but its admin state will be DOWN. 

**AreaId** = Unique area id . Used as key.

::


    curl  -H "Content-Type: application/json" -d '{"AreaId":"0.0.0.0", "AdminState":"UP"}'  http://localhost:8080/public/v1/config/Ospfv2Area

Ospfv2Intf
^^^^^^^^^^^^^^^^^^^^^

IfEntry configures OSPF interface. 

**IfIpAddress** = Ip address of the interface 


**AddressLessIf** = Ip index . Used to configure unnumbered P2P links.


The default IfRtrDeadInterval is 40 s whereas HelloInterval is 10s.

::


    configure Ospfv2 Interface with ip address 40.1.1.1 

    curl  -H "Content-Type: application/json" -d '{"IpAddress":"40.1.1.1", "AddressLessIfIdx":0, "AdminState":"UP", "Type":"PointToPoint"}'  http://localhost:8080/public/v1/config/Ospfv2Intf
   

Ospfv2Global
^^^^^^^^^^^^^^
This object will enable the global ospf feature. Unless ospf global is enabled  ,Ospfv2AreaEntry wont take effect. 

**RouterId** = OSPF router id. 

**ASBdrRtrStatus** = set to true if router acts as ASBR.


::


     curl -X PATCH -i "Content-Type: application/json" -d '{"Vrf":"default", "RouterId":"10.1.1.1", "AdminState":"UP"}'  http://localhost:8080/public/v1/config/Ospfv2Global




Configure d_inst2 docker
^^^^^^^^^^^^^^^^^^^^^^^^^^

- enter bash shell for docker 

::


    sudo docker exec -it d_inst2 bash


::
      
      Configure IPv4 intf
      curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.2/24", "IntfRef": "eth35"}' http://localhost:8080/public/v1/config/IPv4Intf

- Configure OSPF 

**Ospfv2 Area config**

::


      curl  -H "Content-Type: application/json" -d '{"AreaId":"0.0.0.0", "AdminState":"UP"}'  http://localhost:8080/public/v1/config/Ospfv2Area


**Ospfv2 Interface config** 

::


        curl  -H "Content-Type: application/json" -d '{"IpAddress":"40.1.1.2", "AddressLessIfIdx":0, "AdminState":"UP", "Type":"PointToPoint"}'  http://localhost:8080/public/v1/config/Ospfv2Intf


**Enable global OSPF parameters**

::
    

     curl -X PATCH -i "Content-Type: application/json" -d '{"Vrf":"default", "RouterId":"10.1.1.2", "AdminState":"UP"}'  http://localhost:8080/public/v1/config/Ospfv2Global


 
Show commands 
^^^^^^^^^^^^^^

- Check Ospfv2 Neighbors

::


    curl  -H "Accept: application/json" "http://localhost:8080/public/v1/state/Ospfv2Nbrs" | python -m json.tool
 
   root@snaproute-lab-r815-2:~/git/snaproute/src/test/setups# curl  -H "Accept: application/json" "http://localhost:8080/public/v1/state/Ospfv2Nbrs" | python -m json.tool
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   191  100   191    0     0  90392      0 --:--:-- --:--:-- --:--:--  186k
{
    "CurrentMarker": 0,
    "MoreExist": false,
    "NextMarker": 1,
    "ObjCount": 1,
    "Objects": [
        {
            "Object": {
                "AddressLessIfIdx": 0,
                "IpAddr": "10.1.1.2",
                "Options": 0,
                "RtrId": "10.1.1.2",
                "State": "FULL"
            },
            "ObjectId": ""
        }
    ]
}
 
- check LSA database

::
        curl  -H "Accept: application/json" "http://localhost:8080/public/v1/state/Ospfv2Lsdbs" | python -m json.tool

