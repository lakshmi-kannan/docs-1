Ping Test 
===============

.. Note :: For this tutorial we assume that  you have docker image installed on you machine.




With this tutorial we are going to spawn 2 docker containers. 
And begin with pinging from interface on 1 docker to the other.

Run docker_startup script
******************************

This script will create 2 docker instances named d_inst1 and d_inst2 with point to point interfaces eth25 and eth35 created on them respectively.



::
    
    sh docker_startup.sh



Configure d_inst1
^^^^^^^^^^^^^^^^^^^^^^^^^^
-  Enter into the docker shell for d_inst1

::
    
    docker exec -it d_inst1 bash
    (you can install curl using this command - apt-get install curl) 

- All below commands are executed on the docker shell. 
   Flexswitch needs syslog and redis-server running before we start to configure. When you run the docker container syslog and redis-server is started at the bootup time. 


- Lets start configuring interface with IP . 

While configuring "IPv4Intf" , "IntfRef" can either be port-name or ifindex.

::
   
   curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.1/24", "IntfRef": "eth25"}' http://localhost:8080/public/v1/config/IPv4Intf


Configure d_inst2
^^^^^^^^^^^^^^^^^^^^^^^^^^

Login to d_inst2 and configure ipv4 interface

 
::
    
    docker exec -it d_inst2 bash
    (get curl - apt-get install curl) 
    curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.2/24", "IntfRef": "eth35"}' http://localhost:8080/public/v1/config/IPv4Intf
 

 
- We are ready to ping from docker_ping1

::
     
    ping 40.1.1.2


Show Commands
^^^^^^^^^^^^^^^^^^^^^

- Check system health 

It shows details if each daemon is up/down along and reason of failure if any. 

:: 

	$ curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://localhost:8080/public/v1/state/SystemStatus' | python -m json.tool
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

	$ curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://localhost:8080/public/v1/state/Ports' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
	100   926  100   926    0     0   201k      0 --:--:-- --:--:-- --:--:--  226k
	{
    	"CurrentMarker": 0,
    	"MoreExist": false,
    	"NextMarker": 2,
    	"ObjCount": 2,
    	"Objects": [
        	{
            	"Object": {
                	"ErrDisableReason": "",
        	 	"IfInDiscards": 0,
                	"IfInErrors": 0,
                	"IfInOctets": 90084,
                	"IfInUcastPkts": 1123,
                	"IfInUnknownProtos": 0,
                	"IfIndex": 0,
                	"IfOutDiscards": 0,
                	"IfOutErrors": 0,
                	"IfOutOctets": 92902,
                	"IfOutUcastPkts": 1154,
                	"IntfRef": "eth25",
                	"LastDownEventTime": "",
                	"LastUpEventTime": "",
                	"Name": "eth25",
                	"NumDownEvents": 0,
                	"NumUpEvents": 0,
                	"OperState": "UP",
        	 	"PresentInHW": "NO",
                	"Pvid": 3050
            	},
            	"ObjectId": "a3e970f1-b4eb-41dc-4e29-8e0eb9a0ed01"
        	},
        	{
            	"Object": {
                	"ErrDisableReason": "",
                	"IfInDiscards": 0,
        	 	"IfInErrors": 0,
                	"IfInOctets": 0,
                	"IfInUcastPkts": 0,
        	 	"IfInUnknownProtos": 0,
                	"IfIndex": 1,
                	"IfOutDiscards": 0,
                	"IfOutErrors": 0,
                	"IfOutOctets": 0,
                	"IfOutUcastPkts": 0,
                	"IntfRef": "eth0",
                	"LastDownEventTime": "",
                	"LastUpEventTime": "",
        		 "Name": "eth0",
                	"NumDownEvents": 0,
                	"NumUpEvents": 0,
                	"OperState": "Port broken out",
                	"PresentInHW": "NO",
                	"Pvid": 4095
            	},
            	"ObjectId": "38224a9f-e5c0-4152-7945-45215ebeb94d"
        	}
    	]
	}
	root@d28c36ed59e5:/# 

- Arp Entries

::

	$ curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://localhost:8080/public/v1/state/ArpEntrys' | python -m json.tool
	root@d28c36ed59e5:/# curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://localhost:8080/public/v1/state/ArpEntrys' | python -m json.tool
  	% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
        	                         Dload  Upload   Total   Spent    Left  Speed
	100   227  100   227    0     0  32922      0 --:--:-- --:--:-- --:--:-- 37833
	{
    	"CurrentMarker": 0,
    	"MoreExist": false,
    	"NextMarker": 0,
    	"ObjCount": 1,
    	"Objects": [
        	{
            	"Object": {
                	"ExpiryTimeLeft": "6m30.741942761s",
                	"Intf": "eth25",
                	"IpAddr": "40.1.1.2",
                	"MacAddr": "42:52:92:50:68:8e",
                	"Vlan": "Internal Vlan"
            	},
            	"ObjectId": ""
        	}
    	]
	}
	root@d28c36ed59e5:/# 
