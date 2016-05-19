.. FlexSwitch documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Installation of FlexSwitch
==========================


FlexSwitch Package Installation
-------------------------------

The SnapRoute FlexSwitch network protocol stack and accompanying toolchain is provided as an installable Debian dpkg package.  The package and can be added to a local repo or installed manually (shown below).


1. SCP flexswitch debian package to the whitebox switch:
   *Default username: admin, default password: snaproute*

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

ONIE Installation
-----------------

Image Deployment
^^^^^^^^^^^^^^^^
ONIE can be used to build out a provisioning environment to automatically deploy images via DHCP and HTTP.  Alternatively, it can be used to manually deploy a single image on a single device with the ONIE console.  Both methods are outlined below.

Setting Up a Basic ONIE Environment
***********************************
Any host can take on the role of an ONIE image server, the only requirements are an HTTP server to host the images and DHCP to serve the URL.  The following instructions detail the process of standing up a new server to fulfil the image hosting requirements.  If a new server is not required, use these steps as a reference for configuration.

Example environment
*******************
For the purposes of this document, a clean install of Ubuntu 14.04 Server is used.

Setup HTTP Server to Host Images
++++++++++++++++++++++++++++++++

1)	Update apt-get package lists:
	$ sudo apt-get update
2)	Install apache2 package to serve as http server:
	$ sudo apt-get install apache2
3)	Create a directory on the in the root www directory for storing ONIE images:
	$ sudo mkdir -p /var/www/html/onie

4)	Copy ONIE image into /var/www/html/onie and validate
	$ cp image_path /var/www/html/onie

	$ ls /var/www/html/onie/
	onie-installer-x86_64-cel_redstone_xp_snapbase

5)	Test image download from another host:
	$ wget http://10.2.10.110/onie/onie-installer-x86_64-cel_redstone_xp_snapbase

Setup DHCP Server
+++++++++++++++++
1)	Update apt-get package lists:
	$ sudo apt-get update
2)	Install apache2 package to serve as http server:
	$ sudo apt-get install isc-dhcp-server
3)	Modify DHCP configuration to serve an IP and an ONIE image URL to the target switch:
	$ sudo vi /etc/dhcp/dhcpd.conf

	**Sample Config:**

	::
		option domain-name-servers 8.8.8.8, 8.8.4.4;
		default-lease-time 86400;
		max-lease-time 86400;
		log-facility local7;

		subnet 10.2.10.0 netmask 255.255.255.0 {
			option routers 10.2.10.1;
			range 10.2.10.2 10.2.10.100;
			option default-url = "http://10.2.10.110/onie/onie-installer-x86_64-cel_redstone_xp_snapbase";
		}

As shown above, the “default-url” DHCP option is used to tell ONIE where to pull the image from.

4)	For the configurations changes to /etc/dhcp/dhcpd.conf to take affect, the service must be restarted:
	$ sudo service isc-dhcp-server restart

ONIE Install Via DHCP
*********************

After the DHCP and HTTP servers are installed and configured, the target switch should discover the ONIE image URL via DHCP and download it automatically.

Here is an example output from the console of an ONIE image installation via DHCP:
::

	** Installer Mode Enabled **
	ONIE:/ # 

	Info: Sleeping for 20 seconds 
	4..3..2..1..Info: eth0:  Checking link... up.
	Info: Trying DHCPv4 on interface: eth0
	ONIE: Using DHCPv4 addr: eth0: 10.2.10.2 / 255.255.255.0
	ONIE: Starting ONIE Service Discovery
	Info: Fetching http://10.2.10.110/onie/onie-installer-x86_64-cel_redstone_xp_snapbase ...
	ONIE: Executing installer: http://10.2.10.110/onie/onie-installer-x86_64-cel_redstone_xp_snapbase
	Verifying image checksum ... OK.
	Preparing image archive ... OK.

The above shows that the target device is receiving an IP address via DHCP of 10.2.10.2, being served the URL to download the ONIE image, and then proceeding to download the image and verify the checksum.

Manual Install Method
*********************

ONIE offers a method of manually installing an image, outside of using a default-url served by DHCP.  All that is required is a DHCP address served to the device and IP reachability to an HTTP server hosting the ONIE image. 

1)	Attach to the target device via the console port and access ONIE shell.
	Until interrupted, ONIE will be looping in discovery mode, trying to download a bootable image for the device:
::

	ONIE:/ # 
	Info: Sleeping for 20 seconds 
	4..3..2..1..Info: eth0:  Checking link... up.
	Info: Trying DHCPv4 on interface: eth0
	ONIE: Using DHCPv4 addr: eth0: 10.1.10.44 / 255.255.255.0
	ONIE: Starting ONIE Service Discovery
	Info: Fetching http://10.1.10.99/onie-installer-x86_64-cel_redstone_xp-r0 ...
	Info: Fetching http://10.1.10.99/onie-installer-x86_64-cel_redstone_xp ...
	Info: Fetching http://10.1.10.99/onie-installer-cel_redstone_xp ...
	Info: Fetching http://10.1.10.99/onie-installer-x86_64 ...
	Info: Fetching http://10.1.10.99/onie-installer ...

2)	Press <Enter> several times to interrupt the discover process and gain access to the BusyBox ONIE console.

3)	Issue “ifconfig” to verify that the management interface is receiving an IP address via DHCP:

::

	ONIE:/ # ifconfig
	eth0      Link encap:Ethernet  HWaddr 00:E0:EC:26:A7:5B
			  inet addr:10.1.10.44  Bcast:10.1.10.255  Mask:255.255.255.0

If eth0 has link, but is not receiving a DHCP address – ONIE defaults to using 192.168.3.10:

::

	ONIE:/ # ifconfig
	eth0      Link encap:Ethernet  HWaddr 00:E0:EC:26:A7:5B  
			  inet addr:192.168.3.10  Bcast:192.168.3.255  Mask:255.255.255.0

4)	Use the “install_url” command to tell ONIE to manually install an image:

::

	ONIE:/ # install_url http://10.1.10.110/onie/onie-installer-x86_64-cel_redstone_xp_snapbase
	Stopping: discover... done.
	Info: Fetching http://10.1.10.110/onie/onie-installer-x86_64-cel_redstone_xp_snapbase ...

5) After the image download is complete, ONIE will verify the checksum and proceed with the installation.

Base Linux NOS
^^^^^^^^^^^^^^

After the image installation, grub will be modified to add an entry for the newly installed Network Operating System (NOS) and the device will reboot into this new OS.

This NOS is indexed as “SnapOS” in grub and is based on Ubuntu 14.04 LTS – with a 3.16.0-29 Linux kernel:

::

	Ubuntu 14.04 LTS localhost ttyS0
	
	localhost login: 

The initial login credentials are:
		Username: admin
		Password: snaproute

The management interface is represented as “eth0” and has a default configuration of DHCP in /etc/network/interfaces:
::

	$ cat /etc/network/interfaces
	iface eth0 inet dhcp
	auto eth0
	
Reinstall NOS
*************
During the course of deployment it may become necessary to “rekick” a device – by forcing ONIE to run on the next reboot.  This prevents the need to reboot with a console attached and manually changing the grub selection during boot.

Force grub to boot into the ONIE menu option during the next reboot:
::

	$ sudo grub-reboot ONIE

If there is a need to clear the above action and revert grub to the default:
::

	$ sudo grub-reboot SnapOS

Alternatively, if remote access via SSH is not available or the OS is in a failed state – an ONIE rekick can be initiated via a console session:

	1)	Connect to the console cable and configure the host device or terminal server with the console settings documented for the target device
	2)	If the device is accessible issue a “sudo reboot” from the console, otherwise physically power-cycle the switch

	3)	When presented with the GRUB menu, select “ONIE” and press <Enter>:

		::
			
								 GNU GRUB  version 2.02~beta2+e4a1fe391

			 +----------------------------------------------------------------------------+
			 | SnapOS                                                                     | 
			 |*ONIE                                                                       |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            | 
			 +----------------------------------------------------------------------------+

				  Use the ^ and v keys to select which entry is highlighted.          
				  Press enter to boot the selected OS, `e' to edit the commands       
				  before booting or `c' for a command-line.            

		The asterisk indicated which option is selected.  There is a several second timeout for the default option (in this example SnapOS) – so it is important to quickly press an arrow key to change the GRUB menu option.

	4)	When the ONIE menu is displayed, select “ONIE: Install OS”:

		::
		
								GNU GRUB  version 2.02~beta2+e4a1fe391

			 +----------------------------------------------------------------------------+
			 |*ONIE: Install OS                                                           | 
			 | ONIE: Rescue                                                               |
			 | ONIE: Uninstall OS                                                         |
			 | ONIE: Update ONIE                                                          |
			 | ONIE: Embed ONIE                                                           |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            |
			 |                                                                            | 
			 +----------------------------------------------------------------------------+

			  Use the ^ and v keys to select which entry is highlighted.          
			  Press enter to boot the selected OS, `e' to edit the commands       
			  before booting or `c' for a command-line.

It may be required to use the “ONIE: Uninstall OS” option – if the ONIE installer fails to partition the flash.  When using the uninstall mode – ONIE will remove the NOS and clear the flash paritions.  After the uninstall is complete – ONIE will automatically restart into the “ONIE: Install OS” mode.

When the ONIE:/ # prompt is available – the steps for loading an image via ONIE can be followed (either DHCP or Manual Install).
	


