BGP with 2 nodes 
======================

.. Note:: Make sure you go through ping and install docker tutorial in order to understand docker run commands below



This tutorial will create 2 docker instances named d_inst1 and d_inst2
Router ids assigned to each bgp instance is 10.1.10.2 and 10.1.10.3 with Ips as
40.1.1.1/24 and 40.1.1.2/24 respectively.

Run docker_startup script
"""""""""""""""""""""""""""""
-  create 2 docker instances named d_inst1 and d_inst2 with point to point 
   interfaces eth25 and eth35 created on them respectively.


:: 


   sh docker_startup.sh
    
 
 
Configure d_inst1
"""""""""""""""""""""""""
-  Enter bash shell of d_inst1

::

    sudo docker exec -it d_inst1 bash
 

-Start the flexswitch . Assign IP address to eth25 
 
::

  
    
    Once all daemons are up and running configure IP address.
    
    curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.1/24", "IntfRef": "eth25"}' http://localhost:8080/public/v1/config/IPv4Intf
 
- configure BGP global and bgp neighbor

**BGPGlobal**

*ASNum - This will take unique AS Number*.

*RouterId - Router id key*.


**BGPNeighbor**

*RouteReflectorClusterId - Not mandatory . Configured for iBgp*

*MultiHopTTL - Not mandatory. Default val 0* 

*ConnectRetryTime - Time to wait before connecting to the neighbor in seconds*

*HoldTime - Default is 180 s*

*KeepaliveTime - Tx keepalive frames timer.*

*AddPathsMaxTx - To enable additional paths.*

::


    curl -H "Content-Type: application/json" -d '{"ASNum":500,"RouterId":"10.1.10.2"}' http://localhost:8080/public/v1/config/BGPGlobal
 
    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"PeerAS":500,"NeighborAddress":"40.1.1.2","IfIndex":0,"RouteReflectorClusterId":0,"MultiHopTTL":0,"ConnectRetryTime":60,"HoldTime":180,"KeepaliveTime":60,"AddPathsMaxTx":0}' 'http://localhost:8080/public/v1/config/BGPNeighbor'
 
Configure d_inst2
"""""""""""""""""""""""""
-  Enter d_inst2 shell 
   Below steps are similar to d_inst2 config 
 
::


    sudo docker exec -it d_inst2 bash
  
    /etc/init.d/flexswitch start

    once system is up and running. Configure with Vlan and IP.

    curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.2/24", "IntfRef": "eth35"}' http://localhost:8080/public/v1/config/IPv4Intf
 
- configure BGP
 
::


    curl -H "Content-Type: application/json" -d '{"ASNum":500,"RouterId":"10.1.10.3"}' http://localhost:8080/public/v1/config/BGPGlobal
    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"PeerAS":500,"NeighborAddress":"40.1.1.1","IfIndex":0,"RouteReflectorClusterId":0,"MultiHopTTL":0,"ConnectRetryTime":60,"HoldTime":180,"KeepaliveTime":60,"AddPathsMaxTx":0}' 'http://localhost:8080/public/v1/config/BGPNeighbor'
 

Show commands
""""""""""""""""""

1) Check all bgp neighbors for the given router.

:: 


    curl -H "Accept: application/json" "http://localhost:8080/public/v1/state/BGPNeighbors" | python -m json.tool

   root@a7c16d650d9d:/# curl -H "Accept: application/json" "http://localhost:8080/public/v1/state/BGPNeighbors" | python -m json.tool                                                                             
   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
   100   761  100   761    0     0   263k      0 --:--:-- --:--:-- --:--:--  371k
   {
    "CurrentMarker": 0,
    "MoreExist": false,
    "NextMarker": 0,
    "ObjCount": 1,
    "Objects": [
        {
            "Object": {
                "AddPathsMaxTx": 0,
                "AddPathsRx": false,
                "AuthPassword": "",
                "BfdNeighborState": "",
                "ConnectRetryTime": 60,
                "Description": "",
                "HoldTime": 180,
                "IfIndex": 0,
                "KeepaliveTime": 60,
                "LocalAS": 500,
                "MaxPrefixes": 0,
                "MaxPrefixesDisconnect": false,
                "MaxPrefixesRestartTimer": 0,
                "MaxPrefixesThresholdPct": 80,
                "Messages": {
                    "Received": {
                        "Notification": 0,
                        "Update": 0
                    },
                    "Sent": {
                        "Notification": 0,
                        "Update": 0
                    }
                },
                "MultiHopEnable": false,
                "MultiHopTTL": 0,
                "NeighborAddress": "40.1.1.1",
                "PeerAS": 500,
                "PeerGroup": "",
                "PeerType": 0,
               "Queues": {
                    "Input": 0,
                    "Output": 0
                },
                "RouteReflectorClient": false,
                "RouteReflectorClusterId": 0,
                "SessionState": 6,
                "TotalPrefixes": 0,
                "UpdateSource": ""
            },
            "ObjectId": "b7fec835-9ae9-42b0-4410-7c0a70021970"
        }
     ]
 }

 
2) IPv4 Routes 

::

    curl  -H "Accept: application/json" "http://localhost:8080/public/v1/state/IPv4Routes" | python -m json.tool

3) BGP routes 

::

    curl -i -H "Content-Type: application/json" "http://localhost:8080/public/v1/state/BGPRoutes"
