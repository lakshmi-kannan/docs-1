Ping Test 
===============

.. Note :: For this tutorial we assume that  you have docker image installed on you machine.



With this tutorial we are going to spawn 2 docker containers. 
And begin with pinging from interface on 1 docker to the other.

Create containers
**********************

-  Start the docker with flexswitch image on it with below command

Make sure to start the container in privileged mode and syslog options enabled.
We have created docker containers with network option "clos-oob-network" . 

::
    
    docker run -dt --privileged --log-driver=syslog --cap-add=ALL  --name docker_ping1 --ip 192.168.0.2 --net=clos-oob-network  -P libero18/ubuntu-14.04:Flexv43
    docker run -dt --privileged --log-driver=syslog --cap-add=ALL --name docker_ping2  --ip 192.168.0.4 --net=clos-oob-network  -P libero18/ubuntu-14.04:Flexv43

-  Create point-to-point link between docker_ping1 and docker_ping2

We create eth10 on docker_ping1 connected to eth20 on docker_ping2
(Note - Get PIDs of docker containers running 
`docker inspect -f '{{.State.Pid}}' docker_ping1`

`docker inspect -f '{{.State.Pid}}' docker_ping2`
)

:: 
    
    These commands create eth10 and eth20 interfaces on docker_ping1 and docker_ping2 
    respectiviely.
    sudo ip link add eth10 type veth peer name eth20
 
    sudo ip link set eth10 netns $<pid_docker_ping1>
    sudo ip netns exec $<pid_docker_ping1> ip link set eth10 up

    sudo ip link set eth20 netns $<pid_docker_ping2>
    sudo ip netns exec $<pid_docker_ping2> ip link set eth20 up


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

Show Commands
^^^^^^^^^^^^^^^^^^^^^

- Check system health 

It shows details if each daemon is up/down along and reason of failure if any. 

:: 

	$ curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://192.168.0.2:8080/public/v1/state/SystemStatus' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100  2940    0  2940    0     0   232k      0 --:--:-- --:--:-- --:--:--  239k
	{
		"Object": {
			"FlexDaemons": [
				{
					"Enable": true,
					"KeepAlive": "Received 5 keepalives",
					"Name": "ribd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:11:01.781882664 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 8 keepalives",
					"Name": "bgpd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:51.859376317 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 4 keepalives",
					"Name": "arpd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:54.183839599 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 4 keepalives",
					"Name": "vxland",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:52.01611385 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 4 keepalives",
					"Name": "dhcpd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:52.307373655 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 5 keepalives",
					"Name": "stpd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:53.812226563 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 4 keepalives",
					"Name": "lldpd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:54.02940049 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 4 keepalives",
					"Name": "bfdd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:11:02.116927367 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 4 keepalives",
					"Name": "confd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:52.074420955 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 5 keepalives",
					"Name": "asicd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:51.773346755 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 4 keepalives",
					"Name": "dhcprelayd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:52.248453375 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 4 keepalives",
					"Name": "vrrpd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:54.899584199 +0000 UTC",
					"State": "up"
				},
				{
					"Enable": true,
					"KeepAlive": "Received 4 keepalives",
					"Name": "lacpd",
					"Reason": "None",
					"RestartCount": 0,
					"RestartReason": "",
					"RestartTime": "",
					"StartTime": "2016-05-20 23:10:52.300769509 +0000 UTC",
					"State": "up"
				}
			],
			"Name": "2cffc37ad362",
			"NumActionCalls": "Total 0 Success 0",
			"NumCreateCalls": "Total 5 Success 3",
			"NumDeleteCalls": "Total 0 Success 0",
			"NumGetCalls": "Total 4 Success 3",
			"NumUpdateCalls": "Total 1 Success 1",
			"Ready": true,
			"Reason": "None",
			"UpTime": "21m28.74429995s"
		},
		"ObjectId": ""
	}



- check ports populated by flexswitch (This will give you ifindex as well) 

::

	$ curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://192.168.0.2:8080/public/v1/state/Ports' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100   869  100   869    0     0   104k      0 --:--:-- --:--:-- --:--:--  121k
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 3,
		"ObjCount": 2,
		"Objects": [
			{
				"Object": {
					"ErrDisableReason": "",
					"IfInDiscards": 2,
					"IfInErrors": 0,
					"IfInOctets": 16759,
					"IfInUcastPkts": 88,
					"IfInUnknownProtos": 0,
					"IfIndex": 1,
					"IfOutDiscards": 0,
					"IfOutErrors": 0,
					"IfOutOctets": 6522,
					"IfOutUcastPkts": 72,
					"LastDownEventTime": "",
					"LastUpEventTime": "",
					"Name": "eth0",
					"NumDownEvents": 0,
					"NumUpEvents": 0,
					"OperState": "UP",
					"PortNum": 1,
					"Pvid": 4095
				},
				"ObjectId": "046c51d1-29aa-41a8-47b0-ae81a5f55320"
			},
			{
				"Object": {
					"ErrDisableReason": "",
					"IfInDiscards": 0,
					"IfInErrors": 0,
					"IfInOctets": 12588,
					"IfInUcastPkts": 177,
					"IfInUnknownProtos": 0,
					"IfIndex": 2,
					"IfOutDiscards": 0,
					"IfOutErrors": 0,
					"IfOutOctets": 4434,
					"IfOutUcastPkts": 72,
					"LastDownEventTime": "",
					"LastUpEventTime": "",
					"Name": "eth10",
					"NumDownEvents": 0,
					"NumUpEvents": 0,
					"OperState": "UP",
					"PortNum": 2,
					"Pvid": 3050
				},
				"ObjectId": "7638f876-0956-45f2-47b7-5e485af1a64a"
			}
		]
	}


- Arp Entries

::

	$ curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://192.168.0.2:8080/public/v1/state/ArpEntrys' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100   227  100   227    0     0  18210      0 --:--:-- --:--:-- --:--:-- 18916
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 0,
		"ObjCount": 1,
		"Objects": [
			{
				"Object": {
					"ExpiryTimeLeft": "9m43.684650453s",
					"Intf": "eth10",
					"IpAddr": "40.1.1.2",
					"MacAddr": "3a:f8:c0:3b:39:d0",
					"Vlan": "Internal Vlan"
				},
				"ObjectId": ""
			}
		]
	}
