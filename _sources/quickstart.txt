QuickStart Guide
================

.. toctree::
   :maxdepth: 1

    Docker Tutorial <dockerIntro>
    Hardware Tutorial <ONIE_install>
    Hardware Support matrix <hwmatrix>



How to use it?
^^^^^^^^^^^^^^

FlexSwitch comes supplied with a configuration manager which supplies the FrontEnd to our system and acts as a light-weight director of RESTful API calls.  This is the portion of the system, that will direct a configuration item to the appropriate daemon or database call.  In order to simplify how these calls are segmented for the user, the API calls are organized into two categories. +State+ and +Config+ operations.  Every object in the system has both a State and Config operation that can be performed against it.  

On the Config portion, this means when you supply the data you want in JSON format and sent to the associated API to have the configuration applied.  These operations can be done in 3 ways:

 - Directly calling the RestFul API
 - Utilizing the supplied Python SDK
 - Pushing configuration via JSON formatted file
 	* File can be managed via Anisble, Puppet, Chef, etc. 
 - Familiar, industry standard CLI 

Utilizing the Rest API
""""""""""""""""""""""

FlexSwitch comes with a RestFul API that can be used for configuration, state querying and troubleshooting of our protocols and system daemons.  Below is a primer on how to interact with this system, utilizing the RestFul API to adjust the ARP global timeout value. 

In order to perform this operation with the Restful API, you would create the correctly structured JSON and send to the ArpConfig REST API:

::

        root@5b5a8d783113:/# curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ArpConfigKey":"1", "Timeout":1000}' http://localhost:8080/public/v1/config/ArpConfig
        {"ObjectId":"a97b920d-8b10-47b1-7ea9-890b07f6e712","Error":""}
  
As you can see This is a 1:1 mapping of config to a specifc Object, in this case Timeout value of 1000 to ARP.


On the State side, this is more invovled, since you can have multiple items, that could potentially have thousand of different states.  Think the prefixes/next-hop entries` in the routing table or multiple IP/MAC mappings with an ARP table.  Due to this variance in data supplied, State operations are broken down into GetBulk, which supplies information from the entire object OR just an indiviual Get, which returns, just the parameters requested from an object.  The way in which these calls are made is based on the pluralization of the object itself.  

Lets use ARP again as an example.  If you wished to grab all entry's from the ARP table, you would query the "+ArpEntry+" state object. However, in order to dictate you wanted all entires, rather than a specific value, you would add a trailing "+s+" to make the operation plural, resulting in a call of "+ArpEntrys+", see below:

::

        root@5c3bca6fb77e:/# curl -X GET --header 'Content-Type: application/json' 'http://localhost:8080/public/v1/state/ArpEntrys' | python -m json.tool
          % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                         Dload  Upload   Total   Spent    Left  Speed
        100   213  100   213    0     0  44654      0 --:--:-- --:--:-- --:--:-- 53250
        {
            "CurrentMarker": 0,
            "MoreExist": false,
            "NextMarker": 0,
            "ObjCount": 1,
            "Objects": [
                {
                    "Object": {
                        "ExpiryTimeLeft": "9m57.74904463s",
                        "Intf": "eth1",
                        "IpAddr": "51.1.1.5",
                        "MacAddr": "4e:8c:3d:c8:d4:09",
                        "Vlan": "5"
                    },
                    "ObjectId": ""
                }
            ]
        }


If you attempted to make such a call to just "+ArpEntry+", you would be returned an error:

::

	root@5c3bca6fb77e:/# curl  -H "Accept: application/json" "http://localhost:8080/public/v1/state/ArpEntry" | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
					 Dload  Upload   Total   Spent    Left  Speed
	100   119  100   119    0     0  21715      0 --:--:-- --:--:-- --:--:-- 23800
	{
	    "Error": "Failed to find entry. Internal error processing GetArpEntryState: Unable to find Arp entry for given IP: \n"
	}

This is due to the fact, that configruation manager expected JSON data to be supplied requesting a specific parameter to search the ARP table on. 


In order to sucessfully, complete the "+ArpEntry+" query, we will supply JSON data for IP address 51.1.1.5:

::

        root@5c3bca6fb77e:/# curl -X GET --header 'Content-Type: application/json' -d '{"IpAddr":"51.1.1.5"}' 'http://localhost:8080/public/v1/state/ArpEntry' | python -m json.tool
          % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                         Dload  Upload   Total   Spent    Left  Speed
        100   157  100   136  100    21  25185   3888 --:--:-- --:--:-- --:--:-- 27200
        {
            "Object": {
                "ExpiryTimeLeft": "9m56.277773536s",
                "Intf": "eth1",
                "IpAddr": "51.1.1.5",
                "MacAddr": "4e:8c:3d:c8:d4:09",
                "Vlan": "5"
            },
            "ObjectId": ""
        }

The call now returns sucessfully with the requested data.  Also note, that returned data is no longer wrapped in GetBulk "+Objects+" header; I.E. the following is missing:
::

            "CurrentMarker": 0,
            "MoreExist": false,
            "NextMarker": 0,
            "ObjCount": 1,
            "Objects": [{}]



This is due to the fact, that only a single object of data was targeted, rather than a bulk operation. The extra object data is not required for a GetBulk operation. 

 

Utilizing the Python SDK 
""""""""""""""""""""""""

FlexSwitch comes with a Python SDK that can be utilized for configuration, state querying and troubleshooting of our protocols and system daemons.  This module can be imported to a python script you have written to deploy the system or grab state on a periodic basis. 
Below is a primer on how to interact with this system, utilizing the Python SDK to adjust the ARP global timeout value. 

In order to perform this operation with the Python SDK API, you would utilize the following python methods:



::  

	>>>from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).createArpConfig("1", 1000)
	({u'ObjectId': u'45dff5a0-7dc1-441d-723d-ccf731186ece', u'Error': u''}, None)      

.. Note:: the ObjectID and UUID are the same.


As you can see This is a 1:1 mapping of config to a specifc Object, in this case Timeout value of 1000 to ARP.


On the State side, this is more invovled, since you can have multiple items, that could potentially have thousand of different states.  Think the prefixes/next-hop entries in the routing table or multiple IP/MAC mappings with an ARP table.  Due to this variance in data supplied, State operations are broken down into GetBulk, which supplies information from the entire object OR just an indiviual Get, which returns, just the parameters requested from an object.  The way in which these calls are made is performed by utilizing the method with "+getAll+" followed by the Object you wanted to grab; I.E. Arp, Bfd, BGP, etc.  

Lets use ARP again as an example.  If you wished to grab all state entry's from the ARP table, you would utilize the "+getAllArpEntryStates()+" method. With all Python SDK methods, see below:


::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).getAllArpEntryStates()
	[{u'Object': {u'ConfigObj': None, u'Intf': u'fpPort47', u'Vlan': u'Internal Vlan', u'IpAddr': u'172.16.0.14', u'ExpiryTimeLeft': u'9m24.869691096s', u'MacAddr': u'a8:9d:21:aa:8e:01'}, u'ObjectId': u''}, {u'Object': {u'ConfigObj': None, u'Intf': u'fpPort49', u'Vlan': u'Internal Vlan', u'IpAddr': u'172.16.0.20', u'ExpiryTimeLeft': u'9m43.991376701s', u'MacAddr': u'00:02:03:04:05:00'}, u'ObjectId': u''}]


If you wanted to make  a call to just grab a specific Arp Entry from the state table, you would utilize method, getArpEntryStates(), see below:

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).getArpEntryState("172.16.0.20")
	({u'Object': {u'ConfigObj': None, u'Intf': u'fpPort49', u'Vlan': u'Internal Vlan', u'IpAddr': u'172.16.0.20', u'ExpiryTimeLeft': u'16m38.505153914s', u'MacAddr': u'00:02:03:04:05:00'}, u'ObjectId': u''}, None)


The call now returns sucessfully with only the requested data. 



Configuration via JSON File
***************************
In addition to configuring FlexSwitch via API calls or the Python SDK – it is also possible to supply a configuration file formatted in JSON.

For example, this JSON file will configure these parameters from the previous examples:

3 Vlans are created:
	- Vlan 100, ports 1-10 with IP address 10.10.100.1/24
	- Vlan 200, ports 11,12 with IP address 10.10.101.1/24
	- Vlan 300, ports 13-15, and 17 with IP address 10.10.102.1/24
	- Speed is set to 1G for port 1
	
Example desiredConfig.json:

	::

		{
			"Vlan": [
				{
					"UntagIntfList": "1-10",
					"IntfList": "",
					"VlanId": 100
				},
				{
					"UntagIntfList": "11,12",
					"IntfList": "",
					"VlanId": 200
				},
				{
					"UntagIntfList": "13-15,17",
					"IntfList": "",
					"VlanId": 300
				}
			],
			"IPv4Intf": [
				{
					"IntfRef": "vlan100",
					"IpAddr": "10.10.100.1/24"
				},
				{
					"IntfRef": "vlan200",
					"IpAddr": "10.10.101.1/24"
				},
				{
					"IntfRef": "vlan300",
					"IpAddr": "10.10.102.1/24"
				}
			],
			"Port": [
					{
					"PortNum": 1,
					"Speed": 1000
				}
			]
		}

This JSON file is declarative and not order-dependent – all configurations are ingested at once and executed in the order required.


Configuration files are parsed and executed using the “monitor.py” python app:


	1) Add JSON configuration to desiredConfig.json (creating the file, if necessary):
		::
			
			$ vi /opt/flexswitch/desiredConfig.json
 
	2) Apply the configuration using monitor.py in the /opt/flexswitch/apps/cfgmon directory:
		::
		
			$ cd /opt/flexswitch/apps/cfgmon

			$ python monitor.py --applyConfig=True

			Namespace(applyConfig=True, cfgDir='/opt/flexswitch/', ip='localhost', poll=None, port='8080', saveConfig=True)
			System Is ready
			Configuration is saved to /opt/flexswitch//runningConfig.json
			Updating object Port
			Creating Object Vlan
			Creating Object Vlan
			Creating Object Vlan
			Creating Object IPv4Intf
			Creating Object IPv4Intf
			Creating Object IPv4Intf

Now that the configuration is applied, the operational state can be verified:

http://10.1.10.43:8080/public/v1/state/IPv4Intfs


.. image:: images/python_IPv4Intfs_config.png

Ansible Integration
*******************
Utilizing the JSON file method, it is possible to utilize automation tools like Ansible to manage FlexSwitch configurations.

Prerequisites:
Prior to utilizing Ansible to manage FlexSwitch, a working Ansible environment needs to be built.

	1) Follow the Operating System appropriate instructions to install Ansible on the desired host:
		::
		
			http://docs.ansible.com/ansible/intro_installation.html

			For the purposes of this guide, these steps were performed on an Ubuntu Server running 14.04:

			$ sudo apt-get install software-properties-common
			$ sudo apt-add-repository ppa:ansible/ansible
			$ sudo apt-get update
			$ sudo apt-get install ansible

	2) Generate an SSH key for Ansible to use for managing devices:
		::
			$ ssh-keygen

			For the purposes of this guide a passphrase is not used and the key is stored in the default location: /home/ansible/.ssh/id_rsa.pub.

	3) This generated SSH key needs to be added to the root user of the device, enabling SSH management by Ansible:
		::
		
			On the device to be managed by Ansible:

			$ sudo mkdir -p /root/.ssh/
			$ sudo vi /root/.ssh/authorized_keys

			Add the contents of id_rsa.pub from the user on the device running Ansible to this authorized_keys file.  The id_rsa.pub contents should be one line and follow this format:

			ssh-rsa <snip> ansible@ansible-server.snaproute.com

	4) Add target host to /etc/ansible/hosts:
		::
		
			$ sudo vi /etc/ansible/hosts

			Add hosts as either IP or resolvable hostname, one on each line.  The /etc/ansible/hosts inventory file can be simply a list of hosts or it can be more complex and define groups – as outlined in the example.

			For this example, here is the contents of the Ansible inventory file:

			$ cat /etc/ansible/hosts
			10.1.10.43

	5) The ssh key can be tested by issuing a “ping” from Ansible:
		::

			$ ansible -u root -m ping all

			10.1.10.43 | SUCCESS => {
				"changed": false, 
				"ping": "pong"
			}

			The above shows a successful ping response using the remote user of root, as that is the user that houses the SSH key on the target system.







