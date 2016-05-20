Ping Test 
===============

.. Note :: For this tutorial we assume that  you have docker image installed on you machine.



With this tutorial we are going to spawn 2 docker containers. 
And begin with pinging from interface on 1 docker to the other.

Create containers
**********************

-  Start the docker with flexswitch image on it with below command

Make sure to start the container in privileged mode and syslog options enabled.
::
    
    docker run -dt --privileged --log-driver=syslog --cap-add=ALL  --name docker_ping1 --ip 192.168.0.2 --net=clos-oob-network  -P libero18/ubuntu-14.04:Flexv43
    docker run -dt --privileged --log-driver=syslog --cap-add=ALL --name docker_ping2  --ip 192.168.0.4 --net=clos-oob-network  -P libero18/ubuntu-14.04:Flexv43

-  Create point-to-point link between docker_ping1 and docker_ping2

We create eth10 on docker_ping1 connected to eth20 on docker_ping2


:: 
    
    These commands create eth10 and eth20 interfaces on docker_ping1 and docker_ping2 
    respectiviely.
    sudo ip link add eth10 type veth peer name eth20

    sudo ip link set eth10 netns $spine1_pid
    sudo ip netns exec $spine1_pid ip link set eth10 up

    sudo ip link set eth20 netns $leaf1_pid
    sudo ip netns exec $leaf1_pid ip link set eth20 up


Configure docker_ping1 
^^^^^^^^^^^^^^^^^^^^^^^^^^
-  Enter into the docker shell for docker_ping1

::
    
    sudo docker exec -it docker_ping1 bash


- All below commands are executed on the docker shell. 
   Flexswitch needs syslog and redis-server running before we start to configure. When you run the docker container syslog and redis-server is started at the bootup time. 


- Following script is used to start/stop/restart flexswitch instance. 

::

     /etc/init.d/flexswitch start

- Lets start configuring interface with IP . 

While configuring "IPv4Intf" , "IntfRef" can either be port-name or ifindex.

::
   
   curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.1/24", "IntfRef": "eth10"}' http://localhost:8080/public/v1/config/IPv4Intf

Configure docker_ping2 
^^^^^^^^^^^^^^^^^^^^^^^^^^
-  Run docker_ping2 and start the flexswitch

Following commands are same above  to spawn the container and create an interface 

 
::


    /etc/init.d/flexswitch start
    curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.2/24", "IntfRef": "eth20"}' http://localhost:8080/public/v1/config/IPv4Intf
 

 
- We are ready to ping from docker_ping1

::
     
    ping 40.1.1.2

Debug Commands
^^^^^^^^^^^^^^^^^^^^^

- Check system health 

It shows details if each daemon is up/down along and reason of failure if any. 

:: 

    http://192.168.0.2:8080/public/v1/state/SystemStatus
    Excerpt from the output

    {
    "ObjectId": "",
    "Object": {
    "Name": "c5d463d0c7c8",
    "Ready": true,
    "Reason": "None",
    "UpTime": "53m13.224364167s",
    "NumCreateCalls": "Total 10 Success 1",
    "NumDeleteCalls": "Total 0 Success 0",
    "NumUpdateCalls": "Total 0 Success 0",
    "NumGetCalls": "Total 2 Success 1",
    "NumActionCalls": "Total 0 Success 0",



- check ports populated by flexswitch (This will give you ifindex as well) 

::

    http://192.168.0.2:8080/public/v1/state/Ports


{

"MoreExist": false,

"ObjCount": 2,

"CurrentMarker": 0,

"NextMarker": 3,

"Objects": [

{

"ObjectId": "0c3f2608-ed51-4d04-5d97-c18f7330c9ef",

"Object": {

"PortNum": 1,

"IfIndex": 1,

"Name": "eth0",

"OperState": "UP",

"NumUpEvents": 0,

"LastUpEventTime": "",

"NumDownEvents": 0,

"LastDownEventTime": "",

"Pvid": 4095,

"IfInOctets": 13878,

"IfInUcastPkts": 138,

"IfInDiscards": 1,

"IfInErrors": 0,

"IfInUnknownProtos": 0,

"IfOutOctets": 2744,

"IfOutUcastPkts": 43,

"IfOutDiscards": 0,

"IfOutErrors": 0,

"ErrDisableReason": ""

}

},

{

"ObjectId": "a7ab14fb-c50f-4842-6e23-4d68a711af2d",

"Object": {

"PortNum": 2,

"IfIndex": 2,

"Name": "eth10",

"OperState": "UP",

"NumUpEvents": 0,

"LastUpEventTime": "",

"NumDownEvents": 0,

"LastDownEventTime": "",

"Pvid": 4095,

"IfInOctets": 2508,

"IfInUcastPkts": 39,

"IfInDiscards": 0,

"IfInErrors": 0,

"IfInUnknownProtos": 0,

"IfOutOctets": 2508,

"IfOutUcastPkts": 39,

"IfOutDiscards": 0,

"IfOutErrors": 0,
"ErrDisableReason": ""

}

}

]

}    

- Arp Entries

::

    http://192.168.0.2:8080/public/v1/state/ArpEntrys
  
    {
    "MoreExist": false,
    "ObjCount": 1,
    "CurrentMarker": 0,
    "NextMarker": 0,
    "Objects": [
    {
     "ObjectId": "",
     "Object": {
     "IpAddr": "40.1.1.2",
     "MacAddr": "e6:c9:7f:04:cd:0c",
     "Vlan": "Internal Vlan",
     "Intf": "eth10",
     "ExpiryTimeLeft": "8m38.177476246s"
    }
    }
    ]
   }


