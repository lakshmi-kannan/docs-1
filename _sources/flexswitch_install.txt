.. FlexSwitch documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

FlexSwitch Package Installation
===============================

The SnapRoute FlexSwitch network protocol stack and accompanying toolchain is provided as an installable Debian dpkg package.  The package and can be added to a local repo or installed manually (shown below).


1. SCP flexswitch debian package to the whitebox switch:
   .. Note:: Default username: admin, default password: snaproute

	:: 
	
		$ scp flexswitch_0.0.80_amd64.deb admin@10.1.10.240:./
		admin@10.1.10.240's password: 
		flexswitch_0.0.80_amd64.deb                                                                                                                                                    100%   59MB   9.9MB/s   00:06 ``

2. Once complete login to the whitebox switch and utilize dpkg to install package on the system:

	:: 
	
		admin@localhost:~$ sudo dpkg -i flexswitch_0.0.80_amd64.deb 
		(Reading database ... 20599 files and directories currently installed.)
		Preparing to unpack flexswitch_0.0.80_amd64.deb ...
		Getting MAC address
		Stopping Daemon asicd
		Stopping Daemon sysd
		Stopping Daemon ribd
		Stopping Daemon bfdd
		Stopping Daemon arpd
		Stopping Daemon bgpd
		Stopping Daemon ospfd
		Stopping Daemon lacpd
		Stopping Daemon dhcprelayd
		Stopping Daemon stpd
		Stopping Daemon vrrpd
		Stopping Daemon lldpd
		Stopping Daemon vxland
		Stopping Daemon confd
		preinst INSTALL called with argument `upgrade'
		Unpacking flexswitch (0.0.80) over (0.0.80) ...
		Setting up flexswitch (0.0.80) ...
		postinst Configure called with unknown argument `configure'
		Getting MAC address
		Starting Daemon asicd Params: -params=/opt/flexswitch/params
		Starting Daemon sysd Params: -params=/opt/flexswitch/params
		Starting Daemon ribd Params: -params=/opt/flexswitch/params
		Starting Daemon bfdd Params: -params=/opt/flexswitch/params
		Starting Daemon arpd Params: -params=/opt/flexswitch/params
		Starting Daemon bgpd Params: -params=/opt/flexswitch/params
		Starting Daemon ospfd Params: -params=/opt/flexswitch/params
		Starting Daemon lacpd Params: -params=/opt/flexswitch/params
		Starting Daemon dhcprelayd Params: -params=/opt/flexswitch/params
		Starting Daemon stpd Params: -params=/opt/flexswitch/params
		Starting Daemon vrrpd Params: -params=/opt/flexswitch/params
		Starting Daemon lldpd Params: -params=/opt/flexswitch/params
		Starting Daemon vxland Params: -params=/opt/flexswitch/params
		Starting Daemon confd Params: -params=/opt/flexswitch/params
		Total time taken to start all 14 daemons is  0:00:28.025121
		Processing triggers for libc-bin (2.19-18+deb8u4) ...
		admin@localhost:~$`` 

3. Verify FlexSwitch is up and all daemons are running 

	::
		curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.243:8080/public/v1/state/SystemStatus' | python -m json.tool
		  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
										 Dload  Upload   Total   Spent    Left  Speed
		100  2949    0  2949    0     0   330k      0 --:--:-- --:--:-- --:--:--  359k

		{
			"Object": {
				"Name": "rxp-tor-ru40",
				"NumActionCalls": "Total 0 Success 0",
				"NumCreateCalls": "Total 16 Success 14",
				"NumDeleteCalls": "Total 0 Success 0",
				"NumGetCalls": "Total 11 Success 10",
				"NumUpdateCalls": "Total 3 Success 2",
				"Ready": true,
				"Reason": "None",
				"UpTime": "15h34m45.905629054s"	
				"FlexDaemons": [
					{
						"Enable": true,
						"KeepAlive": "Received 2 keepalives",
						"Name": "asicd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:42:13.021281962 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 1 keepalives",
						"Name": "bfdd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:42:19.168999062 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 1 keepalives",
						"Name": "arpd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:42:15.169367385 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 1 keepalives",
						"Name": "dhcprelayd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:41:59.211601355 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 2 keepalives",
						"Name": "vxland",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:42:13.035179142 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 2 keepalives",
						"Name": "ribd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:42:18.729224609 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 1 keepalives",
						"Name": "vrrpd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:42:15.313853582 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 4 keepalives",
						"Name": "bgpd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:41:58.813972783 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 1 keepalives",
						"Name": "confd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:41:59.135234435 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 1 keepalives",
						"Name": "dhcpd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:41:59.207273785 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 1 keepalives",
						"Name": "stpd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:42:15.404720612 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 1 keepalives",
						"Name": "lldpd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:42:15.244707926 -0700 PDT",
						"State": "up"
					},
					{
						"Enable": true,
						"KeepAlive": "Received 1 keepalives",
						"Name": "lacpd",
						"Reason": "None",
						"RestartCount": 0,
						"RestartReason": "",
						"RestartTime": "",
						"StartTime": "2016-05-17 18:41:59.36188443 -0700 PDT",
						"State": "up"
					}
				],
			},
			"ObjectId": ""
		}

5. Verify the switch is running the correct version:

	::
		
		curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.243:8080/public/v1/state/SystemSwVersion' | python -m json.tool
		  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
										 Dload  Upload   Total   Spent    Left  Speed
		100  1283  100  1283    0     0   216k      0 --:--:-- --:--:-- --:--:--  250k
		{
			"Object": {
				"FlexswitchVersion": "1.0.0.101",
				"Repos": [
					{
						"Branch": "master",
						"Name": "l2",
						"Sha1": "5b86f674d3c72c8dd46bae393e17482b8c562b60",
						"Time": "Tue May 17 09:37:13 2016 -0700"
					},
					{
						"Branch": "master",
						"Name": "l3",
						"Sha1": "c09d7cfaff49cfc9437c695f2f49bfca5b4468ba",
						"Time": "Tue May 17 09:37:46 2016 -0700"
					},
					{
						"Branch": "master",
						"Name": "utils",
						"Sha1": "80108d345dcbd01a5ffc3af9c7a4322ba8e702c7",
						"Time": "Tue May 17 09:38:53 2016 -0700"
					},
					{
						"Branch": "master",
						"Name": "asicd",
						"Sha1": "f03366887e07531a52ad8f25197466b9af7f169f",
						"Time": "Tue May 17 09:35:56 2016 -0700"
					},
					{
						"Branch": "master",
						"Name": "config",
						"Sha1": "9813b1df844bbeaa40d4cdd69d1613a256deb370",
						"Time": "Tue May 17 09:36:24 2016 -0700"
					},
					{
						"Branch": "master",
						"Name": "models",
						"Sha1": "46e3a29ffe9c07b2b7b6bdeefeb801dcb016d1e8",
						"Time": "Tue May 17 09:38:17 2016 -0700"
					},
					{
						"Branch": "master",
						"Name": "infra",
						"Sha1": "271790a06452894aa9305fbbc842980a1a0961fd",
						"Time": "Tue May 17 09:36:51 2016 -0700"
					},
					{
						"Branch": "master",
						"Name": "vendors",
						"Sha1": "commit",
						"Time": "Fri May 13 09:48:01 2016 -0700"
					},
					{
						"Branch": "master",
						"Name": "flexSdk",
						"Sha1": "fcbf47f392b84dd050db4fd5fc2dc1b919c2a767",
						"Time": "Fri May 13 16:20:28 2016 -0700"
					},
					{
						"Branch": "master",
						"Name": "apps",
						"Sha1": "6965c05b1be95e7ea4f7493a251637c21237867a",
						"Time": "Wed Apr 27 13:51:06 2016 -0700"
					}
				]
			},
			"ObjectId": ""
		}			
			
4. Change the daemons that start and are running on the system. 

	a. Start/Stop daemons via RestAPI:
		::
			
			To be Filled in with example to start/stop daemon


	b. On Linux edit the file /opt/flexswitch/params/clients.json and remove or add daemon specific JSON, I.E. *{"Name": "<daemon>", "Port": <port-number>}*

		::

			[
				{"Name": "asicd",
				 "Port": 10000},

				{"Name": "bgpd",
				 "Port": 10001},

				{"Name":"ribd",  
				 "Port":10002},
	
				{"Name":"arpd", 
				 "Port":10003},
		
				{"Name":"lacpd",
				 "Port":10004},

				{"Name":"ospfd",
				 "Port":10005},
	
				{"Name":"stpd",
				 "Port":10006},

				{"Name":"dhcprelayd",
				 "Port": 10007},

				{"Name":"bfdd",
				 "Port":10008},

				{"Name":"vrrpd",
				 "Port":10009},

				{"Name":"sysd",
				 "Port":10010},
	
				{"Name":"lldpd",
				 "Port":10011},
	
				{"Name":"vxland",
				 "Port":10012},
	
				{"Name":"dhcpd",
				 "Port":10013},

			   {"Name":"local",
				  "Port":0}
			]

		If you wanted to remove BGPd or STPd from running on start, you would remove these JSON objects:
		
			::
				
				{"Name": "bgpd",
				"Port": 10001},
				{"Name":"stpd",
			 	"Port":10006},			
			 
		Resulting in the following:
			::
				
				[
				{"Name": "asicd",
				 "Port": 10000},

				{"Name":"ribd",  
				 "Port":10002},
	
				{"Name":"arpd", 
				 "Port":10003},
		
				{"Name":"lacpd",
				 "Port":10004},

				{"Name":"ospfd",
				 "Port":10005},

				{"Name":"dhcprelayd",
				 "Port": 10007},

				{"Name":"bfdd",
				 "Port":10008},

				{"Name":"vrrpd",
				 "Port":10009},

				{"Name":"sysd",
				 "Port":10010},
	
				{"Name":"lldpd",
				 "Port":10011},
	
				{"Name":"vxland",
				 "Port":10012},
	
				{"Name":"dhcpd",
				 "Port":10013},

			   {"Name":"local",
				  "Port":0}
			]

		.. Note:: ASICD and SYSD is required for system function.  These daemons can not be removed from this file.  FlexSwitch will not function, if these daemons are not set to start. 



