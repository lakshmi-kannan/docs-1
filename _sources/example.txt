.. FlexSwitchSDK documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. sectnum::

Configuration Examples 
========================================

Configuring ARP
---------------

The ARP protocol is utilized to be learn the layer 2 MAC address of a directly attached device and associate it with an IP address in which to communicate.  ARPd is the daemon on FlexSwitch that manages, learns, and programs layer 2 adjancency information into the data-plane.   

Timeout Values
^^^^^^^^^^^^^^
FlexSwitch supports the ability to change the ARP timers Globally.  The default timeout value is 10 minutes(600 seconds).  ARP daemon will attempt refresh of the ARP entry at the following intervals, with example times based on default timer and number of attempts:

	- 50% of ARP timeout (300 seconds, 1 ARP request frame sent)
	- 25% of ARP timeout (150 seconds, 1 ARP request frame sent)

With more aggressve attempts in the last minute for timeout:

	- 60 seconds of ARP Timeout (1 ARP request frame sent)
	- 30 seconds remaining in ARP Timeout (1 ARP request frame sent)
	- 10 seconds remaining in ARP timeout (10 ARP request frames sent)

Configuring  with Rest API 
"""""""""""""""""""""""""""""""""""""

FlexSwitch has a REST based API, and below is an example utilzing Linux cURL: 

**COMMAND:**
::
	
	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"Vrf":"VRF Name", "Timeout":<*Timeout Value in seconds*>}' 'http://<*your-switchip*>:8080/public/v1/config/ArpGlobal'
	

**OPTIONS:**

+------------+------------+-------------------------------------------+----------+----------+
| Variables  | Type       |  Description                              | Required |  Default |   
+============+============+===========================================+==========+==========+ 
|     Vrf    | string     | VRF name where configuration is applied.  |    No    | "default"|
+------------+------------+-------------------------------------------+----------+----------+
| Timeout    | integer    | Length of ARP timeout in seconds.         |    Yes   |    600s  |   
+------------+------------+-------------------------------------------+----------+----------+ 


**EXAMPLE:**
::
	
	root@5b5a8d783113:/# curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"Vrf":"default", "Timeout":1000}' http://localhost:8080/public/v1/config/ArpGlobal
	{"ObjectId":"a97b920d-8b10-47b1-7ea9-890b07f6e712","Error":""}


	root@5b5a8d783113:/# curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:8080/public/v1/config/ArpGlobals | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
					 Dload  Upload   Total   Spent    Left  Speed
	100   174  100   174    0     0  87087      0 --:--:-- --:--:-- --:--:--  169k
	{
	    "CurrentMarker": 0,
	    "MoreExist": false,
	    "NextMarker": 0,
	    "ObjCount": 1,
	    "Objects": [
		{
		    "Object": {
			"Vrf": "default",
			"Timeout": 1000
		    },
		    "ObjectId": "a97b920d-8b10-47b1-7ea9-890b07f6e712"
		}
	    ]
	}



Configuring with Python SDK
""""""""""""""""""""""""""""""""""

Setting the ARP Timeout to 1000 seconds via FlexSwitch's Python SDK, utilizing method *createArpGlobal()*.

**COMMAND:**
::

	>>> FlexSwitch("*Switch IP*", *TCP port*).createArpGlobal("<*VRF*>",<"*Timeout*">)
	
**OPTIONS:**
	
+------------------+------------+------------+-------------------------------------------+----------+----------+
| Python Method    | Variables  | Type       |  Description                              | Required |  Default |   
+==================+============+============+===========================================+==========+==========+ 
| createArpGlobal  |    Vrf     | string     | VRF name where configuration is applied.  |    No    | "default"|
+                  +------------+------------+-------------------------------------------+----------+----------+
|                  | Timeout    | integer    | Length of ARP timeout in seconds.         |    Yes   |    600s  |   
+------------------+------------+------------+-------------------------------------------+----------+----------+   


**EXAMPLE:**

Below are examples for utilizing this method via the Python CLI, python script and Displaying the results 

1. Python CLI:


::  

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).createArpGlobal("default", 1000)
	({u'ObjectId': u'45dff5a0-7dc1-441d-723d-ccf731186ece', u'Error': u''}, None)      

	>>> FlexSwitch("10.1.10.243", 8080).getAllArpGlobals()
	[{u'Object': {u'ConfigObj': None, u'Vrf': u'default', u'Timeout': 1000}, u'ObjectId': u'45dff5a0-7dc1-441d-723d-ccf731186ece'},

.. Note:: the ObjectID and UUID are the same.

2. Utilizing a Python Script to set ARP timeout

::

	#!/usr/bin/python
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		Timeout=1000
		restIf = FlexSwitch(switch_ip, 8080)
		restIf.createArpGlobal("default",Timeout)


3. Display results of this change:

::

	#!/usr/bin/python
	import json
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		print json.dumps(restIf.getAllArpGlobals(), indent=4)

Output:

::

	acasella@snaproute-lab-r710-1:~$ python getarpglobal.py
	[
	    {
		"Object": {
		    "Vrf": "default",
		    "Timeout": 1000
		}, 
		"ObjectId": "e607400d-71f1-4fd2-4574-e40d313fd3e7"
	    }
	]

Configuring via Configuration file 
""""""""""""""""""""""""""""""""""

-----------------

Configuring Static Entries
^^^^^^^^^^^^^^^^^^^^^^^^^^

Configuring with Rest API 
""""""""""""""""""""""""""""""""

FlexSwitch has a REST based API, and below is an example utilzing Linux cURL:

**COMMAND:**
::

        curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"IP":"<*IPv4 Address*>", "MAC":"<*MAC address*>"}' 'http://<*your-switchip*>:8080/public/v1/config/ArpConfig'


**OPTIONS:**

+------------+------------+---------------------------------------------------+----------+----------+
| Variables  | Type       |  Description                                      | Required |  Default |    
+============+============+===================================================+==========+==========+  
| IP         | String     | IPv4 address to have a static entry applied       |    Yes   |   None   |
+------------+------------+---------------------------------------------------+----------+----------+
| MAC        | String     | Layer 2 MAC address associated with IPv4 address. |    Yes   |   None   |   
+------------+------------+---------------------------------------------------+----------+----------+  

	
**EXAMPLE:**
::

        root@5b5a8d783113:/# curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"IP":"192.168.0.1", "MAC":"01:23:34:56:78"}' http://localhost:8080/public/v1/config/ArpConfig
        {"ObjectId":"a97b920d-8b10-47b1-7ea9-890b07f6e712","Error":""}


        root@5b5a8d783113:/# curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:8080/public/v1/config/ArpConfigs | python -m json.tool
          % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                         Dload  Upload   Total   Spent    Left  Speed
        100   174  100   174    0     0  87087      0 --:--:-- --:--:-- --:--:--  169k
        {
            "CurrentMarker": 0,
            "MoreExist": false,
            "NextMarker": 0,
            "ObjCount": 1,
            "Objects": [
                {
                    "Object": {
                        "IP": "192.168.0.1",
                        "MAC":"01:23:34:56:78"
                    },
                    "ObjectId": "a97b920d-8b10-47b1-7ea9-890b07f6e712"
                }
            ]
        }




Configuring with Python SDK
""""""""""""""""""""""""""""""""""
Setting a static arp entry via FlexSwitch's Python SDK, utilizing method *createArpStatic()*. 


**COMMAND:**
::

	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).createArpStatic(<*IPv4Address*>, <*MAC*>)

**OPTIONS:**

+------------------+------------+------------+---------------------------------------------------+----------+----------+
| Python Method    | Variables  | Type       |  Description                                      | Required |  Default |    
+==================+============+============+===================================================+==========+==========+  
| createArpStatic  | IP         | String     | IPv4 address to have a static entry applied       |    Yes   |   None   |
+                  +------------+------------+---------------------------------------------------+----------+----------+
|                  | MAC        | String     | Layer 2 MAC address associated with IPv4 address. |    Yes   |   None   |   
+------------------+------------+------------+---------------------------------------------------+----------+----------+  

**EXAMPLE:**

Below are examples for utilizing this method via the Python CLI, python script and displaying the results:

1. Python CLI:

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).createArpStatic("50.1.1.10","01:23:34:56:78")
	({u'ObjectId': u'9e81f7d4-f9f0-4c86-556b-6398e47897bc', u'Error': u''}, None)
	
2. Utilizing a Python Script to set Static ARP:

::

	#!/usr/bin/python
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		Timeout=1000
		restIf = FlexSwitch(switch_ip, 8080)
		arp_ip="192.168.0.1"
		mac="01:23:34:56:78"
		restIf.createArpStatic(arp_ip,mac)


3. Display results of this change:

::

	#!/usr/bin/python
	import json
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		print json.dumps(restIf.getAllArpStatics(), indent=4)	

Output:

::

	acasella@snaproute-lab-r710-1:~$ ./getarpstatic.py 
	[
	   {
	       "Object": {
	   	   "IP": "192.168.0.1",
	 	   "MAC":"01:23:34:56:78"
	       },
	       "ObjectId": "a97b920d-8b10-47b1-7ea9-890b07f6e712"
	   }
	]



Configuring via Configuration file
""""""""""""""""""""""""""""""""""

----------------------

Display ARP Entry
^^^^^^^^^^^^^^^^^

Display All ARP Entries
"""""""""""""""""""""""

Display via Rest API 
********************
 
Utilizing the GetBulk API for ARP, "*ArpEntrys*", we can display all ARP entries learned on the device.  

**COMMAND:**
::

        curl -X GET --header 'Content-Type: application/json' 'http://<*your-switchip*>:8080/public/v1/state/ArpEntrys'


OPTIONS

::

	None

**EXAMPLE:**
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


Displaying via Python SDK
*************************

Displaying all ARP entries utilizing FlexSwitch's Python SDK, utilizing method *getAllArpEntryStates()*

**COMMAND:**

::

	>>> FlexSwitch("<*Switch IP*>", <*TCP Port*>).getAllArpEntryStates()


**OPTIONS:**

::

   getAllArpEntryStates(self)
	

**EXAMPLE:**

Below are examples for utilizing this method via the Python CLI, python script and displaying the results:

1. Python CLI 
::

	>>> from flexswitchV2 import FlexSwitch
	>>> flexSwitch("10.1.10.243", 8080).getAllArpEntryStates()
	[{u'Object': {u'ConfigObj': None, u'Intf': u'fpPort47', u'Vlan': u'Internal Vlan', u'IpAddr': u'172.16.0.14', u'ExpiryTimeLeft': u'9m24.869691096s', u'MacAddr': u'a8:9d:21:aa:8e:01'}, u'ObjectId': u''}, {u'Object': {u'ConfigObj': None, u'Intf': u'fpPort49', u'Vlan': u'Internal Vlan', u'IpAddr': u'172.16.0.20', u'ExpiryTimeLeft': u'9m43.991376701s', u'MacAddr': u'00:02:03:04:05:00'}, u'ObjectId': u''}]



2. Utilizing a Python Script pretty print Arp Entries

You can display the results of this change with the following Python Script:

::

	#!/usr/bin/python
	import json
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		print json.dumps(restIf.getAllArpEntryStates(), indent=4)	

Output:

::

	acasella@snaproute-lab-r710-1:~$ python getAllArpEntry.py
	[
		{
			"Object": {
				"ConfigObj": null, 
				"Intf": "fpPort47", 
				"Vlan": "Internal Vlan", 
				"IpAddr": "172.16.0.14", 
				"ExpiryTimeLeft": "16m38.415016779s", 
				"MacAddr": "a8:9d:21:aa:8e:01"
			}, 
			"ObjectId": ""
		}, 
		{
			"Object": {
				"ConfigObj": null, 
				"Intf": "fpPort49", 
				"Vlan": "Internal Vlan", 
				"IpAddr": "172.16.0.20", 
				"ExpiryTimeLeft": "16m29.520461011s", 
				"MacAddr": "00:02:03:04:05:00"
			}, 
			"ObjectId": ""
		}
	]


-----------------------

Display a specific ARP entry
""""""""""""""""""""""""""""

Display via Rest API 
********************

You can return the value of an object based on any of the variables within that object.  For example you can query an ARP entry via an IPv4 Address. 

The example below will show how to grab a specific ARP entry by IP address. 

**COMMAND:**

::

	curl -X GET --header 'Content-Type: application/json' -d '{"IpAddr":"<*IPv4 Address*>"}' 'http://<*your-switchip*>:8080/public/v1/state/ArpEntry'


**OPTIONS:**

+------------+------------+---------------------------------------+----------+----------+
| Variables  | Type       |  Description                          | Required |  Default |     
+============+============+=======================================+==========+==========+   
| IpAddr     | String     | IPv4 Address ArpEntry to be queried   |    Yes   |   None   |
+------------+------------+---------------------------------------+----------+----------+

**EXAMPLE:**
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



Displaying via Python SDK
*************************

Displaying all ARP entries utilizing FlexSwitch's Python SDK, utilizing method *getArpEntryStates()*

**COMMAND:**

::

	>>> FlexSwitch("<*Switch IP*>", <*TCP Port*>).getArpEntryState("<*IPv4Address*>")

**OPTIONS:**


+------------------+------------+-------+--------------------------------------+----------+----------+
| Python Method    | Variables  | Type  | Description                          | Required |  Default |  
+==================+============+=======+======================================+==========+==========+
| getArpEntryState | IPv4Address| String|  IPv4 Address ArpEntry to be queried |    Yes   |   None   |
+------------------+------------+-------+--------------------------------------+----------+----------+

	
**EXAMPLE:**

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).getArpEntryState("172.16.0.20")
	({u'Object': {u'ConfigObj': None, u'Intf': u'fpPort49', u'Vlan': u'Internal Vlan', u'IpAddr': u'172.16.0.20', u'ExpiryTimeLeft': u'16m38.505153914s', u'MacAddr': u'00:02:03:04:05:00'}, u'ObjectId': u''}, None)


.. Hint:: You can pretty print the results with the following python script:

::

	#!/usr/bin/python
	import json
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		print json.dumps(restIf.getArpEntryState("172.16.0.20"), indent=4)

Output:

::

	acasella@snaproute-lab-r710-1:~$  python ~/getArpState.py
	[
		{
			"Object": {
				"ConfigObj": null, 
				"Intf": "fpPort49", 
				"Vlan": "Internal Vlan", 
				"IpAddr": "172.16.0.20", 
				"ExpiryTimeLeft": "16m19.337528389s", 
				"MacAddr": "00:02:03:04:05:00"
			}, 
			"ObjectId": ""
		}, 
		null
	]



-------------------------

Python SDK ARP Methods
^^^^^^^^^^^^^^^^^^^^^^
State Methods
"""""""""""""

::

    @processReturnCode
    def getArpEntryState(self,
                         IpAddr):
        obj =  { 
                'IpAddr' : IpAddr,
                }
        reqUrl =  self.stateUrlBase+'ArpEntry'
        r = requests.get(reqUrl, data=json.dumps(obj), headers=headers) 
        return r

    @processReturnCode
    def getArpEntryStateById(self, objectId ):
        reqUrl =  self.stateUrlBase+'ArpEntry'+"/%s"%(objectId)
        r = requests.get(reqUrl, data=None, headers=headers) 
        return r

    def getAllArpEntryStates(self):
        return self.getObjects( 'ArpEntry', self.stateUrlBase)

Config Methods
""""""""""""""

::

    """
    .. automethod :: createArpConfig(self,
        :param string ArpConfigKey :  Arp config  Arp config
        :param integer Timeout :  Global Arp entry timeout value. Default value  Global Arp entry timeout value. Default value

	"""
    @processReturnCode
    def createArpConfig(self,
                        ArpConfigKey,
                        Timeout):
        obj =  { 
                'ArpConfigKey' : ArpConfigKey,
                'Timeout' : int(Timeout),
                }
        reqUrl =  self.cfgUrlBase+'ArpConfig'
        r = requests.post(reqUrl, data=json.dumps(obj), headers=headers) 
        return r

    @processReturnCode
    def updateArpConfig(self,
                        ArpConfigKey,
                        Timeout = None):
        obj =  {}
        if ArpConfigKey != None :
            obj['ArpConfigKey'] = ArpConfigKey

        if Timeout != None :
            obj['Timeout'] = int(Timeout)

        reqUrl =  self.cfgUrlBase+'ArpConfig'
        r = requests.patch(reqUrl, data=json.dumps(obj), headers=headers) 
        return r

    @processReturnCode
    def updateArpConfigById(self,
                             objectId,
                             Timeout = None):
        obj =  {'objectId': objectId }
        if Timeout !=  None:
            obj['Timeout'] = Timeout

        reqUrl =  self.cfgUrlBase+'ArpConfig'
        r = requests.patch(reqUrl, data=json.dumps(obj), headers=headers) 
        return r

    @processReturnCode
    def deleteArpConfig(self,
                        ArpConfigKey):
        obj =  { 
                'ArpConfigKey' : ArpConfigKey,
                }
        reqUrl =  self.cfgUrlBase+'ArpConfig'
        r = requests.delete(reqUrl, data=json.dumps(obj), headers=headers) 
        return r

    @processReturnCode
    def deleteArpConfigById(self, objectId ):
        reqUrl =  self.cfgUrlBase+'ArpConfig'+"/%s"%(objectId)
        r = requests.delete(reqUrl, data=None, headers=headers) 
        return r

    @processReturnCode
    def getArpConfig(self,
                     ArpConfigKey):
        obj =  { 
                'ArpConfigKey' : ArpConfigKey,
                }
        reqUrl =  self.stateUrlBase+'ArpConfig'
        r = requests.get(reqUrl, data=json.dumps(obj), headers=headers) 
        return r

    @processReturnCode
    def getArpConfigById(self, objectId ):
        reqUrl =  self.stateUrlBase+'ArpConfig'+"/%s"%(objectId)
        r = requests.get(reqUrl, data=None, headers=headers) 
        return r

    def getAllArpConfigs(self):
        return self.getObjects( 'ArpConfig', self.cfgUrlBase)

---------------------

---------------------

Configuring BFD
---------------
BFD provides an independent method to validate the operation of the forwarding plane between two routers.  
This can be utilized to ensure subsecond detection of a failure and be utilized to trigger an action in a routing protocol (severing a session or adjacency).

BFD Support
^^^^^^^^^^^

BFD supports the following options:

 - Asynchronous mode
 - Demand mode
 - Authentication  
 - BGP peer failure detection 

-------------

BFD Operation
^^^^^^^^^^^^^^

Flexswitch's BFD implementation was designed to allow for single or multi-hop session establishment. This is done by either having an IP based BFD session, where there could be one of many layer 3 hops between the two devices
or interface based sessions, where the BFD peer, much be directly attached.  This allows for BFD sessions to be tied an interface based protocol, such as OSPF vs a peer-based protocol, such as BGP. 

------------------

Session Establishment 
"""""""""""""""""""""

BFD session establishments begins by implementing a slow timer, by setting the *Desired min Tx Interval* to 2000 ms with a multiplier of 3, resulting in a 6000ms timeout for hello packets that are sent.  
This is done to ensure proper interoperability between 3rd-party peers by ensuring the appropriate BFD parameters are correctly negotiated; I.E. RemoteDiscriminator, SessionState and failure detection timers. 
Once this information is negotiated, we begin to send BFD hello packets at the configured rate. 

If a BFD session does not see hello packets within the configured *Required min Rx Interval*, three things occur:

	1. BFD session state is set to down 
	2. Any associated protocol sessions are torn down
	3. BFD will flush the learned Remote Discriminator  
	
If BFD is associated to a particular protocol, BFD will hold down that protocols session state, until the associated routing-protocol or user-created session is reset by an administrator.   If BFD is brought administratively-down (either locally or remotely), the BFD session is cleared without any impact 
to the associated protocol and only the BFD session is self is torn down. 

For details surrounding specific routing protocol implementations, check out the "BGP with BFD" or "OSPF with BFD" sections. 

Demand Mode
""""""""""""

In demand mode, no Hello packets are exchanged after the session is established; it is assumed that the endpoints have another way to verify connectivity to each other, perhaps on the underlying physical layer.

..
	Per-link
	""""""""

	Since traditional Asynchronous BFD is an IP point-to-point protocol, it has no concept of layer 2 links that may exist between two devices.  This is especially true for layer 2 port-channels with multiple member-links.   
	If these one of these links happen to fail, while BFD is running across them, it may result in a false-positive detection of a connectivity failure.  This could have unintended impact, by bringing down an associated routing-protocol session incorrectly, 
	thus taking our an entire port-channel, rather than a single-link.  

	BFD over LAG or BFD per-link was created as an enhancement to limit the impact of single port-channel member-link failure.  When BFD per-link is enabled on a port-channel interface, an asynchronous mode BFD sessions is run on every port-channel member link.  This allows for failure detection of a single port-channel member-link, 
	limiting the impact and traffic-transitions to only links that failed.  When all BFD sessions fail on a particular port-channel interface, only then are the associated protocol sessions torn down, allowing for accurate fault detection. 


Protocol Specific Failure Detection
""""""""""""""""""""""""""""""""""""

For more details on how BFD integrates with other protocols, please see that protocols specific section:

    - BGP with BFD 
    - OSPF with BFD 
    
-------------------

Enabling BFD
^^^^^^^^^^^^

BFD is enabled in the following order:

 1. Enable globally (Default when daemon is started)
 2. Creation of BFD session parameter profile
 3. Attach to User created BFD session or a routing protocol 
 4. Review configuration and state 

.. Note::The above assumes that the BFD daemon is already running and has registered with the system. 

-----------------

Configuring with Rest API 
"""""""""""""""""""""""""

Enable BFD Globally
*******************

**COMMAND:**
::

	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"Bfd":"default","Enable":true}' 'http://<*your-switchip*>:8080/public/v1/config/BfdGlobal'
	

**OPTIONS:**

+------------+------------+--------------------------------------------------------+----------+----------+
| Variables  | Type       |  Description                                           | Required |  Default |     
+============+============+========================================================+==========+==========+   
| Bfd        | string     | VRF where BFD will be enabled.                         |    Yes   |   None   |
+------------+------------+--------------------------------------------------------+----------+----------+
| Enable     | boolean    | IPv4 Address ArpEntry to be queried; I.E. true/false.  |    Yes   |   None   |
+------------+------------+--------------------------------------------------------+----------+----------+


**EXAMPLE:**

You need to set the "*Enable*" parameter to "*true*".  You can also see the "*Bfd*" parameter is set to the name "*default*".  This value is the 
VRF name where BFD will be Globally enabled. By default this is the "*default*" VRF and should not need to be set by the user. 

.. Note::BFD is enabled by default when the Daemon is started. 

::
	
	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"Bfd":"default","Enable":true}' 'http://10.1.10.43:8080/public/v1/config/BfdGlobal'
	{"ObjectId":"0880b0cb-d0da-461e-7826-9b2eef1b800e","Error":""}

.. _bfd-session-parameters-rest:

Creating BFD session parameters 
*******************************

**COMMAND:**
::

	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"Name":"<*Param Profile Name*>","LocalMultiplier":3,"DesiredMinTxInterval":250,"RequiredMinRxInterval":250,"RequiredMinEchoRxInterval":0,"DemandEnabled":false,"AuthenticationEnabled":false,"AuthKeyId":1,"AuthData":"snaproute"}' 'http://<*your-switchip*>:8080/public/v1/config/BfdSessionParam'
	

**OPTIONS:**


+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| Variables                 | Type       |  Description                                                                     | Required |  Default  |     
+===========================+============+==================================================================================+==========+===========+   
| Name                      | string     | Name of the BFD session                                                          |    Yes   |   None    |
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| LocalMultiplier           | integer    | Multiplier of BFD hello RX interval to wait before tearing down session          |    no    |   3       |
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| DesiredMinTxInterval      | integer    | Time in milliseconds between interval TX of BFD hello packets                    |    no    |   1000    |
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| RequiredMinRxInterval     | integer    | Expected interval in milliseconds between RX of BFD  packets                     |    no    |   1000    |
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| RequiredMinRxEchoInterval | integer    | Expected interval in milliseconds between RX of BFD echo packets                 |    no    |   0       |
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| DemandEnabled             | boolean    | Boolean value to specify the global state for BFD demand mode; I.E. true/false   |    no    |   false   |
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| AuthenticationEnabled     | boolean    | Boolean value to specify the global state for BFD authentication; I.E. true/false|    no    |   false   |
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| AuthType                  | string     | Authentication type; I.E. keyed MD5, simple, keyed Sha1                          |    no    |   None    |
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| AuthKeyId                 | integer    | Authentication key ID                                                            |    no    |   1       |
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| AuthData                  | string     | Authentication string                                                            |    no    |"snaproute"|
+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+



**EXAMPLE:**

Here we are creating the BFD session parameters that will be utilized by the BFD session between devices. 

::

	acasella@snaproute-lab-r710-1:~$ curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"Name":"BFD_session","LocalMultiplier":3,"DesiredMinTxInterval":250,"RequiredMinRxInterval":250,"RequiredMinEchoRxInterval":0,"DemandEnabled":false,"AuthenticationEnabled":false,"AuthKeyId":1,"AuthData":"snaproute"}' 'http://10.1.10.43:8080/public/v1/config/BfdSessionParam'
	{"ObjectId":"40ebf60d-1230-4c7b-4c91-bc4a076693d4","Error":""}
	
	
Attaching BFD params to a BFD session  
*************************************

	Attaching BFD parameter profile to user create BFD session:

			**COMMAND:**
			::
				
				curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"IpAddr":"<*IPv4 Address*>","ParamName":"<*Param Profile Name*>","Interface":"None","Owner":"user"}' 'http://<*your-switchip*>:8080/public/v1/config/BfdSession'

				
			**OPTIONS:**
				+-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				| Variables | Type       |  Description                                                                          | Required |  Default  |     
				+===========+============+=======================================================================================+==========+===========+   
				| IpAddr    | string     | BFD neighbor IP address                                                               |    Yes   |   None    |
				+-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				| ParaName  | string     | Name of the session parameters object to be applied on this session                   |    no    | "default" |
				+-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				| Interface | boolean    | Name of the interface this session has to be established on                           |    no    |   None    |
				+-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				| PerLink   | string     | Run BFD sessions on individual link of a LAG if the neighbor is reachable through LAG |    no    |   false   |
				+-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				| Owner     | string     | Module requesting BFD session configuration                                           |    no    |   user    |
				+-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
						
			
			
			**EXAMPLE:**
			
			As you can see below "ParamName" variable specifies the BFD parameter profile with a BFD session.  
			
			::
				
				curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"IpAddr":"1.1.1.1","ParamName":"BFD_session","Interface":"None","Owner":"user"}' 'http://10.1.10.43:8080/public/v1/config/BfdSession'



	Attaching BFD parameter profile to protocol created BFD session:

		For more details on how BFD integrates with other protocols, please goto that protocols specific section:

		    - BGP with BFD 
   		    - OSPF with BFD 
    
							

Configuring BFD demand mode
***************************

Configuring BFD Authentication
******************************


Displaying Configuration and State
**********************************


Display BFD session parameter profile configuration:

**COMMAND:**
::
	
	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.43:8080/public/v1/config/BfdSessionParams'

**OPTIONS:**
::
	
	None
	
**EXAMPLE:**
	
We can start by looking at the BFD configuration of was setup in the example sections above.  We can view the session parameters:

::

	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.43:8080/public/v1/config/BfdSessionParams' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100   386  100   386    0     0  51411      0 --:--:-- --:--:-- --:--:-- 55142
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 0,
		"ObjCount": 1,
		"Objects": [
			{
				"Object": {
					"AuthData": "snaproute",
					"AuthKeyId": 1,
					"AuthType": "",
					"AuthenticationEnabled": false,
					"ConfigObj": null,
					"DemandEnabled": false,
					"DesiredMinTxInterval": 250,
					"LocalMultiplier": 3,
					"Name": "BFD_session",
					"RequiredMinEchoRxInterval": 0,
					"RequiredMinRxInterval": 250
				},
				"ObjectId": "4c46080c-f4c1-477b-6ce3-873aee89ab9c"
			}
		]
	}


Display BFD Session configuration:


**COMMAND:**
::
	
	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.43:8080/public/v1/config/BfdSessions'

**OPTIONS:**
::
	
	None
	
**EXAMPLE:**

Below we can see the BFD Session Parameter profile "BFD_Session": parameter profile as well:

::

	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.43:8080/public/v1/config/BfdSessions' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100   431  100   431    0     0  64987      0 --:--:-- --:--:-- --:--:-- 71833
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 0,
		"ObjCount": 1,
		"Objects": [
			{
				"Object": {
					"ConfigObj": null,
					"Interface": "None",
					"IpAddr": "1.1.1.1",
					"Owner": "user",
					"ParamName": "BFD_session",
					"PerLink": false
				},
				"ObjectId": "b825914b-5b6c-4c5f-6a65-a80fc958d38d"
			},



Display BFD Session Parameter State:


**COMMAND:**

::

	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.245:8080/public/v1/state/BfdSessionParams'

**OPTIONS:**
::
	
	None
	
**EXAMPLE:**

When we look at the BfdSessionParams status, we see very similar data to that of the configuration, but there are a few very important differences:

1. This indicated that BFDd has ingested the configuration and is ready to begin utilizing it.
2. State related items to show us how this configuration is being utilized. 

   
If we look at the "NumSessions" variable, we can see this BFD session parameter profile is being utilized by 1 BFD session. We can also see that the 
millisecond variables we utilized in the configuration have been changed to microseconds.  This is done for RFC compliance and interoperability with 3rd-party
BFD implementations. 


::

	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.43:8080/public/v1/state/BfdSessionParams' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100   789  100   789    0     0  55657      0 --:--:-- --:--:-- --:--:-- 60692
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 0,
		"ObjCount": 1,
		"Objects": [
			{
				"Object": {
					"AuthenticationData": "snaproute",
					"AuthenticationEnabled": false,
					"AuthenticationKeyId": 1,
					"AuthenticationType": "",
					"ConfigObj": null,
					"DemandEnabled": false,
					"DesiredMinTxInterval": "250000(us)",
					"LocalMultiplier": 3,
					"Name": "BFD_session",
					"NumSessions": 0,
					"RequiredMinEchoRxInterval": "0(us)",
					"RequiredMinRxInterval": "250000(us)"
				},
				"ObjectId": "4c46080c-f4c1-477b-6ce3-873aee89ab9c"
			}
		]
	}

Display BFD Session State:


**COMMAND:**

::

	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.245:8080/public/v1/state/BfdSessions'

**OPTIONS:**
::
	
	None
	
**EXAMPLE:**

The BfdSessions state API responds with the relevant state of all BFD sessions.  We can see the current BFD timers being utilized, the BFD Parameter Profile this information was
inherited via the *ParamName* variable, BFD_Sessions in this case. As well aa BFD session status via *SessionState* variable, which is up and working. 

::

	curl -H "Content-Type: application/json" 'http://10.1.10.245:8080/public/v1/state/BfdSessions' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100  1391  100  1391    0     0  95371      0 --:--:-- --:--:-- --:--:-- 99357
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 0,
		"ObjCount": 2,
		"Objects": [
			{
				"Object": {
					"AuthSeqKnown": false,
					"AuthType": "",
					"ConfigObj": null,
					"DemandMode": false,
					"DesiredMinTxInterval": "250000(us)",
					"DetectionMultiplier": 3,
					"IfIndex": 30,
					"IfName": "",
					"InterfaceSpecific": false,
					"IpAddr": "1.1.1.1",
					"LocalDiagType": "None",
					"LocalDiscriminator": 979,
					"LocalMacAddr": "",
					"NumRxPackets": 217275,
					"NumTxPackets": 199389,
					"ParamName": "BFD_Sessions",
					"PerLinkSession": false,
					"ReceivedAuthSeq": 0,
					"RegisteredProtocols": "user, ",
					"RemoteDemandMode": false,
					"RemoteDiscriminator": 533,
					"RemoteMacAddr": "",
					"RemoteMinRxInterval": "250000(us)",
					"RemoteSessionState": "up",
					"RequiredMinRxInterval": "250000(us)",
					"SentAuthSeq": 0,
					"SessionId": 979,
					"SessionState": "up"
				},
				"ObjectId": ""
			},

-------------------

Configuring with Python SDK
"""""""""""""""""""""""""""

Enable BFD Globally
*******************

**COMMAND:**

::

	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).createBfdGlobal(Bfd=<*VRF Name*> , Enable=<*true/false*>)

**OPTIONS:**

+------------------+-------------+------------+------------------------------------+----------+-----------+
| Python Method    | Variables   | Type       |  Description                       | Required |  Default  |     
+==================+=============+============+====================================+==========+===========+   
| createBfdGlobal  | Bfd         | string     | VRF Name where BFD is enabled      |    Yes   | "default" |
|                  +-------------+------------+------------------------------------+----------+-----------+
|                  | Enable      | boolean    | Enable BFD within specified VRF    |    Yes   |   true    |
+------------------+-------------+------------+------------------------------------+----------+-----------+

       					 
**EXAMPLE:**

You need to set the "*Enable*" parameter to "*true*".  You can also see the "*Bfd*" parameter is set to the name "*default*".  This value is the 
VRF name where BFD will be Globally enabled. By default this is the "*default*" VRF and should not need to be set by the user. 

.. Note::BFD is enabled by default when the Daemon is started. 

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).createBfdGlobal("default", True)
	({u'ObjectId': u'5b4a4b49-7310-444e-64da-5d8e8764e914', u'Error': u''}, None)


Can be applied with the following Python Script:


::

	#!/usr/bin/python
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		restIf.createBfdGlobal("default", True)	


.. _bfd-session-parameters-python:

Creating BFD session parameters 
*******************************


**COMMAND:**
::

	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).createBfdSessionParam(<*Name*>, <*LocalMultiplier*>, <*DesiredMinTxInterval*>, <*RequiredMinRxInterval*>,<*RequiredMinRxEchoInterval*>,<*DemandEnabled*>,<*AuthenticationEnabled*>, <*AuthKeyId*>,<*AuthData*> )

**OPTIONS:**

+------------------------+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
| Python Method          | Variables                 | Type       |  Description                                                                     | Required |  Default  |     
+========================+===========================+============+==================================================================================+==========+===========+   
| createBfdSessionParam  | Name                      | string     | Name of the BFD session                                                          |    Yes   |   None    |
|                        +---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
|                        | LocalMultiplier           | integer    | Multiplier of BFD hello RX interval to wait before tearing down session          |    no    |   3       |
|                        +---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
|                        | DesiredMinTxInterval      | integer    | Time in milliseconds between interval TX of BFD hello packets                    |    no    |   1000    |
|                        +---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
|                        | RequiredMinRxInterval     | integer    | Expected interval in milliseconds between RX of BFD  packets                     |    no    |   1000    |
|                        +---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
|                        | RequiredMinRxEchoInterval | integer    | Expected interval in milliseconds between RX of BFD echo packets                 |    no    |   0       |
|                        +---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
|                        | DemandEnabled             | boolean    | Boolean value to specify the global state for BFD demand mode; I.E. true/false   |    no    |   false   |
|                        +---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
|                        | AuthenticationEnabled     | boolean    | Boolean value to specify the global state for BFD authentication; I.E. true/false|    no    |   false   |
|                        +---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
|                        | AuthKeyId                 | integer    | Authentication key ID                                                            |    no    |   1       |
|                        +---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+
|                        | AuthData                  | string     | Authentication string                                                            |    no    |"snaproute"|
+------------------------+---------------------------+------------+----------------------------------------------------------------------------------+----------+-----------+



**EXAMPLE:**

Here we are creating the BFD session parameters that will be utilized by the BFD session between devices. 

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).createBfdSessionParam("BFD_Session", LocalMultiplier=3, RequiredMinRxInterval=250, DesiredMinTxInterval=250)
	({u'ObjectId': u'5b4a4b49-7310-444e-64da-5d8e8764e914', u'Error': u''}, None)


Can be applied with the following Python Script:


::

	#!/usr/bin/python
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		restIf.createBfdSessionParam("BFD_Session", LocalMultiplier=3, RequiredMinRxInterval=250, DesiredMinTxInterval=250)


Attaching BFD params to a BFD session  
*************************************


	Attaching BFD parameter profile to user create BFD session:

		
			**COMMAND:**
			::
				>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).createBfdSession(ParaName=<*Name*>, IpAddr=<*IPv4 Address*>, Interface=<*L3 interface*>, PerLink=<*perlink*>,Owner=<*BFD owner*>)
			
			**OPTIONS**
				+-------------------+-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				| Python Method     | Variables | Type       |  Description                                                                          | Required |  Default  |      
				+===================+===========+============+=======================================================================================+==========+===========+    
				| createBfdSession  | IpAddr    | string     | BFD neighbor IP address                                                               |    Yes   |   None    |
				|                   +-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				|                   | ParaName  | string     | Name of the session parameters object to be applied on this session                   |    no    | "default" |
				|                   +-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				|                   | Interface | boolean    | Name of the interface this session has to be established on                           |    no    |   None    |
				|                   +-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				|                   | PerLink   | string     | Run BFD sessions on individual link of a LAG if the neighbor is reachable through LAG |    no    |   false   |
				|                   +-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
				|                   | Owner     | string     | Module requesting BFD session configuration                                           |    no    |   user    |
				+-------------------+-----------+------------+---------------------------------------------------------------------------------------+----------+-----------+
	    
										
			**EXAMPLE**
			As you can see below "ParamName" variable specifies the BFD parameter profile with a BFD session.  

			::

				>>> from flexswitchV2 import FlexSwitch
				>>> FlexSwitch("10.1.10.243", 8080).createBfdSession(ParaName="BFD_Sessions", IpAddr="1.1.1.1")
				({u'ObjectId': u'5b4a4b49-7310-444e-64da-5d8e8764e914', u'Error': u''}, None)


			Can be applied with the following Python Script:


			::

				#!/usr/bin/python
				from flexswitchV2 import FlexSwitch


				if __name__ =='__main__':
					switch_ip = "10.1.10.243"
					restIf = FlexSwitch(switch_ip, 8080)
					restIf.createBfdSession(ParaName="BFD_Sessions", IpAddr="1.1.1.1")

	Attaching BFD parameter profile to protocol created BFD session:

		For more details on how BFD integrates with other protocols, please goto that protocols specific section:

		    - BGP with BFD 
   		    - OSPF with BFD 

Configuring BFD demand mode
***************************

Configuring BFD Authentication
******************************


Displaying Configuration and State
**********************************

Display BFD session parameter profile configuration:

**COMMAND:**
::

	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).getAllBfdSessionParams(self)


**OPTIONS:**
::
	
	None
	
**EXAMPLE:**
	
We can start by looking at the BFD configuration of was setup in the example sections above.  We can view the session parameters via python CLI:

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).getAllBfdSessionParams()
	[{u'Object': {u'ConfigObj': None, u'RequiredMinRxInterval': 250, u'AuthType': u'simple', u'Name': u'Session1', u'AuthKeyId': 1, u'AuthData': u'snaproute', u'DesiredMinTxInterval': 250, u'AuthenticationEnabled': False, u'DemandEnabled': False, u'RequiredMinEchoRxInterval': 0, u'LocalMultiplier': 3}, u'ObjectId': u'376eebef-4061-45e8-77c4-058b4b501deb'}]	

Can be viewed with the following Python Script:


::

	#!/usr/bin/python
	import json
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		json.dumps(restIf.getAllBfdSessionParams(), indent=4)

	acasella@snaproute-lab-r710-1:~$ python get_bfd.py 
	
	[
		{
			"Object": {
				"ConfigObj": null, 
				"RequiredMinRxInterval": 250, 
				"AuthType": "simple", 
				"Name": "Session1", 
				"AuthKeyId": 1, 
				"AuthData": "snaproute", 
				"DesiredMinTxInterval": 250, 
				"AuthenticationEnabled": false, 
				"DemandEnabled": false, 
				"RequiredMinEchoRxInterval": 0, 
				"LocalMultiplier": 3
			}, 
			"ObjectId": "376eebef-4061-45e8-77c4-058b4b501deb"
		}
	]


Display BFD Session configuration:


**COMMAND:**
::

	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).getAllBfdSessions(self)


**OPTIONS:**
::
	
	None
	
**EXAMPLE:**
	
Below we can see the BFD Session Parameter profile "BFD_Session": parameter profile as well:

::

	>>> FlexSwitch("10.1.10.243", 8080).getAllBfdSessions()
	[{u'Object': {u'ConfigObj': None, u'IpAddr': u'1.1.1.1', u'PerLink': False, u'Owner': u'user', u'ParamName': u'BFD_Sessions', u'Interface': u'None'}, u'ObjectId': u'b37cd681-90ad-487c-4afa-1efae74eda29'}]


Can be viewed with the following Python Script:

::

	#!/usr/bin/python
	import json
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		print json.dumps(restIf.getAllBfdSessions(), indent=4)
	
	acasella@snaproute-lab-r710-1:~$ python get_bfd.py 
	[
		{
			"Object": {
				"ConfigObj": null, 
				"IpAddr": "1.1.1.1", 
				"PerLink": false, 
				"Owner": "user", 
				"ParamName": "BFD_Sessions", 
				"Interface": "None"
			}, 
			"ObjectId": "b37cd681-90ad-487c-4afa-1efae74eda29"
		}
	]
 
Display BFD Session Parameter State:


**COMMAND:**

::

	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).getAllBfdSessionParamStates(self)
	
	
**OPTIONS:**
::
	
	None
	
**EXAMPLE:**

When we look at the BfdSessionParams status, we see very similar data to that of the configuration, but there are a few very important differences:

1. This indicated that BFDd has ingested the configuration and is ready to begin utilizing it.
2. State related items to show us how this configuration is being utilized. 

   
If we look at the "NumSessions" variable, we can see this BFD session parameter profile is being utilized by 1 BFD session. We can also see that the 
millisecond variables we utilized in the configuration have been changed to microseconds.  This is done for RFC compliance and interoperability with 3rd-party
BFD implementations. 



::

	>>> FlexSwitch("10.1.10.243", 8080).getAllBfdSessionParamStates()
	[{u'Object': {u'ConfigObj': None, u'RequiredMinRxInterval': u'250000(us)', u'Name': u'BFD_Sessions', u'AuthenticationType': u'simple', u'AuthenticationData': u'snaproute', u'DesiredMinTxInterval': u'250000(us)', u'AuthenticationEnabled': False, u'DemandEnabled': False, u'NumSessions': 0, u'AuthenticationKeyId': 1, u'RequiredMinEchoRxInterval': u'0(us)', u'LocalMultiplier': 3}, u'ObjectId': u'376eebef-4061-45e8-77c4-058b4b501deb'}]


Can be viewed via the following python script

::

	#!/usr/bin/python
	import json
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		print json.dumps(restIf.getAllBfdSessionParamStates(), indent=4)
	
	acasella@snaproute-lab-r710-1:~$ python get_bfd.py 
	[
		{
			"Object": {
				"ConfigObj": null, 
				"RequiredMinRxInterval": "250000(us)", 
				"Name": "BFD_Sessions", 
				"AuthenticationType": "simple", 
				"AuthenticationData": "snaproute", 
				"DesiredMinTxInterval": "250000(us)", 
				"AuthenticationEnabled": false, 
				"DemandEnabled": false, 
				"NumSessions": 0, 
				"AuthenticationKeyId": 1, 
				"RequiredMinEchoRxInterval": "0(us)", 
				"LocalMultiplier": 3
			}, 
			"ObjectId": "376eebef-4061-45e8-77c4-058b4b501deb"
		}
	]


Display BFD Session State:


**COMMAND:**

::

	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).getAllBfdSessionStates()
	
**OPTIONS:**
::
	
	None
	
**EXAMPLE:**

The BfdSessions state API responds with the relevant state of all BFD sessions.  We can see the current BFD timers being utilized, the BFD Parameter Profile this information was
inherited via the *ParamName* variable, BFD_Sessions in this case. As well aa BFD session status via *SessionState* variable, which is up and working. 

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("10.1.10.243", 8080).getAllBfdSessionStates()
	[{u'Object': {u'RegisteredProtocols': u'user, ', u'DesiredMinTxInterval': u'250000(us)', u'SessionId': 640, u'ParamName': u'BFD_Sessons', u'DemandMode': False, u'DetectionMultiplier': 3, u'SentAuthSeq': 0, u'LocalDiscriminator': 640, u'SessionState': u'up', u'AuthSeqKnown': False, u'PerLinkSession': False, u'IfName': u'', u'ConfigObj': None, u'RequiredMinRxInterval': u'250000(us)', u'AuthType': u'', u'RemoteDiscriminator': 564, u'RemoteSessionState': u'up', u'NumTxPackets': 850068, u'InterfaceSpecific': False, u'NumRxPackets': 826751, u'RemoteDemandMode': False, u'LocalMacAddr': u'', u'RemoteMinRxInterval': u'250000(us)', u'IpAddr': u'1.1.1.1', u'RemoteMacAddr': u'', u'LocalDiagType': u'None', u'IfIndex': 49, u'ReceivedAuthSeq': 0}, u'ObjectId': u''}]
	

Can be viewed via the following python script. 

::

	import json
	from flexswitchV2 import FlexSwitch


	if __name__ =='__main__':
		switch_ip = "10.1.10.243"
		restIf = FlexSwitch(switch_ip, 8080)
		print json.dumps(restIf.getAllBfdSessionStates(), indent=4)

	acasella@snaproute-lab-r710-1:~$ python get_bfd.py 
	[
		{
			"Object": {
				"RegisteredProtocols": "user, ", 
				"DesiredMinTxInterval": "250000(us)", 
				"SessionId": 701, 
				"ParamName": "BFD_Sessions", 
				"DemandMode": false, 
				"DetectionMultiplier": 3, 
				"SentAuthSeq": 0, 
				"LocalDiscriminator": 701, 
				"SessionState": "up", 
				"AuthSeqKnown": false, 
				"PerLinkSession": false, 
				"IfName": "", 
				"ConfigObj": null, 
				"RequiredMinRxInterval": "250000(us)", 
				"AuthType": "", 
				"RemoteDiscriminator": 1090519237, 
				"RemoteSessionState": "up", 
				"NumTxPackets": 747461, 
				"InterfaceSpecific": false, 
				"NumRxPackets": 908113, 
				"RemoteDemandMode": false, 
				"LocalMacAddr": "", 
				"RemoteMinRxInterval": "250000(us)", 
				"IpAddr": "1.1.1.1", 
				"RemoteMacAddr": "", 
				"LocalDiagType": "None", 
				"IfIndex": 47, 
				"ReceivedAuthSeq": 0
			}, 
			"ObjectId": ""
		}
	]
			
------------------


Configuring BGP
---------------

Border Gateway Protocol (BGP) is a standardized exterior gateway protocol designed to exchange routing and reachability information among autonomous systems (AS) on a network. The protocol is often classified as a path vector protocol but is sometimes also classed as a distance-vector routing protocol.
BGP version 4 is defined by RFC 4271.

Multiprotocol BGPv4+ can exchange routing information based on multiple address families (AFI) and sub-address families (SAFI) simultaneously over a single BGP established session.  Multiprotocol BGP is defined by RFC 4760.

-------------

BGP Operation
^^^^^^^^^^^^^
BGP is an exterior gateway protocol, that exchanges prefixes through the same or different autonomous systems over established TCP sessions. 

This communication is performed over TCP port 179, and is done via static neighbor relationships configured via an administrator.  BGP is split into two operational schema's, IBGP and EBGP.  IGBP peers
function within a single AS, where EBGP peers function to exchange routing information between different AS's.  The goal of IBGP is used to exchange routing information throughout the AS, where EBGP peers are
utilized to exchange routing information internal to an AS to another/external AS and vice-versa.

Session Establishment
"""""""""""""""""""""

BGP utilizes its own finite state machine for establishing connections to exchange routes with another peer. This is done for both TCP session collision handling (ensuring the right TCP session is being utilized, between
two peers), as well as exchanging BGP information over the TCP session utilized.  The following FSM states exists:

 1. **Idle** - In this state BGP refuses all incoming BGP connections, initiates a TCP connection with its configured BGP peer and Changes its state to **Connect**.  

 		 - If an error occurs during FSM process, BGP session is terminated and returns to **Idle** state. 
 
 2. **Connect** - Waits for successful TCP negotiation with peer, then sends an OPEN message to the peer.
 	
 			- If successful, the router will transition to the **OpenSent** state.  
 			- If unsuccessful, the router will set the *ConnectionRetry* timer and transition to the **Active** state upon expiry. 

 3. **Active** - If TCP session establishment was unsuccessful BGP will be placed in this state.  The router will set *ConnectionRetry* timer to zero, attempt a TCP session establishment then sends an OPEN message to the peer.
 	
 		   - If successful, transition to the **OpenSent** state.  If unsuccessful, transitions to the **Idle** state.  
 		   - Repeated TCP session failures may result in session bouncing between **Active** and **Idle** states. 

 4. **OpenSent** - Listens for Open Message from peer.  Once valid message has been received a Keepalive message is sent, various timers are set and the state transitions to **OpenConfirm**. 
 	
 			 - If there is an error, router then sends a NOTIFICATION message to the peer indicating why the error occurred.

 5. **OpenConfirm** - The Router waits for a keepalive messages from its peer.  If message is received before timer expiry, the router transitions to the **Established** State.  
 	
 				- If keep-alive timer expires or an error occurs,  router transitions to **Idle** state. 

 6. **Established** - Peers exchange UPDATE messages about prefixes they advertise.  
 	
 				- If UPDATE message contains an error the router sends a NOTIFICATION message and then transitions to the **Idle** state.  
 				- If Keepalive timer expires or if an error condition occurs, the router transitions back to the **Idle** state.


During the Established state BGP sessions exchange UPDATE messages about prefixes in which they have connectivity. These UPDATES
contain all the necessary information to forward data to these routes.  The UPDATES include destination prefix, prefix length, AS path, the next hop IP, and additional information which may affect if this route is accepted by the receiving router.
  
Enabling Globally
^^^^^^^^^^^^^^^^^^

.. _bgp-global-rest:

Configuring with Rest API 
""""""""""""""""""""""""""""""""

**COMMAND:**
::

	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ASNum":<*AS Number*>,"RouterId":"<*IP Addr*>","UseMultiplePaths":<*true/false*>,"EBGPMaxPaths":<*Number of Paths*>,"UseMultiplePaths":<*true/false*> ,"IBGPMaxPaths":<*Number of Paths*>}' 'http://<*your-switchip*>:8080/public/v1/config/BGPGlobal'
	

**OPTIONS:**

+----------------------+------------+---------------------------------------------+----------+----------+
| Variables            | Type       |  Description                                | Required |  Default |     
+======================+============+=============================================+==========+==========+   
| ASNum                | integer    | Local AS for BGP global config              |    Yes   |   None   |
+----------------------+------------+---------------------------------------------+----------+----------+
| RouterId             | string     | Router id for BGP global config             |    Yes   |   None   |
+----------------------+------------+---------------------------------------------+----------+----------+
| UseMultiplePaths     | boolean    | Enable/disable ECMP for BGP                 |    no    |  false   |
+----------------------+------------+---------------------------------------------+----------+----------+
| EBGPMaxPaths         | integer    | Max ECMP paths from External BGP neighbors  |    no    |     0    |
+----------------------+------------+---------------------------------------------+----------+----------+
| EBGPAllowMultipleAS  | boolean    | Enable/diable ECMP paths from multiple AS's |    no    |  false   |
+----------------------+------------+---------------------------------------------+----------+----------+
| IBGPMaxPaths         | integer    | Max ECMP paths from Internal BGP neighbors  |    no    |     0    |
+----------------------+------------+---------------------------------------------+----------+----------+

**EXAMPLE:**

BGP requires a local AS Number and a Router ID to enable globally.  Once these two items are assigned, BGP will be globally enabled on FlexSwitch. 

.. Note:: AS number and Router Id, MUST be unique per device.  

::

	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ASNum":65535,"RouterId":"1.1.1.1"}' 'http://192.168.0.2:8080/public/v1/config/BGPGlobal'
	{"ObjectId":"c5f253d9-1f0d-461e-62aa-963b1ef3b0bd","Error":""}

.. _bgp-global-python:

Configuring with Python SDK
"""""""""""""""""""""""""""""""""""

**COMMAND:**
::


	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).createBGPGlobal(ASNum=<*AS Number*>,
									RouterId=<*IP Addr*>,
									UseMultiplePaths=<*true/false*>,
									EBGPMaxPaths=<*Number of Paths*>,
									EBGPAllowMultipleAS=<*true/false*>, 
									IBGPMaxPaths=<*Number of Paths*>,)
	

**OPTIONS:**

+----------------------+----------------------+------------+---------------------------------------------+----------+----------+
| Python Method        | Variables            | Type       |  Description                                | Required |  Default |     
+======================+======================+============+=============================================+==========+==========+   
| createBGPGlobal      | ASNum                | integer    | Local AS for BGP global config              |    Yes   |   None   |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | RouterId             | string     | Router id for BGP global config             |    Yes   |   None   |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | UseMultiplePaths     | boolean    | Enable/disable ECMP for BGP                 |    no    |  False   |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | EBGPMaxPaths         | integer    | Max ECMP paths from External BGP neighbors  |    no    |     0    |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | EBGPAllowMultipleAS  | boolean    | Enable/diable ECMP paths from multiple AS's |    no    |  False   |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | IBGPMaxPaths         | integer    | Max ECMP paths from Internal BGP neighbors  |    no    |     0    |
+----------------------+----------------------+------------+---------------------------------------------+----------+----------+

**EXAMPLE:**

BGP requires a local AS Number and a Router ID to enable globally.  Once these two items are assigned, BGP will be globally enabled on FlexSwitch. 

.. Note:: AS number and Router Id, MUST be unique per device.  

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("192.168.0.2", 8080).createBGPGlobal(ASNum=65535 ,RouterId="1.1.1.1")
	({u'ObjectId': u'61e6ad4b-6bc7-4e35-5c9a-89106728c4b4', u'Error': u''}, None)


Neighbor Setup 
^^^^^^^^^^^^^^

BGP requires established peering relationships to exchange routing information.  This section will assist in setting up a BGP peer with another device. 

.. _bgp-neighbor-rest:

Configuring with Rest API 
"""""""""""""""""""""""""

**COMMAND:**

::

	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"PeerAS":<*Peer AS Number*>,"LocalAS":"<*Local AS number*>","AuthPassword":<*Password*>,"Description":<*Peer Description*>,"NeighborAddress":<*IPv4 Address*> ,"IfIndex":<*Interface IfIndex*>,"RouteReflectorClusterId":<*ClusterID*>,"RouteReflectorClient":<*true/false*>,"MultiHopEnable":<*true/false*>,"MultiHopTTL":<*TTL*>, "ConnectRetryTime":<*Retry Timer*>, "HoldTime":<*Hold down Timer*>, "KeepAliveTime":<*Keepalive Timer*>, "AddPathRx":<*true/false*>, "AddPathsMaxTx":<*Max Transmit AddPaths*>,"PeerGroup":<*Peer Group Name*>, "BfdEnable":<*true/false*>, "BfdSessionParam":<*Bfd session param profile*>, "MaxPrefixes"":<*number of prefix's*>, "MaxPrefixesThresholdPct":<*Percentage of Prefix's*>, "MaxPrefixesDisconnect":<*true/false*>, "MaxPrefixesRestartTimer":<*Restart Timer*>	}' 'http://<*your-switchip*>:8080/public/v1/config/BGPNeighbor'
	

**OPTIONS:**

+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| Variables               | Type       |  Description                                                                            | Required |  Default |     
+=========================+============+=========================================================================================+==========+==========+   
| PeerAS                  | integer    | Peer AS of the BGP neighbor                                                             |    Yes   |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| LocalAS                 | integer    | Local AS of the BGP, overrides Global AS value, can be used to spoof AS number          |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| AuthPassword            | string     | Password to connect to the BGP neighbor                                                 |    no    |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| Description             | string     | Description of the BGP neighbor                                                         |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| NeighborAddress         | string     | Address of the BGP neighbor (required if IfIndex is not supplied)                       |    Yes   |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| IfIndex                 | integer    | Interface of BGP neighbor (required if NeighborAddress is not supplied)                 |    Yes   |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| RouteReflectorClusterId | integer    | Cluster ID of the internal BGP neighbor router reflector client                         |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| RouteReflectorClient    | boolean    | Set/Clear BGP neighbor as a route reflector client                                      |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MultiHopEnable          | boolean    | Enable/Disable multihop for BGP neighbor                                                |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MultiHopTTL             | string     | Number of hops(TTL) to multi-hop BGP neighbor                                           |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| ConnectRetryTime        | integer    | Retry timer for BGP session reconnect attempt after disconnect/failure                  |    no    |    60s   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| HoldTime                | integer    | Hold down time for BGP neighbor failure/disconnect                                      |    no    |   180s   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| KeepaliveTime           | integer    | Frequency of BGP Keepalive messages                                                     |    no    |    60s   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| AddPathsRx              | boolean    | Enable/Disable reception of BGP Add-Path NLRI updates                                   |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| AddPathsMaxTx           | integer    | Max number of additional paths that can be transmitted to BGP neighbor                  |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| PeerGroup               | string     | Peer group to inherit common configuration for BGP neighbors                            |    no    |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| BfdEnable               | boolean    | Enable/Disable BFD for BGP neigbor                                                      |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| BfdSessionParam         | string     | BFD session parameter profile name to be utilized by BFD session                        |    no    |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MaxPrefixes             | integer    | Maximum number of prefixes that can be received from the BGP neighbor                   |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MaxPrefixesThresholdPct | string     | The percentage of MaxPrefixes before we start logging                                   |    no    |    80%   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MaxPrefixesDisconnect   | boolean    | Disconnect the BGP peer session when we receive the max prefixes from the neighbor      |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MaxPrefixesRestartTimer | string     | Time in seconds to wait before we start BGP peer session when we receive max prefixes   |    no    |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| UpdateSource            | string     | Interface to source BGP session.  Utilizes Egress interface IP with this is not present |    no    |   None   |                      
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+


**EXAMPLE:**

Here we will configure a BGP session between two devices running FlexSwitch and check the status of these devices. 

Currently we are keeping track of BGP session FSM states based on a numeric value:

+---------------+--------------+
| BGP FSM state | Numeric value|
+---------------+--------------+
| Idle          |      1       |
+---------------+--------------+
| Active        |      2       |
+---------------+--------------+
| Connect       |      3       |
+---------------+--------------+
| OpenSent      |      4       |
+---------------+--------------+
| OpenConfirm   |      5       |
+---------------+--------------+
| Established   |      6       |
+---------------+--------------+


Below we will demonstrate how to create a BGP neighbor relationship between two BGP peers, Device1(10.1.10.241) and Device2(10.1.10.243) in AS 65535.  Display the BGP sessions status on each device and that they are exchanging a connected route from interface Vlan10.  

.. Note:: This is assuming each device has BGP enabled and are in AS 65535 and redistribution of connected routes has been enabled for Vlan10. 


See Topology1 for details:

Topology 1:

.. image:: images/BGP_Diagram1.png


1. On device1 (10.1.10.241), we will create a neighbor 1.1.1.1 from IPv4 1.1.1.0

	::

		curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"PeerAS":65535,"NeighborAddress":"1.1.1.1"}' 'http://10.1.10.241:8080/public/v1/config/BGPNeighbor'
		{"ObjectId":"b72d2e52-8878-490e-5ee8-6873bd40f423","Error":""}

2. On device2 (10.1.10.243), we will create a neighbor to 1.1.1.0 from IPv4 1.1.1.1

	::

		curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"PeerAS":65535,"NeighborAddress":"1.1.1.0"}' 'http://10.1.10.243:8080/public/v1/config/BGPNeighbor'
		{"ObjectId":"5977ffa7-67bd-4847-7597-4175b513883c","Error":""}

.. Note:: You can run RestAPI calls from any location that has IP connectivity to FlexSwitch.  


3. Validation:

Below it can be seen that both  Device1 and Device2 are in the Established state (Session State 6), and are exchanging routing information for the prefix on Vlan10. 


On Device1 (10.1.10.241):

Neighbor 1.1.1.1 in the Established state (Session State 6), and is receiving a single prefix from this peer. 

::
	
	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json'  'http://10.1.10.241:8080/public/v1/state/BGPNeighbors' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100  2999    0  2999    0     0   414k      0 --:--:-- --:--:-- --:--:--  488k
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
					"ConfigObj": null,
					"ConnectRetryTime": 60,
					"Description": "",
					"HoldTime": 180,
					"IfIndex": 0,
					"KeepaliveTime": 60,
					"LocalAS": 65535,
					"MaxPrefixes": 0,
					"MaxPrefixesDisconnect": false,
					"MaxPrefixesRestartTimer": 0,
					"MaxPrefixesThresholdPct": 80,
					"Messages": {
						"Received": {
							"Notification": 1,
							"Update": 4
						},
						"Sent": {
							"Notification": 1,
							"Update": 7
						}
					},
					"MultiHopEnable": false,
					"MultiHopTTL": 0,
					"NeighborAddress": "1.1.1.1",
					"PeerAS": 65535,
					"PeerGroup": "",
					"PeerType": 1,
					"Queues": {
						"Input": 0,
						"Output": 0
					},
					"RouteReflectorClient": false,
					"RouteReflectorClusterId": 0,
					"SessionState": 6, <---------Session is Established
					"TotalPrefixes": 1, <--------Received 1 Prefix
					"UpdateSource": ""
				},
            	"ObjectId": "b72d2e52-8878-490e-5ee8-6873bd40f423"
			}
		]
	}

BGP Routes:

Device1 is receiving 10.10.0.0/24 with next hop of 1.1.1.1, which is the IP address on fpPort47 on Device2 and the redistributed route 10.10.1.0/24 in the BGP table from Vlan10:

::

	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json'  'http://10.1.10.241:8080/public/v1/state/BGPRoutes' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100  5005    0  5005    0     0   489k      0 --:--:-- --:--:-- --:--:--  543k
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 0,
		"ObjCount": 2,
		"Objects": [

			{
				"Object": {
					"CIDRLen": 24,
					"ConfigObj": null,
					"LocalPref": 0,
					"Metric": 0,
					"Network": "10.10.1.0",
					"NextHop": "0.0.0.0",
					"Path": null,
					"PathId": 0,
					"UpdatedDuration": "21m15.486384069s",
					"UpdatedTime": "2016-05-11 12:36:32.932082062 -0700 PDT"
				},
				"ObjectId": ""
			},
			{
				"Object": {
					"CIDRLen": 24,
					"ConfigObj": null,
					"LocalPref": 0,
					"Metric": 0,
					"Network": "10.10.0.0",
					"NextHop": "1.1.1.1",
					"Path": [
                    	"65535",
                	],
					"PathId": 0,
					"UpdatedDuration": "11m15.485818198s",
					"UpdatedTime": "2016-05-11 12:46:02.932650633 -0700 PDT"
				},
				"ObjectId": ""
			}
		]
	}

	





On Device2 (10.1.10.243):

Neighbor 1.1.1.0 in the Established state (Session State 6), and is receiving a single prefix from this peer. 

::
	
	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json'  'http://10.1.10.243:8080/public/v1/state/BGPNeighbors' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100  2270    0  2270    0     0   227k      0 --:--:-- --:--:-- --:--:--  246k
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
					"ConfigObj": null,
					"ConnectRetryTime": 60,
					"Description": "",
					"HoldTime": 180,
					"IfIndex": 0,
					"KeepaliveTime": 60,
					"LocalAS": 65535,
					"MaxPrefixes": 0,
					"MaxPrefixesDisconnect": false,
					"MaxPrefixesRestartTimer": 0,
					"MaxPrefixesThresholdPct": 80,
					"Messages": {
						"Received": {
							"Notification": 1,
							"Update": 9
						},
						"Sent": {
							"Notification": 1,
							"Update": 6
						}
					},
					"MultiHopEnable": false,
					"MultiHopTTL": 0,
					"NeighborAddress": "1.1.1.0",
					"PeerAS": 65535,
					"PeerGroup": "",
					"PeerType": 1,
					"Queues": {
						"Input": 0,
						"Output": 0
					},
					"RouteReflectorClient": false,
					"RouteReflectorClusterId": 0,
					"SessionState": 6, <---------Session is Established
					"TotalPrefixes": 1, <--------Received 1 Prefix
					"UpdateSource": ""
				},
				"ObjectId": "5977ffa7-67bd-4847-7597-4175b513883c"
			}
		]
	}

BGP Routes:

Device2 is receiving 10.10.1.0/24 with next hop of 1.1.1.0, which is the IP address on fpPort47 on Device1 and the redistributed route 10.10.0.0/24 in the BGP table from Vlan10:

::

	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json'  'http://10.1.10.243:8080/public/v1/state/BGPRoutes' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100  3442    0  3442    0     0   411k      0 --:--:-- --:--:-- --:--:--  480k
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 0,
		"ObjCount": 2,
		"Objects": [
			{
				"Object": {
					"CIDRLen": 26,
					"ConfigObj": null,
					"LocalPref": 0,
					"Metric": 0,
					"Network": "10.10.0.0",
					"NextHop": "0.0.0.0",
					"Path": null,
					"PathId": 0,			  
					"UpdatedDuration": "21m14.232453255s",",
					"UpdatedTime": "2016-05-11 12:36:31.432218651 -0700 PDT"
				},
				"ObjectId": ""
			},
			{
				"Object": {
					"CIDRLen": 26,
					"ConfigObj": null,
					"LocalPref": 0,
					"Metric": 0,
					"Network": "10.10.1.0",
					"NextHop": "1.1.1.0",
					"Path": [
						"65535",
					],
					"PathId": 0,
					"UpdatedDuration": "11m14.223927853s",
					"UpdatedTime": "2016-05-11 12:46:02.55002553 -0700 PDT"
				},
				"ObjectId": ""
			}
		]
	}


.. _bgp-neighbor-python:

Configuring with Python SDK
""""""""""""""""""""""""""""
**COMMAND**

::
	
	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("<*IP address*>", <*TCP Port *>).createBGPNeighbor(PeerAS=<*Peer AS Number*>
									LocalAS=<*Local AS number*>,
									AuthPassword=<*Password*>,
									Description=<*Peer Description*>,
									NeighborAddress=<*IPv4 Address*>, 
									IfIndex=<*Interface IfIndex*>,
									RouteReflectorClusterId=<*ClusterID*>,
									RouteReflectorClient=<*true/false*>,
									MultiHopEnable=<*true/false*>,
									MultiHopTTL=<*TTL*>,
									ConnectRetryTime=<*Retry Timer*>,
									HoldTime=<*Hold down Timer*>,
									KeepAliveTime=<*Keepalive Timer*>,
									AddPathRx=<*true/false*>,
									AddPathsMaxTx=<*Max Transmit AddPaths*>,
									PeerGroup=<*Peer Group Name*>,
									BfdEnable=<*true/false*>,
									BfdSessionParam=<*Bfd session param profile*>,
									MaxPrefixes=<*number of prefix's*>,
									MaxPrefixesThresholdPct=<*Percentage of Prefix's*>,
									MaxPrefixesDisconnect=<*true/false*>,
									MaxPrefixesRestartTimer=<*Restart Timer*>,)


**OPTIONS**


+----------------------+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| Python Method        | Variables               | Type       |  Description                                                                            | Required |  Default | 
+======================+=========================+============+=========================================================================================+==========+==========+
| createBGPNeighbor    | PeerAS                  | integer    | Peer AS of the BGP neighbor                                                             |    Yes   |   None   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | LocalAS                 | integer    | Local AS of the BGP, overrides Global AS value, can be used to spoof AS number          |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | AuthPassword            | string     | Password to connect to the BGP neighbor                                                 |    no    |   None   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | Description             | string     | Description of the BGP neighbor                                                         |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | NeighborAddress         | string     | Address of the BGP neighbor (required if IfIndex is not supplied)                       |    Yes   |   None   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | IfIndex                 | integer    | Interface of BGP neighbor (required if NeighborAddress is not supplied)                 |    Yes   |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | RouteReflectorClusterId | integer    | Cluster ID of the internal BGP neighbor router reflector client                         |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | RouteReflectorClient    | boolean    | Set/Clear BGP neighbor as a route reflector client                                      |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MultiHopEnable          | boolean    | Enable/Disable multihop for BGP neighbor                                                |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MultiHopTTL             | string     | Number of hops(TTL) to multi-hop BGP neighbor                                           |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | ConnectRetryTime        | integer    | Retry timer for BGP session reconnect attempt after disconnect/failure                  |    no    |    60s   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | HoldTime                | integer    | Hold down time for BGP neighbor failure/disconnect                                      |    no    |   180s   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | KeepaliveTime           | integer    | Frequency of BGP Keepalive messages                                                     |    no    |    60s   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | AddPathsRx              | boolean    | Enable/Disable reception of BGP Add-Path NLRI updates                                   |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | AddPathsMaxTx           | integer    | Max number of additional paths that can be transmitted to BGP neighbor                  |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | PeerGroup               | string     | Peer group to inherit common configuration for BGP neighbors                            |    no    |   None   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | BfdEnable               | boolean    | Enable/Disable BFD for BGP neigbor                                                      |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | BfdSessionParam         | string     | BFD session parameter profile name to be utilized by BFD session                        |    no    |   None   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MaxPrefixes             | integer    | Maximum number of prefixes that can be received from the BGP neighbor                   |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MaxPrefixesThresholdPct | string     | The percentage of MaxPrefixes before we start logging                                   |    no    |    80%   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MaxPrefixesDisconnect   | boolean    | Disconnect the BGP peer session when we receive the max prefixes from the neighbor      |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MaxPrefixesRestartTimer | string     | Time in seconds to wait before we start BGP peer session when we receive max prefixes   |    no    |   None   |                      
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | UpdateSource            | string     | Interface to source BGP session.  Utilizes Egress interface IP with this is not present |    no    |   None   |                      
+----------------------+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+


**EXAMPLE:**

Here we will configure a BGP session between two devices running FlexSwitch and check the status of these devices. 

Currently we are keeping track of BGP session FSM states based on a numeric value:

+---------------+--------------+
| BGP FSM state | Numeric value|
+---------------+--------------+
| Idle          |      1       |
+---------------+--------------+
| Active        |      2       |
+---------------+--------------+
| Connect       |      3       |
+---------------+--------------+
| OpenSent      |      4       |
+---------------+--------------+
| OpenConfirm   |      5       |
+---------------+--------------+
| Established   |      6       |
+---------------+--------------+


Below we will demonstrate how to create a BGP neighbor relationship between two BGP peers, Device1(10.1.10.241) and Device2(10.1.10.243) in AS 65535.  Display the BGP sessions status on each device and that they are exchanging a connected route from interface Vlan10.  

.. Note:: This is assuming each device has BGP enabled and are in AS 65535 and redistribution of connected routes has been enabled for Vlan10. 


See Topology1 for details:

.. image:: images/BGP_Diagram1.png


1. On device1 (10.1.10.241), we will create a neighbor to 1.1.1.1 from IPv4 1.1.1.0

	::
	
		>>> from flexswitchV2 import FlexSwitch
		>>> FlexSwitch("10.1.0.241", 8080).createBGPNeighbor(PeerAS=65535 , NeighborAddress="1.1.1.1", IfIndex=0)
		({u'ObjectId': u'a34dde27-eea0-40ee-43f0-2836376accb7', u'Error': u''}, None)

2. On device2 (10.1.10.243), we will create a neighbor to 1.1.1.0 from IPv4 1.1.1.1
	::

		>>> from flexswitchV2 import FlexSwitch
		>>> FlexSwitch("10.1.0.243", 8080).createBGPNeighbor(PeerAS=65535 , NeighborAddress="1.1.1.0", IfIndex=0)
		({u'ObjectId': u'28fb7889-ee13-4ee8-4d4b-784d8121f707', u'Error': u''}, None)

.. Note:: You can run Python SDK methods from any location that has IP connectivity to FlexSwitch.  


3. Validation:

Below it can be seen that both Device1 and Device2 are in the Established state (Session State 6), and are exchanging routing information for the prefix on Vlan10. 


On Device1 (10.1.10.241):

::
	
	>>> print json.dumps(FlexSwitch("10.1.10.241", 8080).getAllBGPNeighborStates(), indent=4)
	[
		{
			"Object": {
				"RouteReflectorClient": false, 
				"MultiHopTTL": 0, 
				"BfdNeighborState": "", 
				"LocalAS": 65535, 
				"KeepaliveTime": 60, 
				"AddPathsRx": false, 
				"PeerGroup": "", 
				"PeerType": 0, 
				"MaxPrefixesRestartTimer": 0, 
				"Description": "", 
				"TotalPrefixes": 1, <-------Received 1 Prefix
				"MultiHopEnable": false, 
				"SessionState": 6, <-------Session is Established
				"PeerAS": 65535, 
				"ConfigObj": null, 
				"RouteReflectorClusterId": 0, 
				"MaxPrefixesDisconnect": false, 
				"Queues": {
					"Input": 0, 
					"Output": 0
				}, 
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
				"AddPathsMaxTx": 0, 
				"NeighborAddress": "1.1.1.0", 
				"MaxPrefixes": 0, 
				"MaxPrefixesThresholdPct": 80, 
				"AuthPassword": "", 
				"IfIndex": 0, 
				"HoldTime": 180, 
				"ConnectRetryTime": 60,
				"UpdateSource": ""
			}, 
			"ObjectId": "358c6e8c-0b25-45b3-6f9c-2adef0d9b48c"
		}
	]


BGP Routes:

Device1 is receiving 10.10.0.0/24 with next hop of 1.1.1.1, which is the IP address on fpPort47 on Device2 and the redistributed route 10.10.1.0/24 in the BGP table from Vlan10:

::

	>>> print json.dumps(FlexSwitch("10.1.10.241", 8080).getAllBGPRouteStates(), indent=4)
	[
		{
			"Object": {
				"CIDRLen": 24,
				"ConfigObj": null,
				"LocalPref": 0,
				"Metric": 0,
				"Network": "10.10.1.0",
				"NextHop": "0.0.0.0",
				"Path": null,
				"PathId": 0,
				"UpdatedDuration": "21m15.486384069s",
				"UpdatedTime": "2016-05-11 12:36:32.932082062 -0700 PDT"
			},
			"ObjectId": ""
		},
		{
			"Object": {
				"CIDRLen": 24,
				"ConfigObj": null,
				"LocalPref": 0,
				"Metric": 0,
				"Network": "10.10.2.0",
				"NextHop": "1.1.1.1",
				"Path": [
					"65535",
				],
				"PathId": 0,
				"UpdatedDuration": "11m15.485818198s",
				"UpdatedTime": "2016-05-11 12:46:02.932650633 -0700 PDT"
			},
			"ObjectId": ""
		}
	]




On Device2 (10.1.10.243):

::
	
	>>> print json.dumps(FlexSwitch("10.1.10.243", 8080).getAllBGPNeighborStates(), indent=4)
	[
		{
			"Object": {
				"RouteReflectorClient": false, 
				"MultiHopTTL": 0, 
				"BfdNeighborState": "", 
				"LocalAS": 65535, 
				"KeepaliveTime": 60, 
				"AddPathsRx": false, 
				"PeerGroup": "", 
				"PeerType": 0, 
				"MaxPrefixesRestartTimer": 0, 
				"Description": "", 
				"TotalPrefixes": 1, <-------Received 1 Prefix
				"MultiHopEnable": false, 
				"SessionState": 6, <-------Session is Established
				"PeerAS": 65535, 
				"ConfigObj": null, 
				"RouteReflectorClusterId": 0, 
				"MaxPrefixesDisconnect": false, 
				"Queues": {
					"Input": 0, 
					"Output": 0
				}, 
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
				"AddPathsMaxTx": 0, 
				"NeighborAddress": "1.1.1.1", 
				"MaxPrefixes": 0, 
				"MaxPrefixesThresholdPct": 80, 
				"AuthPassword": "", 
				"IfIndex": 0, 
				"HoldTime": 180, 
				"ConnectRetryTime": 60,
				"UpdateSource": ""
			}, 
			"ObjectId": "28fb7889-ee13-4ee8-4d4b-784d8121f707"
		}
	]


BGP Routes:

::

	>>> print json.dumps(FlexSwitch("10.1.10.243", 8080).getAllBGPRouteStates(), indent=4)
	[
		{
 			"Object": {
                "CIDRLen": 26,
                "ConfigObj": null,
                "LocalPref": 0,
                "Metric": 0,
                "Network": "10.10.1.0",
                "NextHop": "0.0.0.0",
                "Path": null,
                "PathId": 0,			  
                "UpdatedDuration": "21m14.232453255s",",
                "UpdatedTime": "2016-05-11 12:36:31.432218651 -0700 PDT"
            },
            "ObjectId": ""
        },
        {
            "Object": {
                "CIDRLen": 26,
                "ConfigObj": null,
                "LocalPref": 0,
                "Metric": 0,
                "Network": "10.10.0.0",
                "NextHop": "1.1.1.1",
                "Path": [
                    "65535",
                ],
                "PathId": 0,
                "UpdatedDuration": "11m14.223927853s",
                "UpdatedTime": "2016-05-11 12:46:02.55002553 -0700 PDT"
            },
            "ObjectId": ""
		}
	]





Peer Groups
^^^^^^^^^^^

PeerGroups are utilized in order to apply common parameters to multiple BGP neighbors, such as Peer AS, Timers, and routing policies, etc.   The advantage is the ability to apply and adjust variables common to multiple neighbor as well as a reduction to the amount of overall configuration required.  

.. Note:: Configuration applied directly to a neighbor takes precedence over configuration applied via a peer groups.  Configured peer group values, take precedence over default applied values on neighbor configuration. 

Utilizing Peer Groups
"""""""""""""""""""""

Below is example of creating a Peer Group and applying it to a neighbor.  We will set the BGP Hold Time, Keep Alive Time for multiple neighbors. 

Configuring with Rest API 
*************************

**COMMAND**

::

	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"PeerAS":<*Peer AS Number*>,"AuthPassword":<*Password*>,"Description":<*Peer Description*>,"RouteReflectorClusterId":<*ClusterID*>,"RouteReflectorClient":<*true/false*>,"MultiHopEnable":<*true/false*>,"MultiHopTTL":<*TTL*>, "ConnectRetryTime":<*Retry Timer*>, "HoldTime":<*Hold down Timer*>, "KeepAliveTime":<*Keepalive Timer*>, "AddPathRx":<*true/false*>, "AddPathsMaxTx":<*Max Transmit AddPaths*>, "MaxPrefixes"":<*number of prefix's*>, "MaxPrefixesThresholdPct":<*Percentage of Prefix's*>, "MaxPrefixesDisconnect":<*true/false*>, "MaxPrefixesRestartTimer":<*Restart Timer*>	}' 'http://<*your-switchip*>:8080/public/v1/config/BGPNeighbor'


**OPTIONS**

+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| Variables               | Type       |  Description                                                                            | Required |  Default | 
+=========================+============+=========================================================================================+==========+==========+
| Name                    | string     | Name of the BGP peer group                                                              |    Yes   |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| PeerAS                  | integer    | Peer AS of the BGP neighbor                                                             |    Yes   |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| AuthPassword            | string     | Password to connect to the BGP neighbor                                                 |    no    |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| Description             | string     | Description of the BGP neighbor                                                         |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| RouteReflectorClusterId | integer    | Cluster ID of the internal BGP neighbor router reflector client                         |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| RouteReflectorClient    | boolean    | Set/Clear BGP neighbor as a route reflector client                                      |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MultiHopEnable          | boolean    | Enable/Disable multihop for BGP neighbor                                                |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MultiHopTTL             | string     | Number of hops(TTL) to multi-hop BGP neighbor                                           |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| ConnectRetryTime        | integer    | Retry timer for BGP session reconnect attempt after disconnect/failure                  |    no    |    60s   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| HoldTime                | integer    | Hold down time for BGP neighbor failure/disconnect                                      |    no    |   180s   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| KeepaliveTime           | integer    | Frequency of BGP Keepalive messages                                                     |    no    |    60s   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| AddPathsRx              | boolean    | Enable/Disable reception of BGP Add-Path NLRI updates                                   |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| AddPathsMaxTx           | integer    | Max number of additional paths that can be transmitted to BGP neighbor                  |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MaxPrefixes             | integer    | Maximum number of prefixes that can be received from the BGP neighbor                   |    no    |     0    |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MaxPrefixesThresholdPct | string     | The percentage of MaxPrefixes before we start logging                                   |    no    |    80%   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MaxPrefixesDisconnect   | boolean    | Disconnect the BGP peer session when we receive the max prefixes from the neighbor      |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| MaxPrefixesRestartTimer | string     | Time in seconds to wait before we start BGP peer session when we receive max prefixes   |    no    |   None   |                      
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+


**EXAMPLE**

The example provided will utilize the *Topology 1* seen below:

Topology 1:

.. image:: images/BGP_Diagram1.png

1. On device1 (10.1.10.241), where I will create Peer Group *Group1*, setting the Keep Alive Time, Hold Time and Connect Retry Time. 
	:: 
	
		curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"KeepaliveTime":30, "HoldTime":90, "ConnectRetryTime":30 ,  "Name":"Group1"}' 'http://10.1.10.241:8080/public/v1/config/BGPPeerGroup'
		{"ObjectId":"fb508ac1-9958-4922-7cfe-b41a48f9a72d","Error":""}
		

2. On device2 (10.1.10.243), where I will create Peer Group *Group1*, setting the Keep Alive Time, Hold Time and Connect Retry Time. 

	::

		curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"KeepaliveTime":30, "HoldTime":90, "ConnectRetryTime":30 ,  "Name":"Group1"}' 'http://10.1.10.243:8080/public/v1/config/BGPPeerGroup'
		{"ObjectId":"5977ffa7-67bd-4847-7597-4175b513883c","Error":""}
	

3. Utilizing previously created Neighbors on Device1 to apply Peer Group *Group1*

	a. Existing neighbor configuration on Device1 
	
		.. Note:: PeerGroup field is blank
	
		::

			curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.241:8080/public/v1/config/BGPNeighbors' | python -m json.tool
			  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
											 Dload  Upload   Total   Spent    Left  Speed
			100   612  100   612    0     0  43290      0 --:--:-- --:--:-- --:--:-- 47076
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
							"BfdEnable": false,
							"BfdSessionParam": "default",
							"ConfigObj": null,
							"ConnectRetryTime": 60,
							"Description": "",
							"HoldTime": 180,
							"IfIndex": 0,
							"KeepaliveTime": 60,
							"LocalAS": 0,
							"MaxPrefixes": 0,
							"MaxPrefixesDisconnect": false,
							"MaxPrefixesRestartTimer": 0,
							"MaxPrefixesThresholdPct": 80,
							"MultiHopEnable": false,
							"MultiHopTTL": 0,
							"NeighborAddress": "1.1.1.0",
							"PeerAS": 65535,
							"PeerGroup": "",
							"RouteReflectorClient": false,
							"RouteReflectorClusterId": 0
						},
						"ObjectId": "358c6e8c-0b25-45b3-6f9c-2adef0d9b48c"
					}
				]
			}
			
	b. Peer Group Configuration:
		
		Below we can see the following timers have been set within the Peer Group:
				
				* KeepaliveTime = 30
				* ConnectRetryTime = 30
				* HoldTime = 90
		
		::

			curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.241:8080/public/v1/config/BGPPeerGroups' | python -m json.tool
			  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
											 Dload  Upload   Total   Spent    Left  Speed
			100   966  100   966    0     0   302k      0 --:--:-- --:--:-- --:--:--  471k
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
							"ConfigObj": null,
							"ConnectRetryTime": 30,
							"Description": "",
							"HoldTime": 90,
							"KeepaliveTime": 30,
							"LocalAS": 0,
							"MaxPrefixes": 0,
							"MaxPrefixesDisconnect": false,
							"MaxPrefixesRestartTimer": 0,
							"MaxPrefixesThresholdPct": 0,
							"MultiHopEnable": false,
							"MultiHopTTL": 0,
							"Name": "Group2",
							"PeerAS": 0,
							"RouteReflectorClient": false,
							"RouteReflectorClusterId": 0
						},
						"ObjectId": "fb508ac1-9958-4922-7cfe-b41a48f9a72d"
					},
				]
			}
			

	c. Applying Peer Group
	
		::
			
			curl -X PATCH --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"NeighborAddress":"1.1.1.0", "PeerGroup":"Group1"}' 'http://10.1.10.241:8080/public/v1/config/BGPNeighbor'
			{"ObjectId":"358c6e8c-0b25-45b3-6f9c-2adef0d9b48c","Error":"None."}

	d. Verification PeerGroup is applied to Neighbors
	
		We can see below in the configuration and state objects, that the "PeerGroup" field now has the value assigned to *Group1*

		.. Note:: The timers specified in the Peer Group, *Group1*, have been updated to reflect the timers on the neighbor State Object.  The configuration object reflects the default configuration on the neighbor.  If these values were user configured, they would take precedence. 
	
		**Config:**
			::

				curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.241:8080/public/v1/config/BGPNeighbors' | python -m json.tool
				  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
												 Dload  Upload   Total   Spent    Left  Speed
				100   618  100   618    0     0   399k      0 --:--:-- --:--:-- --:--:--  603k
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
								"BfdEnable": false,
								"BfdSessionParam": "default",
								"ConfigObj": null,
								"ConnectRetryTime": 60,
								"Description": "",
								"HoldTime": 180,
								"IfIndex": 0,
								"KeepaliveTime": 60,
								"LocalAS": 0,
								"MaxPrefixes": 0,
								"MaxPrefixesDisconnect": false,
								"MaxPrefixesRestartTimer": 0,
								"MaxPrefixesThresholdPct": 80,
								"MultiHopEnable": false,
								"MultiHopTTL": 0,
								"NeighborAddress": "1.1.1.0",
								"PeerAS": 65535,
								"PeerGroup": "Group1", <---------------
								"RouteReflectorClient": false,
								"RouteReflectorClusterId": 0
							},
							"ObjectId": "358c6e8c-0b25-45b3-6f9c-2adef0d9b48c"
						}
					]
				}


		**State**
			::

				curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.241:8080/public/v1/state/BGPNeighbors' | python -m json.tool
				  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
												 Dload  Upload   Total   Spent    Left  Speed
				100   765  100   765    0     0   269k      0 --:--:-- --:--:-- --:--:--  373k
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
								"ConfigObj": null,
								"ConnectRetryTime": 30, <---------------
								"Description": "",
								"HoldTime": 90,<---------------
								"IfIndex": 0,
								"KeepaliveTime": 30,<---------------
								"LocalAS": 0,
								"MaxPrefixes": 0,
								"MaxPrefixesDisconnect": false,
								"MaxPrefixesRestartTimer": 0,
								"MaxPrefixesThresholdPct": 80,
								"Messages": {
									"Received": {
										"Notification": 0,
										"Update": 3
									},
									"Sent": {
										"Notification": 0,
										"Update": 2
									}
								},
								"MultiHopEnable": false,
								"MultiHopTTL": 0,
								"NeighborAddress": "1.1.1.1",
								"PeerAS": 65535,
								"PeerGroup": "Group1",<---------------
								"PeerType": 0,
								"Queues": {
									"Input": 0,
									"Output": 0
								},
								"RouteReflectorClient": false,
								"RouteReflectorClusterId": 0,
								"SessionState": 6,
								"TotalPrefixes": 1
							},
							"ObjectId": "358c6e8c-0b25-45b3-6f9c-2adef0d9b48c"
						}
					]
				}

4. Utilizing previously created Neighbors on Device2 to apply Peer Group *Group1*

	a. Existing neighbor configuration on Device2
	
		.. Note:: PeerGroup field is blank
	
		::

			curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.243:8080/public/v1/config/BGPNeighbors' | python -m json.tool
			  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
											 Dload  Upload   Total   Spent    Left  Speed
			100   612  100   612    0     0  43290      0 --:--:-- --:--:-- --:--:-- 47076
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
							"BfdEnable": false,
							"BfdSessionParam": "default",
							"ConfigObj": null,
							"ConnectRetryTime": 60,
							"Description": "",
							"HoldTime": 180,
							"IfIndex": 0,
							"KeepaliveTime": 60,
							"LocalAS": 0,
							"MaxPrefixes": 0,
							"MaxPrefixesDisconnect": false,
							"MaxPrefixesRestartTimer": 0,
							"MaxPrefixesThresholdPct": 80,
							"MultiHopEnable": false,
							"MultiHopTTL": 0,
							"NeighborAddress": "1.1.1.1",
							"PeerAS": 65535,
							"PeerGroup": "",  <---------------
							"RouteReflectorClient": false,
							"RouteReflectorClusterId": 0
						},
						"ObjectId": "086b6651-474d-493a-4b3f-ee756435ac95"
					}
				]
			}

	b. Peer Group Configuration:
		
		Below we can see the following timers have been set within the Peer Group:
				
				* KeepaliveTime = 30
				* ConnectRetryTime = 30
				* HoldTime = 90
		
		::

			curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.243:8080/public/v1/config/BGPPeerGroups' | python -m json.tool
			  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
											 Dload  Upload   Total   Spent    Left  Speed
			100   966  100   966    0     0   302k      0 --:--:-- --:--:-- --:--:--  471k
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
							"ConfigObj": null,
							"ConnectRetryTime": 30,
							"Description": "",
							"HoldTime": 90,
							"KeepaliveTime": 30,
							"LocalAS": 0,
							"MaxPrefixes": 0,
							"MaxPrefixesDisconnect": false,
							"MaxPrefixesRestartTimer": 0,
							"MaxPrefixesThresholdPct": 0,
							"MultiHopEnable": false,
							"MultiHopTTL": 0,
							"Name": "Group2",
							"PeerAS": 0,
							"RouteReflectorClient": false,
							"RouteReflectorClusterId": 0
						},
						"ObjectId": "5977ffa7-67bd-4847-7597-4175b513883c"
					},
				]
			}
			
	c. Applying Peer Group:
		
		::
			
			curl -X PATCH --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"NeighborAddress":"1.1.1.1", "PeerGroup":"Group1"}' 'http://10.1.10.243:8080/public/v1/config/BGPNeighbor'
			{"ObjectId":"086b6651-474d-493a-4b3f-ee756435ac95","Error":"None."}

	d. Verification PeerGroup is applied:

		We can see below in the configuration and state objects, that the "PeerGroup" field now has the value assigned to *Group1*

		.. Note:: The timers specified in the Peer Group, *Group1*, have been updated to reflect the timers on the neighbor State Object.  The configuration object reflects the default configuration on the neighbor.  If these values were user configured, they would take precedence. 
	
		**Config:**
			::

				curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.243:8080/public/v1/config/BGPNeighbors' | python -m json.tool
				  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
												 Dload  Upload   Total   Spent    Left  Speed
				100   618  100   618    0     0   399k      0 --:--:-- --:--:-- --:--:--  603k
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
								"BfdEnable": false,
								"BfdSessionParam": "default",
								"ConfigObj": null,
								"ConnectRetryTime": 60,
								"Description": "",
								"HoldTime": 180,
								"IfIndex": 0,
								"KeepaliveTime": 60,
								"LocalAS": 0,
								"MaxPrefixes": 0,
								"MaxPrefixesDisconnect": false,
								"MaxPrefixesRestartTimer": 0,
								"MaxPrefixesThresholdPct": 80,
								"MultiHopEnable": false,
								"MultiHopTTL": 0,
								"NeighborAddress": "1.1.1.1",
								"PeerAS": 65535,
								"PeerGroup": "Group1", <------------------
								"RouteReflectorClient": false,
								"RouteReflectorClusterId": 0
							},
							"ObjectId": "086b6651-474d-493a-4b3f-ee756435ac95"
						}
					]
				}


		**State**
			::

				curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.243:8080/public/v1/state/BGPNeighbors' | python -m json.tool
				  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
												 Dload  Upload   Total   Spent    Left  Speed
				100   765  100   765    0     0   269k      0 --:--:-- --:--:-- --:--:--  373k
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
								"ConfigObj": null,
								"ConnectRetryTime": 30,<---------------
								"Description": "",
								"HoldTime": 90,<---------------
								"IfIndex": 0,
								"KeepaliveTime": 30,<---------------
								"LocalAS": 0,
								"MaxPrefixes": 0,
								"MaxPrefixesDisconnect": false,
								"MaxPrefixesRestartTimer": 0,
								"MaxPrefixesThresholdPct": 80,
								"Messages": {
									"Received": {
										"Notification": 0,
										"Update": 3
									},
									"Sent": {
										"Notification": 0,
										"Update": 2
									}
								},
								"MultiHopEnable": false,
								"MultiHopTTL": 0,
								"NeighborAddress": "1.1.1.1",
								"PeerAS": 65535,
								"PeerGroup": "Group1", <------------------
								"PeerType": 0,
								"Queues": {
									"Input": 0,
									"Output": 0
								},
								"RouteReflectorClient": false,
								"RouteReflectorClusterId": 0,
								"SessionState": 6,
								"TotalPrefixes": 1
							},
							"ObjectId": "086b6651-474d-493a-4b3f-ee756435ac95"
						}
					]
				}


Configuring with Python SDK
***************************


**COMMAND**

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("<*IP address*>", <*TCP Port *>).createBGPPeerGroup(PeerAS=<*Peer AS Number*>
									AuthPassword=<*Password*>,
									Description=<*Peer Description*>,
									RouteReflectorClusterId=<*ClusterID*>,
									RouteReflectorClient=<*true/false*>,
									MultiHopEnable=<*true/false*>,
									MultiHopTTL=<*TTL*>,
									ConnectRetryTime=<*Retry Timer*>,
									HoldTime=<*Hold down Timer*>,
									KeepAliveTime=<*Keepalive Timer*>,
									AddPathRx=<*true/false*>,
									AddPathsMaxTx=<*Max Transmit AddPaths*>,
									MaxPrefixes=<*number of prefix's*>,
									MaxPrefixesThresholdPct=<*Percentage of Prefix's*>,
									MaxPrefixesDisconnect=<*true/false*>,
									MaxPrefixesRestartTimer=<*Restart Timer*>,)

	


**OPTIONS**

+----------------------+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| Python Method        | Variables               | Type       |  Description                                                                            | Required |  Default | 
+======================+=========================+============+=========================================================================================+==========+==========+
| createBGPPeerGroup   | Name                    | string     | Name of the BGP peer group                                                              |    Yes   |   None   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | PeerAS                  | integer    | Peer AS of the BGP neighbor                                                             |    Yes   |   None   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | AuthPassword            | string     | Password to connect to the BGP neighbor                                                 |    no    |   None   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | Description             | string     | Description of the BGP neighbor                                                         |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | RouteReflectorClusterId | integer    | Cluster ID of the internal BGP neighbor router reflector client                         |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | RouteReflectorClient    | boolean    | Set/Clear BGP neighbor as a route reflector client                                      |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MultiHopEnable          | boolean    | Enable/Disable multihop for BGP neighbor                                                |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MultiHopTTL             | string     | Number of hops(TTL) to multi-hop BGP neighbor                                           |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | ConnectRetryTime        | integer    | Retry timer for BGP session reconnect attempt after disconnect/failure                  |    no    |    60s   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | HoldTime                | integer    | Hold down time for BGP neighbor failure/disconnect                                      |    no    |   180s   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | KeepaliveTime           | integer    | Frequency of BGP Keepalive messages                                                     |    no    |    60s   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | AddPathsRx              | boolean    | Enable/Disable reception of BGP Add-Path NLRI updates                                   |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | AddPathsMaxTx           | integer    | Max number of additional paths that can be transmitted to BGP neighbor                  |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MaxPrefixes             | integer    | Maximum number of prefixes that can be received from the BGP neighbor                   |    no    |     0    |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MaxPrefixesThresholdPct | string     | The percentage of MaxPrefixes before we start logging                                   |    no    |    80%   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MaxPrefixesDisconnect   | boolean    | Disconnect the BGP peer session when we receive the max prefixes from the neighbor      |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | MaxPrefixesRestartTimer | string     | Time in seconds to wait before we start BGP peer session when we receive max prefixes   |    no    |   None   |                      
+----------------------+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+


**EXAMPLE**

The example provided will utilize the *Topology 1* seen below:

Topology 1:

.. image:: images/BGP_Diagram1.png

1. On device1 (10.1.10.241), where I will create Peer Group *Group1*, setting the Keep Alive Time, Hold Time and Connect Retry Time. 

	::
	
		>>> from flexswitchV2 import FlexSwitch
		>>> FlexSwitch("10.1.0.241", 8080).createBGPPeerGroup(KeepaliveTime=30, HoldTime=90, ConnectRetryTime=30 , Name="Group1")
		({u'ObjectId': u'f91bc8e5-fcb7-461a-4c17-5298b19ab280', u'Error': u''}, None)
		

2. On device2 (10.1.10.243), where I will create Peer Group *Group1*, setting the Keep Alive Time, Hold Time and Connect Retry Time. 

	::
	
		>>> from flexswitchV2 import FlexSwitch
		>>> FlexSwitch("10.1.0.243", 8080).createBGPPeerGroup(KeepaliveTime=30, HoldTime=90, ConnectRetryTime=30 , Name="Group1")
		({u'ObjectId': u'5683eeac-8457-65bd-43f0-23642abf2e78', u'Error': u''}, None)


3. Utilizing previously created neighbors on Device1 to apply Peer Group *Group1*

	a. Existing neighbor configuration on Device1 
	
		.. Note:: PeerGroup field is blank

		::
		
			>>> print json.dumps(FlexSwitch("10.1.10.241", 8080).getAllBGPNeighbors(), indent=4)
			[
				{
					"Object": {
						"BfdEnable": False, 
						"RouteReflectorClient": false, 
						"MultiHopTTL": 0, 
						"LocalAS": 0, 
						"KeepaliveTime": 60, 
						"AddPathsRx": false, 
						"UpdateSource": " ", 
						"PeerGroup": "", 
						"MaxPrefixesRestartTimer": 0, 
						"Description": "", 
						"MultiHopEnable": false, 
						"AuthPassword": "", 
						"RouteReflectorClusterId": 0, 
						"MaxPrefixesDisconnect": false, 
						"PeerAS": 65535, 
						"AddPathsMaxTx": 0, 
						"NeighborAddress": "1.1.1.0", 
						"MaxPrefixes": 0, 
						"MaxPrefixesThresholdPct": 80, 
						"HoldTime": 180, 
						"IfIndex": 0, 
						"BfdSessionParam": "", 
						"ConnectRetryTime": 60
					}, 
					"ObjectId": "fd88413e-b0b5-420b-5596-ea0bd2337064"
				}, 
			]
			
	b. Peer Group Configuration:
		
		Below we can see the following timers have been set within the Peer Group:
				
				* KeepaliveTime = 30
				* ConnectRetryTime = 30
				* HoldTime = 90

		::
		
			>>> print json.dumps(FlexSwitch("10.1.10.241", 8080).getAllBGPPeerGroups(), indent=4)
			[
				{
					"Object": {
						"RouteReflectorClusterId": 0, 
						"RouteReflectorClient": false, 
						"Description": "", 
						"MaxPrefixes": 0, 
						"MultiHopTTL": 0, 
						"MaxPrefixesDisconnect": false, 
						"PeerAS": 0, 
						"KeepaliveTime": 30, 
						"AuthPassword": "", 
						"MaxPrefixesRestartTimer": 0, 
						"AddPathsMaxTx": 0, 
						"MultiHopEnable": false, 
						"AddPathsRx": false, 
						"UpdateSource": " ", 
						"ConnectRetryTime": 30, 
						"HoldTime": 90, 
						"LocalAS": 0, 
						"MaxPrefixesThresholdPct": 0, 
						"Name": "Group1"
					}, 
					"ObjectId": "f91bc8e5-fcb7-461a-4c17-5298b19ab280"
				}
			]
		
	c. Applying Peer Group
	
		::
			
			>>> FlexSwitch("10.1.0.241", 8080).updateBGPNeighbor(NeighborAddress="1.1.1.0", PeerGroup="Group1")
			({u'ObjectId': u'fd88413e-b0b5-420b-5596-ea0bd2337064', u'Error': u''}, None)
			
	d. Verification PeerGroup is applied to Neighbors
	
		We can see below in the configuration and state objects, that the "PeerGroup" field now has the value assigned to *Group1*

		.. Note:: The timers specified in the Peer Group, *Group1*, have been updated to reflect the timers on the neighbor State Object.  The configuration object reflects the default configuration on the neighbor.  If these values were user configured, they would take precedence. 
	
		**Config:**
			::

				>>> print json.dumps(FlexSwitch("10.1.10.241", 8080).getAllBGPNeighbors(), indent=4)
				[
					{
						"Object": {
							"BfdEnable": false, 
							"RouteReflectorClient": false, 
							"MultiHopTTL": 0, 
							"LocalAS": 0, 
							"KeepaliveTime": 60, 
							"AddPathsRx": false, 
							"PeerGroup": "Group1", <---------------
							"MaxPrefixesRestartTimer": 0, 
							"Description": "", 
							"MultiHopEnable": false, 
							"AuthPassword": "", 
							"RouteReflectorClusterId": 0, 
							"MaxPrefixesDisconnect": false, 
							"PeerAS": 65535, 
							"AddPathsMaxTx": 0, 
							"NeighborAddress": "1.1.1.0", 
							"MaxPrefixes": 0, 
							"MaxPrefixesThresholdPct": 80, 
							"HoldTime": 180, 
							"IfIndex": 0, 
							"BfdSessionParam": "default", 
							"ConnectRetryTime": 60
						}, 
						"ObjectId": "fd88413e-b0b5-420b-5596-ea0bd2337064"
					},

		**State**
			::

				>>> print json.dumps(FlexSwitch("10.1.10.241", 8080).getAllBGPNeighborStates(), indent=4)
				[
					{
						"Object": {
							"RouteReflectorClient": false, 
							"MultiHopTTL": 0, 
							"BfdNeighborState": "", 
							"LocalAS": 0, 
							"KeepaliveTime": 30, <---------------
							"AddPathsRx": false, 
							"PeerGroup": "Group1", <---------------
							"PeerType": 1, 
							"MaxPrefixesRestartTimer": 0, 
							"Description": "", 
							"TotalPrefixes": 8, 
							"MultiHopEnable": false, 
							"SessionState": 6, 
							"PeerAS": 65535, 
							"RouteReflectorClusterId": 0, 
							"MaxPrefixesDisconnect": false, 
							"Queues": {
								"Input": 0, 
								"Output": 0
							}, 
							"Messages": {
								"Received": {
									"Notification": 0, 
									"Update": 3
								}, 
								"Sent": {
									"Notification": 0, 
									"Update": 4
								}
							}, 
							"AddPathsMaxTx": 0, 
							"NeighborAddress": "1.1.1.0", 
							"MaxPrefixes": 0, 
							"MaxPrefixesThresholdPct": 80, 
							"AuthPassword": "", 
							"IfIndex": 0, 
							"HoldTime": 90, <---------------
							"ConnectRetryTime": 30 <---------------
						}, 
						"ObjectId": "fd88413e-b0b5-420b-5596-ea0bd2337064"
					}, 


4. Utilizing previously created Neighbors on Device2 to apply Peer Group *Group1*

	a. Existing neighbor configuration on Device2
	
		.. Note:: PeerGroup field is blank

		::
		
			>>> print json.dumps(FlexSwitch("10.1.10.243", 8080).getAllBGPNeighbors(), indent=4)
			[
				{
					"Object": {
						"BfdEnable": False, 
						"RouteReflectorClient": false, 
						"MultiHopTTL": 0, 
						"LocalAS": 0, 
						"KeepaliveTime": 60, 
						"AddPathsRx": false, 
						"UpdateSource": " ", 
						"PeerGroup": "", 
						"MaxPrefixesRestartTimer": 0, 
						"Description": "", 
						"MultiHopEnable": false, 
						"AuthPassword": "", 
						"RouteReflectorClusterId": 0, 
						"MaxPrefixesDisconnect": false, 
						"PeerAS": 65535, 
						"AddPathsMaxTx": 0, 
						"NeighborAddress": "1.1.1.1", 
						"MaxPrefixes": 0, 
						"MaxPrefixesThresholdPct": 80, 
						"HoldTime": 180, 
						"IfIndex": 0, 
						"BfdSessionParam": "", 
						"ConnectRetryTime": 60
					}, 
					"ObjectId": "aad53634-a7d2-2314-9974-dea42f3456ac"
				}, 
			]
			
	b. Peer Group Configuration:
		
		Below we can see the following timers have been set within the Peer Group:
				
				* KeepaliveTime = 30
				* ConnectRetryTime = 30
				* HoldTime = 90

		::
		
			>>> print json.dumps(FlexSwitch("10.1.10.243", 8080).getAllBGPPeerGroups(), indent=4)
			[
				{
					"Object": {
						"RouteReflectorClusterId": 0, 
						"RouteReflectorClient": false, 
						"Description": "", 
						"MaxPrefixes": 0, 
						"MultiHopTTL": 0, 
						"MaxPrefixesDisconnect": false, 
						"PeerAS": 0, 
						"KeepaliveTime": 30, 
						"AuthPassword": "", 
						"MaxPrefixesRestartTimer": 0, 
						"AddPathsMaxTx": 0, 
						"MultiHopEnable": false, 
						"AddPathsRx": false, 
						"UpdateSource": " ", 
						"ConnectRetryTime": 30, 
						"HoldTime": 90, 
						"LocalAS": 0, 
						"MaxPrefixesThresholdPct": 0, 
						"Name": "Group1"
					}, 
					"ObjectId": "5683eeac-8457-65bd-43f0-23642abf2e78"
				}
			]
		
	c. Applying Peer Group
	
		::
			
			>>> FlexSwitch("10.1.0.243", 8080).updateBGPNeighbor(NeighborAddress="1.1.1.0", PeerGroup="Group1")
			({u'ObjectId': u'aad53634-a7d2-2314-9974-dea42f3456ac', u'Error': u''}, None)
			
	d. Verification PeerGroup is applied to Neighbors
	
		We can see below in the configuration and state objects, that the "PeerGroup" field now has the value assigned to *Group1*

		.. Note:: The timers specified in the Peer Group, *Group1*, have been updated to reflect the timers on the neighbor State Object.  The configuration object reflects the default configuration on the neighbor.  If these values were user configured, they would take precedence. 
	
		**Config:**
			::

				>>> print json.dumps(FlexSwitch("10.1.10.243", 8080).getAllBGPNeighbors(), indent=4)
				[
					{
						"Object": {
							"BfdEnable": false, 
							"RouteReflectorClient": false, 
							"MultiHopTTL": 0, 
							"LocalAS": 0, 
							"KeepaliveTime": 60, 
							"AddPathsRx": false, 
							"PeerGroup": "Group1", <---------------
							"MaxPrefixesRestartTimer": 0, 
							"Description": "", 
							"MultiHopEnable": false, 
							"AuthPassword": "", 
							"RouteReflectorClusterId": 0, 
							"MaxPrefixesDisconnect": false, 
							"PeerAS": 65535, 
							"AddPathsMaxTx": 0, 
							"NeighborAddress": "1.1.1.1", 
							"MaxPrefixes": 0, 
							"MaxPrefixesThresholdPct": 80, 
							"HoldTime": 180, 
							"IfIndex": 0, 
							"BfdSessionParam": "default", 
							"ConnectRetryTime": 60
						}, 
						"ObjectId": "aad53634-a7d2-2314-9974-dea42f3456ac"
					},

		**State**
			::

				>>> print json.dumps(FlexSwitch("10.1.10.241", 8080).getAllBGPNeighborStates(), indent=4)
				[
					{
						"Object": {
							"RouteReflectorClient": false, 
							"MultiHopTTL": 0, 
							"BfdNeighborState": "", 
							"LocalAS": 0, 
							"KeepaliveTime": 30, <---------------
							"AddPathsRx": false, 
							"PeerGroup": "Group1", <---------------
							"PeerType": 1, 
							"MaxPrefixesRestartTimer": 0, 
							"Description": "", 
							"TotalPrefixes": 8, 
							"MultiHopEnable": false, 
							"SessionState": 6, 
							"PeerAS": 65535, 
							"RouteReflectorClusterId": 0, 
							"MaxPrefixesDisconnect": false, 
							"Queues": {
								"Input": 0, 
								"Output": 0
							}, 
							"Messages": {
								"Received": {
									"Notification": 0, 
									"Update": 3
								}, 
								"Sent": {
									"Notification": 0, 
									"Update": 4
								}
							}, 
							"AddPathsMaxTx": 0, 
							"NeighborAddress": "1.1.1.1", 
							"MaxPrefixes": 0, 
							"MaxPrefixesThresholdPct": 80, 
							"AuthPassword": "", 
							"IfIndex": 0, 
							"HoldTime": 90, <---------------
							"ConnectRetryTime": 30 <---------------
						}, 
						"ObjectId": "aad53634-a7d2-2314-9974-dea42f3456ac"
					}, 


Enabling BFD 
^^^^^^^^^^^^

To ensure fast fail-over of BGP sessions during times of failures, BFD can be enabled, to enabled to ensure sub-second failure detection.  This is done by enabling BFD for that neighbor and tying a BFD session profile per-neighbor relationship. 

.. Note:: This configuration can be enabled via a Peer Group OR directly on the neighbor itself. See :ref:`bgp-neighbor-rest` or :ref:`bgp-neighbor-python` for more details.

Configuring with Rest API 
"""""""""""""""""""""""""

**COMMAND**

Update BGP neighbor:
::

	curl -X PATCH --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"NeighborAddress":"<*IP Address*>", "BfdEnable":"<*enable/disable BFD*>", "BfdSessionParam":"<*BFD parameter profile*>":}' 'http://10.1.10.245:8080/public/v1/config/BGPNeighbor'

Enabled on BGP neighbor Creation:
::

	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"NeighborAddress":"<*IP Address*>", "BfdEnable":"<*enable/disable BFD*>", "BfdSessionParam":"<*BFD parameter profile*>":}' 'http://10.1.10.245:8080/public/v1/config/BGPNeighbor'


.. Note:: This above example, is just a subset of the BGP Neighbor commands.  See :ref:`bgp-neighbor-rest` for more details


**OPTIONS**

+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| Variables               | Type       |  Description                                                                            | Required |  Default | 
+=========================+============+=========================================================================================+==========+==========+
| NeighborAddress         | string     | Address of the BGP neighbor (required if IfIndex is not supplied)                       |    Yes   |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| BfdEnable               | boolean    | Enable/Disable BFD for BGP neigbor                                                      |    no    |  False   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| BfdSessionParam         | string     | BFD session parameter profile name to be utilized by BFD session                        |    no    |   None   |
+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+


**EXAMPLE**

Below is an example of enabling BFD on a BGP neighbor:

1. Create BFD Session Parameters

	::

		curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"Name":"BFD_session","LocalMultiplier":3,"DesiredMinTxInterval":250,"RequiredMinRxInterval":250}' 'http://10.1.10.245:8080/public/v1/config/BfdSessionParam'
 
	.. Note:: See Creating :ref:`bfd-session-parameters-rest` section for more details. 


2. Attach BFD session parameters and enable BFD on exisiting neighbor
	::
	
		curl -X PATCH --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"NeighborAddress":"1.1.1.1", "BfdEnable":"true", "BfdSessionParam":"BFD_Session":}' 'http://10.1.10.245:8080/public/v1/config/BGPNeighbor'
		{"ObjectId":"fcb3a338-1f10-4a18-56da-cc615516024f","Error":""}

	.. Note:: Assumes BFD is enabled on the far-end BGP neighbor

3. Verify BFD is enabled, in the up state and registered with BGP neighbor:
	
	Below we can see that BFD is up and passing traffic.  The *NumRxPackets* and *NumTxPackets* counters show that we are sending and receiving BFD hello packets. 
	*RegisteredProtocols* is BGP, as well as the *SessionState* being in the **up** states. 


	::

		curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.245:8080/public/v1/state/BfdSessions' | python -m json.tool
		  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
										 Dload  Upload   Total   Spent    Left  Speed
		100  1415  100  1415    0     0   233k      0 --:--:-- --:--:-- --:--:--  276k
		{
			"CurrentMarker": 0,
			"MoreExist": false,
			"NextMarker": 0,
			"ObjCount": 2,
			"Objects": [
				{
					"Object": {
						"AuthSeqKnown": false,
						"AuthType": "",
						"DemandMode": false,
						"DesiredMinTxInterval": "250000(us)",
						"DetectionMultiplier": 3,
						"IfIndex": 30,
						"IfName": "",
						"InterfaceSpecific": false,
						"IpAddr": "1.1.1.1",<--------------
						"LocalDiagType": "None",
						"LocalDiscriminator": 95,
						"LocalMacAddr": "",
						"NumRxPackets": 228806,<--------------
						"NumTxPackets": 236795,<--------------
						"ParamName": "BFD_Session",
						"PerLinkSession": false,
						"ReceivedAuthSeq": 0,
						"RegisteredProtocols": "bgp, ",<--------------
						"RemoteDemandMode": false,
						"RemoteDetectionMultiplier": 3,
						"RemoteDiscriminator": 288,
						"RemoteMacAddr": "",
						"RemoteMinRxInterval": "250000(us)",
						"RemoteSessionState": "up",
						"RequiredMinRxInterval": "250000(us)",
						"SentAuthSeq": 0,
						"SessionId": 95,
						"SessionState": "up"<--------------
					},
					"ObjectId": ""
				},


	For the associated BGP neighbor, we can see that the *BfdNeighborState* is UP and this BGP neighbor *SessionState* in Established (state 6) is up:

	::
	
		curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.245:8080/public/v1/state/BGPNeighbors' | python -m json.tool
		  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
										 Dload  Upload   Total   Spent    Left  Speed
		100  1547  100  1547    0     0   185k      0 --:--:-- --:--:-- --:--:--  215k
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
						"BfdNeighborState": "up", <--------------
						"ConnectRetryTime": 60,
						"Description": "",
						"HoldTime": 180,
						"IfIndex": 0,
						"KeepaliveTime": 60,
						"LocalAS": 420000006,
						"MaxPrefixes": 0,
						"MaxPrefixesDisconnect": false,
						"MaxPrefixesRestartTimer": 0,
						"MaxPrefixesThresholdPct": 80,
						"Messages": {
							"Received": {
								"Notification": 0,
								"Update": 25
							},
							"Sent": {
								"Notification": 2,
								"Update": 27
							}
						},
						"MultiHopEnable": false,
						"MultiHopTTL": 0,
						"NeighborAddress": "1.1.1.1",
						"PeerAS": 420000004,
						"PeerGroup": "Group1",
						"PeerType": 1,
						"Queues": {
							"Input": 0,
							"Output": 0
						},
						"RouteReflectorClient": false,
						"RouteReflectorClusterId": 0,
						"SessionState": 6,<--------------
						"TotalPrefixes": 7,
						"UpdateSource": ""
					},
					"ObjectId": "fcb3a338-1f10-4a18-56da-cc615516024f"
				},	
			]
			
		In the BGP neighbor configuration, we can see the *BfdSessionParam* tied to this neighbor is BFD_Session:
			::

			
Configuring with Python SDK
"""""""""""""""""""""""""""
**COMMAND**

Update BGP neighbor:
::

	FlexSwitch("10.1.10.245", 8080).updateBGPNeighbor(NeighborAddress="<*IP Address*>", IfIndex=<*IfIndex*>, BfdSessionParam="<*BFD parameter profile*>", BfdEnable=<*enable/disable bfd*>)

Enabled on BGP neighbor creation:

::
	
	FlexSwitch("10.1.10.245", 8080).createBGPNeighbor(NeighborAddress="<*IP Address*>", IfIndex=<*IfIndex*>, BfdSessionParam="<*BFD parameter profile*>", BfdEnable=<*enable/disable bfd*>)


.. Note:: This above example, is just a subset of the BGP Neighbor commands.  See :ref:`bgp-neighbor-python`

**OPTIONS**

+----------------------+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| Python Method        | Variables               | Type       |  Description                                                                            | Required |  Default | 
+======================+=========================+============+=========================================================================================+==========+==========+
| createBGPNeighbor    | NeighborAddress         | string     | Address of the BGP neighbor (required if IfIndex is not supplied)                       |    Yes   |   None   |
|       OR 	           +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
| updateBGPNeighbor    | BfdEnable               | boolean    | Enable/Disable BFD for BGP neigbor                                                      |    no    |  False   |
|                      +-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+
|                      | BfdSessionParam         | string     | BFD session parameter profile name to be utilized by BFD session                        |    no    |   None   |
+----------------------+-------------------------+------------+-----------------------------------------------------------------------------------------+----------+----------+

**EXAMPLE**


Below is an example of enabling BFD on an existing BGP neighbor:

1. Create BFD Session Parameters

	::

		>>> from flexswitchV2 import FlexSwitch
		>>> FlexSwitch("10.1.10.245", 8080).createBfdSessionParam(Name="BFD_Session", RequiredMinRxInterval=250, DesiredMinTxInterval=250, LocalMultiplier=3)
		({u'ObjectId': u'a4963a6b-b8cc-4dc8-7693-cbf907a0af0f', u'Error': u''}, None) 
	.. Note:: See Creating :ref:`bfd-session-parameters-python` section for more details. 


2. Attach BFD session parameters and enable BFD on exisiting neighbor
	::
	
		FlexSwitch("10.1.10.245", 8080).updateBGPNeighbor(NeighborAddress="1.1.1.1", IfIndex=0, BfdSessionParam="BFD_Session", BfdEnable="True")
		({u'ObjectId': u'3861ec9a-188f-44f2-4e49-db60267c600b', u'Error': u'None.'}, None)

	.. Note:: Assumes BFD is enabled on the far-end BGP neighbor

3. Verify BFD is enabled, in the up state and registered with BGP neighbor:
	
	Below we can see that BFD is up and passing traffic.  The *NumRxPackets* and *NumTxPackets* counters show that we are sending and receiving BFD hello packets. 
	*RegisteredProtocols* is BGP, as well as the *SessionState* being in the **up** states. 

	::
		>>> print json.dumps(FlexSwitch("10.1.10.245", 8080).getAllBfdSessionStates(),indent=4)
		[
			{
				"Object": {
					"RegisteredProtocols": "bgp, ",  <-------------
					"DesiredMinTxInterval": "250000(us)", 
					"SessionId": 701, 
					"ParamName": "BFD_Session", <-------------
					"DemandMode": false, 
					"DetectionMultiplier": 3, 
					"SentAuthSeq": 0, 
					"LocalDiscriminator": 701, 
					"SessionState": "up", <-------------
					"AuthSeqKnown": false, 
					"PerLinkSession": false, 
					"IfName": "", 
					"ConfigObj": null, 
					"RequiredMinRxInterval": "250000(us)", 
					"AuthType": "", 
					"RemoteDiscriminator": 1090519237, 
					"RemoteSessionState": "up", 
					"NumTxPackets": 747461, <-------------
					"InterfaceSpecific": false, 
					"NumRxPackets": 908113, <-------------
					"RemoteDemandMode": false, 
					"LocalMacAddr": "", 
					"RemoteMinRxInterval": "250000(us)", 
					"IpAddr": "1.1.1.1", <-------------
					"RemoteMacAddr": "", 
					"LocalDiagType": "None", 
					"IfIndex": 47, 
					"ReceivedAuthSeq": 0
				}, 
				"ObjectId": ""
			},
		]
	
	For the associated BGP neighbor, we can see that the *BfdNeighborState* is UP and this BGP neighbor *SessionState* in Established (state 6) is up:

	::
	
		>>> print json.dumps(FlexSwitch("10.1.10.245", 8080).getAllBGPNeighborStates(),indent=4)
		[
			  {
					"Object": {
						"RouteReflectorClient": false, 
						"MultiHopTTL": 0, 
						"BfdNeighborState": "up", <--------------
						"LocalAS": 420000006, 
						"KeepaliveTime": 60, 
						"AddPathsRx": false, 
						"UpdateSource": "", 
						"PeerGroup": "Group1", 
						"PeerType": 0, 
						"MaxPrefixesRestartTimer": 0, 
						"Description": "", 
						"TotalPrefixes": 0, 
						"MultiHopEnable": false, 
						"SessionState": 6, <--------------
						"PeerAS": 420000005, 
						"RouteReflectorClusterId": 0, 
						"MaxPrefixesDisconnect": false, 
						"Queues": {
							"Input": 0, 
							"Output": 0
						}, 
						"Messages": {
							"Received": {
								"Notification": 0, 
								"Update": 5
							}, 
							"Sent": {
								"Notification": 0, 
								"Update": 5
							}
						}, 
						"AddPathsMaxTx": 0, 
						"NeighborAddress": "1.1.1.1", 
						"MaxPrefixes": 0, 
						"MaxPrefixesThresholdPct": 80, 
						"AuthPassword": "", 
						"IfIndex": 0, 
						"HoldTime": 180, 
						"ConnectRetryTime": 60
					}, 
					"ObjectId": "3861ec9a-188f-44f2-4e49-db60267c600b"
				}
			]

		In the BGP neighbor configuration, we can see the *BfdSessionParam* tied to this neighbor is BFD_Session:
		::

			[		
				{
					"Object": {
						"BfdEnable": true, 
						"RouteReflectorClient": false, 
						"MultiHopTTL": 0, 
						"LocalAS": 420000006, 
						"KeepaliveTime": 60, 
						"AddPathsRx": false, 
						"UpdateSource": "", 
						"PeerGroup": "Group1", 
						"MaxPrefixesRestartTimer": 0, 
						"Description": "", 
						"MultiHopEnable": false, 
						"AuthPassword": "", 
						"RouteReflectorClusterId": 0, 
						"MaxPrefixesDisconnect": false, 
						"PeerAS": 420000005, 
						"AddPathsMaxTx": 0, 
						"NeighborAddress": "1.1.1.1", 
						"MaxPrefixes": 0, 
						"MaxPrefixesThresholdPct": 80, 
						"HoldTime": 180, 
						"IfIndex": 0, 
						"BfdSessionParam": "BFD_Session", <--------------
						"ConnectRetryTime": 60
					}, 
					"ObjectId": "3861ec9a-188f-44f2-4e49-db60267c600b"
				}
			]			


Enabling MultiPath
^^^^^^^^^^^^^^^^^^
In order for BGP to be configured for Equal Cost Multi Path, or ECMP you must to enable BGP multipath.  This allows the BGP daemon to enable selection of routes that are deemed equal cost via the BGP path selection algorithm, as specified in RFC 4271.

Once Multipath is enabled only the following path variables need to be equal:

	- Weight
	- Local-Preference
	- AS-PATH Length
	- Origin

Keep in mind, that with BGP multipath enabled ONLY the selected best path for that prefix is advertised to neighbors. 


.. Note:: When utilizing BGP add-path, each add-path NLRI is considered separately for BGP Path Selection algorithm as if they are separate prefixes.  This means that ECMP/Multipath is considered differently for each add-path NLRI.  Each add-path NLRI is advertised to add-path neighbors, even if prefix is the same.  For non add-path neighbors only the best BGP path is advertised. 


Multi-path is enabled in the BGP Global object and can be enabled for IBGP routes and  EBGP routes separately.   FlexSwitch supports up to 32-way ECMP for BGP. 

.. Note:: EBGP and IBGP routes will only be compared for ECMP, if both are enabled. 

Configuring with Rest API 
"""""""""""""""""""""""""
**COMMAND**

Update BGP global
::

	curl -X PATCH --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ASNum":<*AS Number*>,"RouterId":"<*IP Addr*>","UseMultiplePaths":<*true/false*>,"EBGPMaxPaths":<*Number of Paths*>,"IBGPMaxPaths":<*Number of Paths*>}' 'http://<*your-switchip*>:8080/public/v1/config/BGPGlobal'
	
On BGP global creation
::

	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ASNum":<*AS Number*>,"RouterId":"<*IP Addr*>","UseMultiplePaths":<*true/false*>,"EBGPMaxPaths":<*Number of Paths*>,"IBGPMaxPaths":<*Number of Paths*>}' 'http://<*your-switchip*>:8080/public/v1/config/BGPGlobal'
	
.. Note:: This command is a variable being enabled part of BGPGlobal object. See :ref:`bgp-global-rest` for more details. 

**OPTIONS:**

+----------------------+------------+---------------------------------------------+----------+----------+
| Variables            | Type       |  Description                                | Required |  Default |     
+======================+============+=============================================+==========+==========+   
| ASNum                | integer    | Local AS for BGP global config              |    Yes   |   None   |
+----------------------+------------+---------------------------------------------+----------+----------+
| RouterId             | string     | Router id for BGP global config             |    Yes   |   None   |
+----------------------+------------+---------------------------------------------+----------+----------+
| UseMultiplePaths     | boolean    | Enable/disable ECMP for BGP                 |    no    |  false   |
+----------------------+------------+---------------------------------------------+----------+----------+
| EBGPMaxPaths         | integer    | Max ECMP paths from External BGP neighbors  |    no    |     0    |
+----------------------+------------+---------------------------------------------+----------+----------+
| IBGPMaxPaths         | integer    | Max ECMP paths from Internal BGP neighbors  |    no    |     0    |
+----------------------+------------+---------------------------------------------+----------+----------+

**EXAMPLE**

Below is an example on how to enable BGP multipath for both IBGP and EBGP routes:

1. Configure Max Paths to desired paths for EBGP and IBGP and enable multipath:
	a. In this example *EBGPMaxPaths* and *IBGPMaxPaths* are set to 32
	b. Updating *UseMultiplePaths* to true to enable multipath

	::
	
		curl -X PATCH --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ASNum":65535,"RouterId":"1.1.1.1","UseMultiplePaths":true,"EBGPMaxPaths":32,"IBGPMaxPaths":32}' 'http://10.1.10.243:8080/public/v1/config/BGPGlobal'
		{"ObjectId":"7f2c589d-3dea-4356-75be-91c7c2de18cb","Error":""}

2. Validate in configuration and state objects that BGP Multipath is enabled:

	**Configuration:**
	::
			
		curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.243:8080/public/v1/config/BGPGlobals' | python -m json.tool
		  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
										 Dload  Upload   Total   Spent    Left  Speed
		100   344  100   344    0     0  62228      0 --:--:-- --:--:-- --:--:-- 68800
		{
			"CurrentMarker": 0,
			"MoreExist": false,
			"NextMarker": 0,
			"ObjCount": 1,
			"Objects": [
				{
					"Object": {
						"ASNum": 420000005,
						"EBGPAllowMultipleAS": true,
						"EBGPMaxPaths": 32,
						"IBGPMaxPaths": 32,
						"Redistribution": [],
						"RouterId": "1.1.1.1",
						"UseMultiplePaths": true
					},
					"ObjectId": "7f2c589d-3dea-4356-75be-91c7c2de18cb"
				}
			]
		}		

	**State:**
	::

		curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.243:8080/public/v1/state/BGPGlobals' | python -m json.tool
		  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
										 Dload  Upload   Total   Spent    Left  Speed
		100   185  100   185    0     0  28664      0 --:--:-- --:--:-- --:--:-- 30833
		{
			"CurrentMarker": 0,
			"MoreExist": false,
			"NextMarker": 0,
			"ObjCount": 1,
			"Objects": [
				{
					"Object": {
						"AS": 65535,
						"EBGPAllowMultipleAS": true,
						"EBGPMaxPaths": 32,
						"IBGPMaxPaths": 32,
						"RouterId": "1.1.1.1",
						"TotalPaths": 0,
						"TotalPrefixes": 0,
						"UseMultiplePaths": true
					},
					"ObjectId": ""
				}
			]
		}
		
.. Note:: BGPGlobal has already been configured with AS number of 65535 and RouterId of 1.1.1.1

Configuring with Python SDK
"""""""""""""""""""""""""""
**COMMAND**

Update BGP global:

::

	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).updateBGPGlobal(ASNum=<*AS Number*>,
									RouterId=<*IP Addr*>,
									UseMultiplePaths=<*true/false*>,
									EBGPMaxPaths=<*Number of Paths*>,
									IBGPMaxPaths=<*Number of Paths*>,)
	
On BGP global creation:

::

	>>> FlexSwitch("<*Switch IP*>", <*TCP port*>).createBGPGlobal(ASNum=<*AS Number*>,
									RouterId=<*IP Addr*>,
									UseMultiplePaths=<*true/false*>,
									EBGPMaxPaths=<*Number of Paths*>,
									IBGPMaxPaths=<*Number of Paths*>,)	
	
.. Note:: This command is a variable being enabled part of BGPGlobal object. See :ref:`bgp-global-python` for more details.
 
**OPTIONS:**

+-------------------+----------------------+------------+---------------------------------------------+----------+----------+
| Python Method     | Variables            | Type       |  Description                                | Required |  Default |     
+===================+======================+============+=============================================+==========+==========+   
| createBGPGlobal   | ASNum                | integer    | Local AS for BGP global config              |    Yes   |   None   |
|        OR         +----------------------+------------+---------------------------------------------+----------+----------+
| updateBGPGlobal   | RouterId             | string     | Router id for BGP global config             |    Yes   |   None   |
|                   +----------------------+------------+---------------------------------------------+----------+----------+
|                   | UseMultiplePaths     | boolean    | Enable/disable ECMP for BGP                 |    no    |  False   |
|                   +----------------------+------------+---------------------------------------------+----------+----------+
|                   | EBGPMaxPaths         | integer    | Max ECMP paths from External BGP neighbors  |    no    |     0    |
|                   +----------------------+------------+---------------------------------------------+----------+----------+
|                   | IBGPMaxPaths         | integer    | Max ECMP paths from Internal BGP neighbors  |    no    |     0    |
+-------------------+----------------------+------------+---------------------------------------------+----------+----------+


Redistribution
^^^^^^^^^^^^^^
To redistribute routes to BGP neighbors, you must enable redistribution in BGP. You can redistribute connected, static and routes learned via other protocols to BGP neighbors. Redistribution is enabled by creating policies and setting the policy in the BGP Global object.

   Configuring with Rest API 
   """""""""""""""""""""""""
A policy has to be configured first to enable redistribution.

.. Note:: See :ref:`routing-policies` to configure the policies.

Update BGP global
::

    curl -X PATCH --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ASNum":<*AS Number*>,"RouterId":"<*IP Addr*>","Redistribution":[{"Sources":"<*CONNECTED/STATIC/OSPF*>","Policy":"<*Policy Name*>"}]}' 'http://<*your-switchip*>:8080/public/v1/config/BGPGlobal'
    
On BGP global creation
::

    curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ASNum":<*AS Number*>,"RouterId":"<*IP Addr*>","Redistribution":[{"Sources":"<*CONNECTED/STATIC/OSPF*>","Policy":"<*Policy Name*>"}]}' 'http://<*your-switchip*>:8080/public/v1/config/BGPGlobal'
    
.. Note:: This command is a variable being enabled part of BGPGlobal object. See :ref:`bgp-global-rest` for more details. 

**OPTIONS:**

+----------------------+----------------------+---------------------------------------------+----------+----------+
| Variables            | Type                 |  Description                                | Required |  Default |     
+======================+======================+=============================================+==========+==========+   
| ASNum                | integer              | Local AS for BGP global config              |    Yes   |   None   |
+----------------------+----------------------+---------------------------------------------+----------+----------+
| RouterId             | string               | Router id for BGP global config             |    Yes   |   None   |
+----------------------+----------------------+---------------------------------------------+----------+----------+
| Redistribution       | [SourcePolicyList]   | Redistribution policies                     |    no    |    []    |
+----------------------+----------------------+---------------------------------------------+----------+----------+

**EXAMPLE**

Below is an example on how to enable BGP redistribution:

1. Configure policies and enable redistribution:
    a. Configure the policy
.. Note:: See :ref:`routing-policies` to configure the policies.

    b. Updating *Redistribution* to enable redistribution

    ::
    
        curl -X PATCH --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"ASNum":65535,"RouterId":"1.1.1.1","Redistribution":[{"Sources":"CONNECTED,STATIC","Policy":"Policy1"},{"Sources":"OSPF","Policy":"Policy2"}]}' 'http://10.1.10.243:8080/public/v1/config/BGPGlobal'
        {"ObjectId":"7f2c589d-3dea-4356-75be-91c7c2de18cb","Error":""}

2. Validate in configuration object that BGP Redistribution is enabled:

    **Configuration:**
    ::
            
        curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.243:8080/public/v1/config/BGPGlobals' | python -m json.tool
          % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                         Dload  Upload   Total   Spent    Left  Speed
        100   344  100   344    0     0  62228      0 --:--:-- --:--:-- --:--:-- 68800
        {
            "CurrentMarker": 0,
            "MoreExist": false,
            "NextMarker": 0,
            "ObjCount": 1,
            "Objects": [
                {
                    "Object": {
                        "ASNum": 65535,
                        "EBGPAllowMultipleAS": false,
                        "EBGPMaxPaths": 0,
                        "IBGPMaxPaths": 0,
                        "RouterId": "1.1.1.1",
                        "UseMultiplePaths": false,
                        "Redistribution": [{"Sources":"CONNECTED,STATIC","Policy":"Policy1"},{"Sources":"OSPF","Policy":"Policy2"}]
                    },
                    "ObjectId": "7f2c589d-3dea-4356-75be-91c7c2de18cb"
                }
            ]
        }       

.. Note:: BGPGlobal has already been configured with AS number of 65535 and RouterId of 1.1.1.1

   Configuring with Python SDK
   """""""""""""""""""""""""""
**COMMAND**

Update BGP global:

::

    >>> FlexSwitch("<*Switch IP*>", <*TCP port*>).updateBGPGlobal(ASNum=<*AS Number*>,
                                    RouterId=<*IP Addr*>,
                                    Redistribution=[{"Sources":"<*CONNECTED/STATIC/OSPF*>","Policy":"<*Policy Name*>"}],)
    
On BGP global creation:

::

    >>> FlexSwitch("<*Switch IP*>", <*TCP port*>).createBGPGlobal(ASNum=<*AS Number*>,
                                    RouterId=<*IP Addr*>,
                                    Redistribution=[{"Sources":"<*CONNECTED/STATIC/OSPF*>","Policy":"<*Policy Name*>"}],)  
    
.. Note:: This command is a variable being enabled part of BGPGlobal object. See :ref:`bgp-global-python` for more details.
 
**OPTIONS:**

+-------------------+----------------------+---------------------+---------------------------------------------+----------+----------+
| Python Method     | Variables            | Type                |  Description                                | Required |  Default |     
+===================+======================+=====================+=============================================+==========+==========+   
| createBGPGlobal   | ASNum                | integer             | Local AS for BGP global config              |    Yes   |   None   |
|        OR         +----------------------+---------------------+---------------------------------------------+----------+----------+
| updateBGPGlobal   | RouterId             | string              | Router id for BGP global config             |    Yes   |   None   |
|                   +----------------------+---------------------+---------------------------------------------+----------+----------+
|                   | Redistribution       | [SourcePolicyList]  | Redistribution policies                     |    no    |    []    |
+-------------------+----------------------+---------------------+---------------------------------------------+----------+----------+

**EXAMPLE**

Below is an example on how to enable BGP redistribution:

1. Configure policies and enable redistribution:
    a. Configure the policy
.. Note:: See :ref:`routing-policies` to configure the policies.

    b. Updating *Redistribution* to enable redistribution

    ::
    
    >>> FlexSwitch("10.1.10.245", 8080).updateBGPGlobal(ASNum=65535, RouterId="1.1.1.1", Redistribution=[{'Sources':'','Policy':'Policy1'}],)  

   Route Reflectors
   ^^^^^^^^^^^^^^^^
   Configuring with Rest API 
   """""""""""""""""""""""""""
   Configuring with Python SDK
   """""""""""""""""""""""""""
   Add Path
   ^^^^^^^^
   Configuring with Rest API 
   """"""""""""""""""""""""""""
   Configuring with Python SDK
   """"""""""""""""""""""""""""

----------------------

Configuring DHCP Relay
-----------------------

DHCP relay agent is a mechanism that acts as a proxy service for a DHCP server on a network. Since DHCP discover packets are broadcast, they can not reach a DHCP server, 
that is off subnet. In order to get around this limitation DHCP relay, will ingest a DHCP DISCOVER broadcast frames and unicast forward them
to a specified DHCP servers and relay the reply to the host attempting IP address assignment. 

DHCP Relay Operation
^^^^^^^^^^^^^^^^^^^^

Below are the FlexSwitch DHCP Relay agent states for this transaction:

	- Receive DISCOVER Packet
	- Relay client Packet to all servers (configured) updating Relay Agent Information in Dhcp Options
	- Receive OFFER Packet
	- Send Unicast OFFER to Client (if configured) else Broadcast OFFER Packet
	- Receive REQUEST Packet
	- Relay REQUEST Packet to Server
	- Receive ACK Packet
	- Relay ACK Packet to Client


Enabling DHCP relay
^^^^^^^^^^^^^^^^^^^
Configuring with Rest API 
"""""""""""""""""""""""""

Enable Globally
***************

**COMMAND**
::
	
	curl -H "Content-Type: application/json" -d '{"DhcpRelay": "dr", "Enable": true }' -X POST http://10.1.10.244:8080/public/v1/config/DhcpRelayGlobal


**OPTIONS**

+----------------------+------------+---------------------------------------------+----------+----------+
| Variables            | Type       |  Description                                | Required |  Default |
+======================+============+=============================================+==========+==========+
| DhcpRelay            | string     | Key used to enable dhcp relay on a switch   |    Yes   |   None   |
|----------------------+------------+---------------------------------------------+----------+----------+
| Enable               | bool       | Dhcp Relay enabled/disabled globally        |    Yes   |   None   |
+----------------------+------------+---------------------------------------------+----------+----------+

Enable On Interface
********************

**COMMAND**
::
	curl -H "Content-Type: application/json" -d '{"IfIndex": 33554442 , "Enable": true , "ServerIp": ["90.0.1.2", "80.0.1.2"] }' -X POST http://10.1.10.244:8080/public/v1/config/DhcpRelayIntf

**OPTIONS**

+----------------------+------------+---------------------------------------------+----------+----------+
| Variables            | Type       |  Description                                | Required |  Default |
+======================+============+=============================================+==========+==========+
| IfIndex              | integer    | Key used to enable dhcp relay on a intf     |    Yes   |   None   |
|----------------------+------------+---------------------------------------------+----------+----------+
| Enable               | bool       | Dhcp Relay enabled/disabled on interface    |    Yes   |   None   |
|----------------------+------------+---------------------------------------------+----------+----------+
| ServerIp             | list       | list of server ip which relay agent will use|    Yes   |   None   |
+----------------------+------------+---------------------------------------------+----------+----------+


**EXAMPLE**


Configuring with Python SDK
"""""""""""""""""""""""""""

Enable Globally
***************

**COMMAND**
::

>>> FlexSwitch ("<*Switch Ip*>", <*TCP Port*>).createDhcpRelayGlobal(DhcpRelay, Enable)

**OPTIONS**

+-----------------------+----------------------+------------+---------------------------------------------+----------+----------+
| Python Method         | Variables            | Type       |  Description                                | Required |  Default |
+=======================+======================+============+=============================================+==========+==========+
| createDhcpRelayGlobal | DhcpRelay            | string     | Key used to enable dhcp relay on a switch   |    Yes   |   None   |
|                       +----------------------+------------+---------------------------------------------+----------+----------+
|                       | Enable               | bool       | Dhcp Relay enabled/disabled globally        |    Yes   |   None   |
+-----------------------+----------------------+------------+---------------------------------------------+----------+----------+

Enable On Interface
********************

**COMMAND**
::

>>> FlexSwitch ("<*Switch Ip*>", <*TCP Port*>).createDhcpRelayIntf(IfIndex, Enable, ServerIp):

**OPTIONS**

+-----------------------+----------------------+------------+---------------------------------------------+----------+----------+
|    Python Method      | Variables            | Type       |  Description                                | Required |  Default |
+-----------------------+======================+============+=============================================+==========+==========+
|  createDhcpRelayIntf  | IfIndex              | integer    | Interface where dhcp relay needs config     |    Yes   |   None   |
|                       +----------------------+------------+---------------------------------------------+----------+----------+
|                       | Enable               | bool       | Dhcp Relay enabled/disabled on interface    |    Yes   |   None   |
|                       +----------------------+------------+---------------------------------------------+----------+----------+
|                       | ServerIp             | list       | list of server ip which relay agent will use|    Yes   |   None   |
+-----------------------+----------------------+------------+---------------------------------------------+----------+----------+

**EXAMPLE**

>>> from flexswitchV2 import FlexSwitch
>>> FlexSwitch ("192.168.10.1", 8080).createDhcpRelayGlobal(DhcpRelay="dr", Enable=true)
>>> FlexSwitch ("192.168.10.1", 8080).createDhcpRelayIntf(IfIndex=355413, Enable=true, ServerIP=['90.0.1.2', '80.0.1.2'])

Configuring LLDP
-----------------
Link Layer Discovery Protocol is a mechanism used by network devices for advertising their identity, capabilities and neighbors on a LAN. LLDP Information is send from each of the interfaces at fixed interval, in the form of Ethernet Frame. Each Frame contains below Information
    - Mandatory TLV's
    - Optional TLV's

Mandatory TLV's include:
    - Chassis ID
    - Port ID
    - TTL
Optional TLV's include:
    - Management Address
    - System Description
    - System Hostname
    - System Version
    - Capabilites

Configuring with Rest API 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    LLDP by default according to IEEE documentation is enabled on all Interfaces which are in Admin UP state. However, lldp per port can be enabled/disabled using following command:
 
**COMMAND:**
::
    curl -H "Content-Type: application/json" -d '{"IfIndex":46, "Enable": false }' -X POST http://<*your switch_ip*>:8080/public/v1/config/LLDPIntf
    curl -X PATCH -H "Content-Type: application/json" -d '{"IfIndex":46, "Enable": true }'  http://<*your switch_ip*>/public/v1/config/LLDPIntf/<*uuid*>

**OPTIONS:**

+----------------------+------------+---------------------------------------------+----------+----------+
| Variables            | Type       |  Description                                | Required |  Default |
+======================+============+=============================================+==========+==========+
| IfIndex              | integer    | Interface where LLDP needs to be changed    |    Yes   |   None   |
|----------------------+------------+---------------------------------------------+----------+----------+
| Enable               | bool       | LLDP enabled/disabled                       |    Yes   |   None   |
+----------------------+------------+---------------------------------------------+----------+----------+

Configuring with Python SDK
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**COMMAND**
::

>>> FlexSwitch ("<*Switch Ip*>", <*TCP Port*>).updateLLDPIntf(IfIndex, Enable):

**OPTIONS:**

+----------------------+----------------------+------------+---------------------------------------------+----------+----------+
| Python Method        | Variables            | Type       |  Description                                | Required |  Default |
+======================+======================+============+=============================================+==========+==========+
| createLLDPIntf       | IfIndex              | integer    | Interface where LLDP needs to be changed    |    Yes   |   None   |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | Enable               | bool       | LLDP enabled/disabled                       |    Yes   |   None   |
+----------------------+----------------------+------------+---------------------------------------------+----------+----------+

**EXAMPLE:**

>>> from flexswitchV2 import FlexSwitch
>>> FlexSwitch ("192.168.10.1", 8080).createLLDPIntf(IfIndex=355414, Enable=false):


Configuring LoopBacks
----------------------

LoopBack is configured using the LogicalIntf object.

Configuring with Rest API 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**COMMAND**
::

    curl -H "Content-Type: application/json" -d '{"Name":"lo1", "Type":"Loopback"}' http://localhost:8080/public/v1/config/LogicalIntf

**OPTIONS:**

+----------------------+------------+---------------------------------------------+----------+----------+
| Variables            | Type       |  Description                                | Required |  Default |     
+======================+============+=============================================+==========+==========+   
| Name                 | string     | Name of the logical interface               |    Yes   |   None   |
+----------------------+------------+---------------------------------------------+----------+----------+
| Type                 | string     | Type of the logical interface               |    Yes   | Loopback |
+----------------------+------------+---------------------------------------------+----------+----------+

**EXAMPLE**
::

    curl -H "Content-Type: application/json" -d '{"Name":"lo1", "Type":"Loopback"}' http://localhost:8080/public/v1/config/LogicalIntf
    curl -H "Content-Type: application/json" -d '{"Name":"lo2", "Type":"Loopback"}' http://localhost:8080/public/v1/config/LogicalIntf
    curl -H "Content-Type: application/json" -d '{"Name":"lo3", "Type":"Loopback"}' http://localhost:8080/public/v1/config/LogicalIntf
	
    curl -H "Content-Type: application/json" 'http://localhost:8080/public/v1/config/LogicalIntfs' | python -m json.tool
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
    100   359  100   359    0     0  99528      0 --:--:-- --:--:-- --:--:--  116k
    {
        "CurrentMarker": 0,
        "MoreExist": false,
        "NextMarker": 0,
        "ObjCount": 3,
        "Objects": [
            {
                "Object": {
                    "Name": "lo3",
                    "Type": "Loopback"
                },
                "ObjectId": "4b0ce45d-455a-4767-6250-470339d3bb40"
            },
            {
                "Object": {
                    "Name": "lo2",
                    "Type": "Loopback"
                },
                "ObjectId": "c154f5c2-d982-48f0-585b-edc346e74f54"
            },
            {
                "Object": {
                    "Name": "lo1",
                    "Type": "Loopback"
                },
                "ObjectId": "777a93ee-f1f0-4117-48a3-678dfee2a194"
            }
        ]
    }


Configuring with Python SDK
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Configuring Logging
---------------------
System 
^^^^^^^
System level logging is enabled by default. It can be disabled or re-enabled. Daemon level logging is set to "info" by default.

Configuring with Rest API 
""""""""""""""""""""""""""""
**COMMAND:**
::
    curl -X PATCH -H "Content-Type: application/json" -d '{"Vrf":"default", "Logging": "off" }'  http://<*your switch_ip*>/public/v1/config/SystemLogging

Configuring with Python SDK
""""""""""""""""""""""""""""

+----------------------+----------------------+------------+---------------------------------------------+----------+----------+
| Python Method        | Variables            | Type       |  Description                                | Required |  Default |
+======================+======================+============+=============================================+==========+==========+
| updateSystemLogging  | Vrf                  | string     | VRF name where logging will be changed      |    Yes   | None     |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | Logging              | string     | Logging on/off                              |    no    |   on     |
+----------------------+----------------------+------------+---------------------------------------------+----------+----------+

**EXAMPLE:**
>>> from flexswitchV2 import FlexSwitch
>>> FlexSwitch ("192.168.10.1", 8080).updateSystemLogging(Vrf="default", Logging="off"):


Daemon
^^^^^^^
Configuring with Rest API 
""""""""""""""""""""""""""""
**COMMAND:**
::
    curl -X PATCH -H "Content-Type: application/json" -d '{"Module":"bfdd", "Level": "debug" }'  http://<*your switch_ip*>/public/v1/config/ComponentLogging

Configuring with Python SDK
""""""""""""""""""""""""""""

+-------------------------+----------------------+------------+-----------------------+----------+----------+
| Python Method           | Variables            | Type       |  Description          | Required |  Default |
+=========================+======================+============+=======================+==========+==========+
| updateComponentLogging  | Module               | string     | Daemon name           |    Yes   | None     |
|                         +----------------------+------------+-----------------------+----------+----------+
|                         | Level                | string     | Logging level         |    no    |   info   |
+-------------------------+----------------------+------------+-----------------------+----------+----------+

Logging level can be - crit/err/warn/alert/emerg/notice/info/debug/trace/off

**EXAMPLE:**
>>> from flexswitchV2 import FlexSwitch
>>> FlexSwitch ("192.168.10.1", 8080).updateComponentLogging(Module="bfdd", Level="debug"):




Configuring OSPF
------------------


OspfAreaEntry
^^^^^^^^^^^^^

It will configure OSPF area specific params.
If ospfArea Entry is not added by default area 0.0.0.0 is created.

**AreaId** = Unique area id . Used as key.

::


        curl -H "Content-Type: application/json" -d '{"AreaId": "0.0.0.2", "AuthType":0, "ImportAsExtern":1, "AreaSummary":1, "AreaNssaTranslatorRole":2}' http://localhost:8080/public/v1/config/OspfAreaEntry


OspfIfEntry
^^^^^^^^^^^

IfEntry configures OSPF interface.

**IfIpAddress** = Ip address of the interface


**AddressLessIf** = Ip index . Used to configure unnumbered P2P links.


The default IfRtrDeadInterval is 40 s whereas HelloInterval is 10s.

::


    configure Ospf Interface with ip address 40.1.1.1 and area id 0.0.0.2
    curl -H "Content-Type: application/json" -d '{"IfIpAddress": "41.0.0.5", "AddressLessIf":0, "IfAreaId":"0.0.0.0", "IfType":"Broadcast", "IfAdminStat":1, "IfRtrPriority":1, "IfTransitDelay":1, "IfRetransInterval":5, "IfHelloInterval":10, "IfRtrDeadInterval":40, "IfPollInterval":120, "IfAuthKey":"0.0.0.0.0.0.0.0", "IfAuthType":0}' http://localhost:8080/public/v1/config/OspfIfEntry

OspfGlobal
^^^^^^^^^^
This object will enable the global ospf feature. Unless ospf global is enabled  ,OspfAreaEntry wont take effect.

**RouterId** = OSPF router id.

**ASBdrRtrStatus** = set to true if router acts as ASBR.

**TOSSupport** = OSPF TOS support. (Currently not supported.)

**RestartSupport** = If the process restart is supported.

::


    curl -H "Content-Type: application/json" -d '{"RouterId": "10.1.1.1", "AdminStat":1, "ASBdrRtrStatus":true, "TOSSupport":true,  "RestartSupport":1, "RestartInterval":10}' http://localhost:8080/public/v1/config/OspfGlobal


Show commands 
^^^^^^^^^^^^^

- Check Ospf Neighbors

::


    curl -H "Accept: application/json" "http://localhost:8080/public/v1/state/OspfNbrEntrys?CurrentMarker=0&NextMarker=0&Count=10" | python -m json.tool

    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
    100   367  100   367    0     0  58272      0 --:--:-- --:--:-- --:--:-- 61166
   {
    "CurrentMarker": 0,
    "MoreExist": false,
    "NextMarker": 0,
    "ObjCount": 1,
    "Objects": [
        {
            "Object": {
                "NbmaNbrPermanence": 0,
                "NbrAddressLessIndex": 0,
                "NbrEvents": 4,
                "NbrHelloSuppressed": false,
                "NbrIpAddr": "51.1.1.6",
                "NbrLsRetransQLen": 0,
                "NbrOptions": 0,
                "NbrRestartHelperAge": 0,
                "NbrRestartHelperExitReason": 0,
                "NbrRestartHelperStatus": 0,
                "NbrRtrId": "10.1.1.3",
                "NbrState": 7
            },
            "ObjectId": ""
        }
    ]
 }

- check LSA database

::

    curl -H "Accept: application/json" "http://localhost:8080/public/v1/state/OspfLsdbEntrys" | python -m json.tool


Configuring Routing Policies
----------------------------

.. _routing-policies:
Configuring Policy Condition with Rest API
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**COMMAND:**
::

     curl -H "Content-Type: application/json" -d '{"Name":"Match40", "ConditionType":"MatchDstIpPrefix", "IpPrefix":"40.1.3.0/24", "MaskLengthRange":"exact"}' http://localhost:8080/public/v1/config/PolicyCondition

	

**OPTIONS:**

+-----------------+-------------+----------------------------------------------+----------+----------+
| Variables       | Type        |  Description                                 | Required |  Default |   
+=================+=============+==============================================+==========+==========+ 
|Name             | string      | Name of the policy condition                 |   Yes    |    N/A   |          
+-----------------+-------------+----------------------------------------------+----------+----------+
|ConditionType    | string      | Condition type:                              |          |          |
|                 |             |              MatchProtocol                   |          |          |
|                 |             |                     OR                       |   Yes    |    N/A   |
|                 |             |              MatchDstIpPrefix                |          |          |
+-----------------+-------------+----------------------------------------------+----------+----------+
|                 |             | If MatchProtocol is ConditionType, this      |          |          |
| Protocol        | String      | specifies the Protocol to be matched;        |    No    |   None   |
|                 |             | I.E. OSPF, BGP, STATIC                       |          |          |
+-----------------+-------------+----------------------------------------------+----------+----------+ 
|                 |             | Prefix to match on when the condition        |          |          |
| IpPrefix        | String      | type is MatchDstIpPrefix/MatchSrcIpPrefix    |    No    |   None   |
+-----------------+-------------+----------------------------------------------+----------+----------+ 
|                 |             | Used along with IpPrefix and specifies       |          |          |
| MaskLengthRange | String      | whether to match the exact prefix or a range |    No    |   None   |
+-----------------+-------------+----------------------------------------------+----------+----------+ 

**EXAMPLE:**
::
	
      //condition to match on a network
      curl -H "Content-Type: application/json" -d '{"Name":"Match40", "ConditionType":"MatchDstIpPrefix", "IpPrefix":"40.1.3.0/24", "MaskLengthRange":"exact"}' http://localhost:8080/public/v1/config/PolicyCondition
      {"ObjectId":"a8c98e74-eeb7-4580-6ff9-23b3b48d76f9","Error":""}

      curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:8080/public/v1/config/PolicyConditions | python -m json.tool
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
      100   257  100   257    0     0  42138      0 --:--:-- --:--:-- --:--:-- 51400
      {
          "CurrentMarker": 0,
           "MoreExist": false,
           "NextMarker": 0,
           "ObjCount": 1,
           "Objects": [
               {
                   "Object": {
                       "ConditionType": "MatchDstIpPrefix",
                       "IpPrefix": "40.1.3.0/24",
                       "MaskLengthRange": "exact",
                       "Name": "Match40",
                       "Protocol": ""
                   },
                   "ObjectId": "a8c98e74-eeb7-4580-6ff9-23b3b48d76f9"
               }
           ]
       }
	
Configuring Policy Statement with Rest API
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**COMMAND:**
::

    curl -H "Content-Type: application/json" -d '{"Name":"Stmt1", "MatchConditions":"all", "Conditions":["Match40"], "Action":"permit"}' http://localhost:8080/public/v1/config/PolicyStmt


**OPTIONS:**

+----------------+-------------+------------------------------------------------+----------+----------+
| Variables      | Type        |  Description                                   | Required |  Default |   
+================+=============+================================================+==========+==========+ 
|Name            | string      | Name of the policy Statement                   |   Yes    |    N/A   |          
+----------------+-------------+------------------------------------------------+----------+----------+
|MatchConditions | string      | Specifies whether to match all or any          |   Yes    |    "all" |
|                |             | of the conditions                              |          |          |
+----------------+-------------+------------------------------------------------+----------+----------+
| Conditions     | [strings]   | list of conditions used to evaluate this       |   Yes    |          |
|                |             | statement                                      |          |          |
+----------------+-------------+------------------------------------------------+----------+----------+ 
| Action         | String      | Action on a successful evaluation of statement |    No    |    "deny"|
+----------------+-------------+------------------------------------------------+----------+----------+ 


**EXAMPLE:**
::
	
      curl -H "Content-Type: application/json" -d '{"Name":"Stmt1", "MatchConditions":"all", "Conditions":["Match40"], "Action":"permit"}' http://localhost:8080/public/v1/config/PolicyStmt
      {"ObjectId":"e73825a0-b307-4498-76ad-5c8552c866e3","Error":""}
	
      curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:8080/public/v1/config/PolicyStmts | python -m json.tool
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
      100   222  100   222    0     0  66486      0 --:--:-- --:--:-- --:--:-- 74000
      {
          "CurrentMarker": 0,
          "MoreExist": false,
          "NextMarker": 0,
          "ObjCount": 1,
          "Objects": [
              {
                "Object": {
                    "Action": "permit",
                    "Conditions": [
                        "Match40"
                    ],
                    "MatchConditions": "all",
                    "Name": "Stmt1"
                },
                "ObjectId": "e73825a0-b307-4498-76ad-5c8552c866e3"
             }
        ]
    }

	
Configuring Policy Definition with Rest API
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**COMMAND:**
::
	
     curl -H "Content-Type: application/json" -d '{"Name":"Policy1", "Priority":1,"MatchType":"all", "PolicyType":"ALL", "StatementList":[{"Priority":1,"Statement":"Stmt1"}]}' http://localhost:8080/public/v1/config/PolicyDefinition

	

**OPTIONS:**

+--------------+--------------------------------+---------------------------------------------+----------+----------+
| Variables    | Type                           |  Description                                | Required |  Default |   
+==============+================================+=============================================+==========+==========+ 
|Name          | string                         | Name of the policy definition               |   Yes    |    N/A   |          
+--------------+--------------------------------+---------------------------------------------+----------+----------+
|Priority      | int32                          | Priority of the policy                      |   Yes    |    N/A   |
+--------------+--------------------------------+---------------------------------------------+----------+----------+
|MatchType     | string                         | Specifies if any or all of the statements   |   No     |    "all" |
|              |                                | of the policy needs to be executed          |          |          |
+--------------+--------------------------------+---------------------------------------------+----------+----------+
|              |                                | List of {priority,statement}s specifies     |          |          |
| StatementList| []PolicyDefinitionStmtPriority | statements in the policy and their priority |    No    |          |
+--------------+--------------------------------+---------------------------------------------+----------+----------+ 


**EXAMPLE:**
::
	
      curl -H "Content-Type: application/json" -d '{"Name":"Policy1", "Priority":1,"MatchType":"all", "PolicyType":"ALL", "StatementList":[{"Priority":1,"Statement":"Stmt1"}]}' http://localhost:8080/public/v1/config/PolicyDefinition
      {"ObjectId":"770dde8f-b357-4c38-4e25-8289e507614a","Error":""}

      curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:8080/public/v1/config/PolicyDefinitions | python -m json.tool
       % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
       100   260  100   260    0     0  61743      0 --:--:-- --:--:-- --:--:-- 65000
       {
           "CurrentMarker": 0,
           "MoreExist": false,
           "NextMarker": 0,
           "ObjCount": 1,
           "Objects": [
               {
                   "Object": {
                       "MatchType": "all",
                       "Name": "Policy1",
                       "PolicyType": "ALL",
                       "Priority": 1,
                       "StatementList": [
                       {
                           "Priority": 1,
                           "Statement": "Stmt1"
                       }
                   ]
               },
               "ObjectId": "770dde8f-b357-4c38-4e25-8289e507614a"
            }
        ]
    }


Configuring Routing 
-------------------

Static Routes
^^^^^^^^^^^^^

Configuring with Rest API 
"""""""""""""""""""""""""

Configuring Single Hop Route
****************************

**COMMAND:**
::
	
     curl -H "Content-Type: application/json" -d '{"DestinationNw": "40.1.10.0", "NetworkMask": "255.255.255.0", "Protocol": "STATIC", "NextHop": [{"NextHopIp": "40.1.1.2", "NextHopIntRef":"fpPort1"}]}' http://localhost:8080/public/v1/config/IPv4Route
	

**OPTIONS:**

+--------------+-------------+-------------------------------------------+----------+----------+
| Variables    | Type        |  Description                              | Required |  Default |   
+==============+=============+===========================================+==========+==========+ 
|DestinationNw | string      | IP address of the destination nw          |   Yes    |    N/A   |          
+--------------+-------------+-------------------------------------------+----------+----------+
|Protocol      | string      | Route Protocol type                       |    No    | "STATIC" |
+--------------+-------------+-------------------------------------------+----------+----------+
| NextHop      | NextHopInfo | List of Next hop details:                 |   Yes    |          |
|              +-------------+-------------------------------------------+----------+----------+
|              | string      |            Next Hop IP                    |   Yes    |   N/A    |
|              +-------------+-------------------------------------------+----------+----------+
|              | string      |            Next Hop Interface             |   Yes    |   N/A    |
|              +-------------+-------------------------------------------+----------+----------+
|              | int32       |            Weight of the next hop  (0..31)|    No    |   0      |
+--------------+-------------+-------------------------------------------+----------+----------+ 
| NullRoute    | Boolean     | Specify if this is Null Route             |    No    |  false   |
+--------------+-------------+-------------------------------------------+----------+----------+ 
| Cost         | int32       | Specify the cost of the Route             |    No    |  0       |
+--------------+-------------+-------------------------------------------+----------+----------+ 


**EXAMPLE:**
::
	
	 curl -H "Content-Type: application/json" -d '{"DestinationNw": "40.1.10.0", "NetworkMask": "255.255.255.0", "Protocol": "STATIC", "NextHop": [{"NextHopIp": "40.1.1.2", "NextHopIntRef":"fpPort1"}]}' http://localhost:8080/public/v1/config/IPv4Route
     {"ObjectId":"99181161-6438-40df-7926-a0dd78d5dd29","Error":""}

      curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:8080/public/v1/config/IPv4Routes | python -m json.tool
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
     100   315  100   315    0     0  76382      0 --:--:-- --:--:-- --:--:--  102k
     {
        "CurrentMarker": 0,
        "MoreExist": false,
        "NextMarker": 0,
        "ObjCount": 1,
        "Objects": [
            {
                "Object": {
                    "Cost": 0,
                    "DestinationNw": "40.1.10.0",
                    "NetworkMask": "255.255.255.0",
                    "NextHop": [
                        {
                            "NextHopIntRef": "fpPort1",
                            "NextHopIp": "40.1.1.2",
                            "Weight": 0
                        }
                    ],
                    "NullRoute": false,
                    "Protocol": "STATIC"
                },
                "ObjectId": "99181161-6438-40df-7926-a0dd78d5dd29"
            }
        ]
    }

	
Configuring ECMP Routes
************************

**COMMAND:**
::

    First route:
     
		curl -H "Content-Type: application/json" -d '{"DestinationNw": "40.1.10.0", "NetworkMask": "255.255.255.0", "Protocol": "STATIC", "NextHop": [{"NextHopIp": "40.1.1.2", "NextHopIntRef":"fpPort1"}]}' http://localhost:8080/public/v1/config/IPv4Route
	
	Subsequent next hops add:
	
		curl -X PATCH -H "Content-Type: application/json" -d '{"op":"add", "DestinationNw": "40.1.10.0", "NetworkMask": "255.255.255.0", "NextHop": [{"NextHopIp": "40.1.2.2", "NextHopIntRef":"fpPort2"}]}' http://localhost:8080/public/v1/config/IPv4Route



**EXAMPLE:**
::
	
	 curl -H "Content-Type: application/json" -d '{"DestinationNw": "40.1.10.0", "NetworkMask": "255.255.255.0", "Protocol": "STATIC", "NextHop": [{"NextHopIp": "40.1.1.2", "NextHopIntRef":"fpPort1"}]}' http://localhost:8080/public/v1/config/IPv4Route
     {"ObjectId":"99181161-6438-40df-7926-a0dd78d5dd29","Error":""}

      curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:8080/public/v1/config/IPv4Routes | python -m json.tool
      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
     100   315  100   315    0     0  76382      0 --:--:-- --:--:-- --:--:--  102k
     {
        "CurrentMarker": 0,
        "MoreExist": false,
        "NextMarker": 0,
        "ObjCount": 1,
        "Objects": [
            {
                "Object": {
                    "Cost": 0,
                    "DestinationNw": "40.1.10.0",
                    "NetworkMask": "255.255.255.0",
                    "NextHop": [
                        {
                            "NextHopIntRef": "fpPort1",
                            "NextHopIp": "40.1.1.2",
                            "Weight": 0
                        }
                    ],
                    "NullRoute": false,
                    "Protocol": "STATIC"
                },
                "ObjectId": "99181161-6438-40df-7926-a0dd78d5dd29"
            }
        ]
    }

	curl -X PATCH -H "Content-Type: application/json" -d '{"op":"add", "DestinationNw": "40.1.10.0", "NetworkMask": "255.255.255.0", "NextHop": [{"NextHopIp": "40.1.2.2", "NextHopIntRef":"fpPort2"}]}' http://localhost:8080/public/v1/config/IPv4Route

    Display after the second next hop add:
	
	curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' http://localhost:8080/public/v1/config/IPv4Routes | python -m json.tool  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
    100   373  100   373    0     0   103k      0 --:--:-- --:--:-- --:--:--  121k
    {
        "CurrentMarker": 0,
        "MoreExist": false,
        "NextMarker": 0,
        "ObjCount": 1,
        "Objects": [
           {
                "Object": {
                    "Cost": 0,
                    "DestinationNw": "40.1.10.0",
                    "NetworkMask": "255.255.255.0",
                    "NextHop": [
                        {
                            "NextHopIntRef": "fpPort2",
                            "NextHopIp": "40.1.2.2",
                            "Weight": 0
                        },
                        {
                            "NextHopIntRef": "fpPort1",
                            "NextHopIp": "40.1.1.2",
                            "Weight": 0
                        }
                    ],
                    "NullRoute": false,
                    "Protocol": "STATIC"
                },
                "ObjectId": "99181161-6438-40df-7926-a0dd78d5dd29"
            }
        ]
    }


Configuring with Python SDK
""""""""""""""""""""""""""""

.. Configuring STP
   ----------------
   RSTP
   ^^^^^
   RSTP-PVST+
   ^^^^^^^^^^
   Configuring with Rest API 
   """"""""""""""""""""""""""""
   Configuring with Python SDK
   """"""""""""""""""""""""""""

Configuring VLANS
-------------------


Configuring with Rest API 
^^^^^^^^^^^^^^^^^^^^^^^^^

**COMMAND**

::
	
	curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"VlanId":<*Vlan-ID*>,"IntfList":<*Tagged Interfaces*>,"UntagIntfList":<*Untagged Interfaces*>}' 'http://your-switchip:8080/public/v1/config/Vlan'

**OPTIONS**

+--------------+-------------+--------------------------------------------+----------+----------+
| Variables    | Type        |  Description                               | Required |  Default |   
+==============+=============+============================================+==========+==========+ 
| VlanId       | integer     | Vlan ID to be configured                   |   Yes    |    N/A   |          
+--------------+-------------+--------------------------------------------+----------+----------+
| Intflist     | string      | comma separated list of tagged interfaces  |    No    |   None   |
+--------------+-------------+--------------------------------------------+----------+----------+
| UntagIntfList| string      | comma separated list of unyagged interfaces|    No    |   None   |
+--------------+-------------+--------------------------------------------+----------+----------+ 


**EXAMPLE**

In this example, 2 new vlans will be created and front-panel ports will be assigned to them.


These curl commands will create vlans 100 and 200 and assign ports 1-10 to vlan 100, ports 11-12 to vlan 200, and ports 13-15, and 17 to vlan 300:

::

	$ curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"VlanId":100,"IntfList":"","UntagIntfList":"1-10"}' 'http://10.1.10.43:8080/public/v1/config/Vlan'

	{"ObjectId":"467f573f-a0d2-42dd-4fcb-181afbfb6624","Error":""}

	$ curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{"VlanId":200,"IntfList":"","UntagIntfList":"11,12"}' 'http://10.1.10.43:8080/public/v1/config/Vlan'

	{"ObjectId":"e183a284-daf1-4397-77f3-c51f45ac5165","Error":""}


**Validation:**

Vlan State:

::

	$ curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.43:8080/public/v1/state/Vlans' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100   502  100   502    0     0  96668      0 --:--:-- --:--:-- --:--:--  122k
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 4096,
		"ObjCount": 3,
		"Objects": [
			{
				"Object": {
					"ConfigObj": null,
					"IfIndex": 33554532,
					"OperState": "UP",
					"VlanId": 100,
					"VlanName": "vlan100"
				},
				"ObjectId": "467f573f-a0d2-42dd-4fcb-181afbfb6624"
			},
			{
				"Object": {
					"ConfigObj": null,
					"IfIndex": 33554632,
					"OperState": "UP",
					"VlanId": 200,
					"VlanName": "vlan200"
				},
				"ObjectId": "e183a284-daf1-4397-77f3-c51f45ac5165"
			},
		]
	}


Vlan Configuration:

::

	$ curl -X GET --header 'Content-Type: application/json' --header 'Accept: application/json' 'http://10.1.10.43:8080/public/v1/config/Vlans' | python -m json.tool
	  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
									 Dload  Upload   Total   Spent    Left  Speed
	100   329  100   329    0     0  23901      0 --:--:-- --:--:-- --:--:-- 25307
	{
		"CurrentMarker": 0,
		"MoreExist": false,
		"NextMarker": 0,
		"ObjCount": 2,
		"Objects": [
			{
				"Object": {
					"ConfigObj": null,
					"IntfList": "",
					"UntagIntfList": "1-10",
					"VlanId": 100
				},
				"ObjectId": "467f573f-a0d2-42dd-4fcb-181afbfb6624"
			},
			{
				"Object": {
					"ConfigObj": null,
					"IntfList": "",
					"UntagIntfList": "11,12",
					"VlanId": 200
				},
				"ObjectId": "e183a284-daf1-4397-77f3-c51f45ac5165"
			}
		]
	}

Configuring with Python SDK
^^^^^^^^^^^^^^^^^^^^^^^^^^^^


Configuring VRRP
-------------------

VRRP (Virtual Router Redundancy Protocol) is an Internet protocol that provides a way to have one or more backup routers when using a statically configured router on a network segment. The most common arrangement is to specify a virtual IP/MAC address between a pair of switches devices to serve as the gateway for forwarding packets from a group of hosts, one switch is designated as a master device, while the other switch (or multiple switches), are designated as a backup device. 
In case the master fails, the ownership of the virtual IP address is mapped to a backup switch's IP address, which has now taken the role of  master.   This action occurs transparently to the end-hosts, since the IP/MAC combination for their discovered gateway (Virtual IP/MAC), does not change. 

Configuring with Rest API 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**COMMAND:**
::

	curl -H "Content-Type: application/json" -d '{"IfIndex":<*Interface Unique Id*>, "VRID":<*Virtual Router ID*>, "Priority":<*Priority for the Vitrual Router*>, "VirtualIPv4Addr":<*Virtual Router Ip Address*>, "PreemptMode":<*true/false*>, "AdvertisementInterval":<*Advertisement time between VRRP frames*>, "AcceptMode":<*true/false*> }' http://<*your-switchip*>:8080/public/v1/VrrpIntf


**OPTIONS:**

+----------------------+------------+---------------------------------------------+----------+----------+
| Variables            | Type       |  Description                                | Required |  Default |
+======================+============+=============================================+==========+==========+
| VRID                 | integer    | Default Virtual Router ID                   |    Yes   |   None   |
|----------------------+------------+---------------------------------------------+----------+----------+
| IfIndex              | integer    | Intf where VRID will be configured          |    Yes   |   None   |
|----------------------+------------+---------------------------------------------+----------+----------+
| VirtualIPv4Addr      | string     | Ip Address for Virtual Router               |    no    |  Port IP |
|----------------------+------------+---------------------------------------------+----------+----------+
| PreemptMode          | boolean    | Preempt a lower-priority Master             |    no    |   True   |
|----------------------+------------+---------------------------------------------+----------+----------+
| Priority             | integer    | Specifiying priority of Virtual Router      |    no    |    100   |
|----------------------+------------+---------------------------------------------+----------+----------+
| AdvertisementInterval| integer    | Adverstise Time interval                    |    no    |     1    |
|----------------------+------------+---------------------------------------------+----------+----------+
| AcceptMode           | boolean    | Accept Packets address to ifIndex           |    no    |   True   |
+----------------------+------------+---------------------------------------------+----------+----------+
**EXAMPLE**



Configuring with Python SDK
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**COMMAND:**
::


	>>> FlexSwitch ("<*Switch Ip*>", <*TCP Port*>).createVrrpIntf(
							   VRID,
							   IfIndex,
							   VirtualIPv4Addr,
							   PreemptMode=True,
							   Priority=100,
							   AdvertisementInterval=1,
							   AcceptMode=False)

**OPTIONS:**

+----------------------+----------------------+------------+---------------------------------------------+----------+----------+
| Python Method        | Variables            | Type       |  Description                                | Required |  Default |
+======================+======================+============+=============================================+==========+==========+
| createVrrpIntf       | VRID                 | integer    | Default Virtual Router ID                   |    Yes   |   None   |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | IfIndex              | integer    | Intf where VRID will be configured          |    Yes   |   None   |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | VirtualIPv4Addr      | string     | Ip Address for Virtual Router               |    no    |  Port IP |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | PreemptMode          | boolean    | Preempt a lower-priority Master             |    no    |   True   |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | Priority             | integer    | Specifiying priority of Virtual Router      |    no    |    100   |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | AdvertisementInterval| integer    | Adverstise Time interval                    |    no    |     1    |
|                      +----------------------+------------+---------------------------------------------+----------+----------+
|                      | AcceptMode           | boolean    | Accept Packets address to ifIndex           |    no    |   True   |
+----------------------+----------------------+------------+---------------------------------------------+----------+----------+

**EXAMPLE:**

Vrrp requires VRID to enable it per port. Once it is configured then Protocol FSM will start

::

	>>> from flexswitchV2 import FlexSwitch
	>>> FlexSwitch("192.168.0.2", 8080).createVrrpIntf(ifIndex=355413 ,VRID=1, VirtualIPv4Addr="172.16.0.1")
