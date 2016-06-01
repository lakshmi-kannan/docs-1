.. FlexSwitch documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.
   
Installed FlexSwitch with ONIE
==============================

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
	
