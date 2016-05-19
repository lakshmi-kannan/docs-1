BGP with 2 nodes 
======================


This tutorial will create 2 docker instances named bgp_inst1 and bgp_inst2.
Router ids assigned to each bgp instance is 10.1.10.2 and 10.1.10.3 with Ips as
51.1.1.5/24 and 51.1.1.6/24 respectively.
 
-  create 2 docker instances named bgp_inst1 and bgp_inst2 with given docker image .

:: 


    docker run -d --log-driver=syslog --cap-add=ALL --name bgp_inst1 libero18/ubuntu-14.04:Flexv15
    docker run -d --log-driver=syslog --cap-add=ALL --name bgp_inst2 libero18/ubuntu-14.04:Flexv15
 
-  Below statements create eth1 interface with IP address 20.0.1.5 and bridge it to the host interface Docker0

::

    sudo pipework docker0 -i eth1 bgp_inst1 20.0.1.5/24
    sudo pipework docker0 -i eth1 bgp_inst2 20.0.1.6/24
 
On bgp_inst1
""""""""""""""""""
-  Enter bash shell of bgp_inst1

::

    sudo docker exec -it bgp_inst1 bash
 

-Start the flexswitch . Create  IPv4 Interface. ( These commands are similar to SVI creation and ping test)
 
::


    rsyslogd &
    redis-server &
    /etc/init.d/flexswitch start
    curl -H "Content-Type: application/json" -d '{"VlanId":5,"UntagIfIndexList":"2"}'     http://localhost:8080/public/v1/Vlan
    curl -H "Content-Type: application/json" -d '{"IpAddr": "51.1.1.5/24", "IfIndex":33554437}' http://localhost:8080/public/v1/IPv4Intf
 
- configure BGP global and bgp neighbor

BGP neighbor creates bgp peer configuration  with parameters .. <TODO - Add more details abt params from Harsha. >

::


    curl -H "Content-Type: application/json" -d '{"ASNum":500,"RouterId":"10.1.10.2"}' http://localhost:8080/public/v1/BGPGlobal
 
    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"PeerAS":500,"NeighborAddress":"51.1.1.6","IfIndex":0,"RouteReflectorClusterId":0,"MultiHopTTL":0,"ConnectRetryTime":60,"HoldTime":180,"KeepaliveTime":60,"AddPathsMaxTx":0}' 'http://localhost:8080/public/v1/BGPNeighbor'
 
On bgp_inst2
""""""""""""""""""
-  Enter bgp_inst2 shell and create SVI with IPv4 interface
 
::


    sudo docker exec -it bgp_inst1 bash
    rsyslogd &
    redis-server &
    /etc/init.d/flexswitch start

    once system is up and running. Configure with Vlan and IP.

    curl -H "Content-Type: application/json" -d '{"VlanId":5,"UntagIfIndexList":"2"}' http://localhost:8080/public/v1/Vlan
   curl -H "Content-Type: application/json" -d '{"IpAddr": "51.1.1.6/24", "IfIndex":33554437}' http://localhost:8080/public/v1/IPv4Intf
 
- configure BGP
 
::


    curl -H "Content-Type: application/json" -d '{"ASNum":500,"RouterId":"10.1.10.3"}' http://localhost:8080/public/v1/BGPGlobal
    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"PeerAS":500,"NeighborAddress":"51.1.1.5","IfIndex":0,"RouteReflectorClusterId":0,"MultiHopTTL":0,"ConnectRetryTime":60,"HoldTime":180,"KeepaliveTime":60,"AddPathsMaxTx":0}' 'http://localhost:8080/public/v1/BGPNeighbor'
 
Debug commands
""""""""""""""""""

1) Check all bgp neighbors for the given router.

:: 


    curl -H "Accept: application/json" "http://localhost:8080/public/v1/BGPNeighborStates?CurrentMarker=0&NextMarker=0&Count=10" | python -m json.tool
 
2) IPv4 Routes 

::

    curl -i -H "Accept: application/json" "http://localhost:8080/public/v1/IPv4RouteState?CurrentMarker=0&NextMarker=0&Count=10" | python -m tool
