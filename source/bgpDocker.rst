BGP with 2 nodes 
======================

:.. Note :: Make sure you go through ping and install docker tutorial in order to understand docker run commands below


This tutorial will create 2 docker instances named bgp_inst1 and bgp_inst2.
Router ids assigned to each bgp instance is 10.1.10.2 and 10.1.10.3 with Ips as
40.1.1.1/24 and 40.1.1.2/24 respectively.
 
-  create 2 docker instances named bgp_inst1 and bgp_inst2 with given docker image .

:: 


    docker run -dt --privileged --log-driver=syslog --cap-add=ALL  --name bgp_inst1 --ip 192.168.0.2 --net=clos-oob-network  -P libero18/ubuntu-14.04:Flexv43
    docker run -dt --privileged --log-driver=syslog --cap-add=ALL --name bgp_inst2  --ip 192.168.0.4 --net=clos-oob-network  -P libero18/ubuntu-14.04:Flexv43
 
-  Below statements create interface eth10 on bgp_inst1 and eth20 on bgp_inst2

:: 
    
    sudo ip link add eth10 type veth peer name eth20

    sudo ip link set eth10 netns $spine1_pid
    sudo ip netns exec $<pid_of_bgp_inst1> ip link set eth10 up

    sudo ip link set eth20 netns $leaf1_pid
    sudo ip netns exec $<pid_of_bgp_inst2> ip link set eth20 up
 
Configure bgp_inst1
"""""""""""""""""""""""""
-  Enter bash shell of bgp_inst1

::

    sudo docker exec -it bgp_inst1 bash
 

-Start the flexswitch . Assign IP address to eth10 
 
::

    /etc/init.d/flexswitch start
    
    Once all daemons are up and running configure IP address.
    
    curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.1/24", "IntfRef": "eth10"}' http://localhost:8080/public/v1/config/IPv4Intf
 
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
 
Configure bgp_inst2
"""""""""""""""""""""""""
-  Enter bgp_inst2 shell 
   Below steps are similar to bgp_inst1 config 
 
::


    sudo docker exec -it bgp_inst1 bash
  
    /etc/init.d/flexswitch start

    once system is up and running. Configure with Vlan and IP.

    curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.2/24", "IntfRef": "eth20"}' http://localhost:8080/public/v1/config/IPv4Intf
 
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
