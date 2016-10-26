VrrpIntf Object
=============================================================

*config/VrrpIntf*
------------------------------------

- Multiple objects of this type can exist in a system.

+-----------------------+---------------+--------------------------------+-------------+------------------+
|  **PARAMETER NAME**   | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| IfIndex **[KEY]**     | int32         | Interface index for which VRRP | N/A         | N/A              |
|                       |               | Config needs to be done        |             |                  |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| VRID **[KEY]**        | int32         | Virtual Router's Unique        | N/A         | N/A              |
|                       |               | Identifier                     |             |                  |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| PreemptMode           | bool          | Controls whether a (starting   | true        | N/A              |
|                       |               | or restarting) higher-priority |             |                  |
|                       |               | Backup router preempts a       |             |                  |
|                       |               | lower-priority Master router   |             |                  |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| Priority              | int32         | Sending VRRP router's priority |         100 | N/A              |
|                       |               | for the virtual router         |             |                  |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| VirtualIPv4Addr       | string        | Virtual Router Identifier      | N/A         | N/A              |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| AcceptMode            | bool          | Controls whether a virtual     | false       | N/A              |
|                       |               | router in Master state will    |             |                  |
|                       |               | accept packets addressed       |             |                  |
|                       |               | to the address owner's IPvX    |             |                  |
|                       |               | address as its own if it is    |             |                  |
|                       |               | not the IPvX address owner.    |             |                  |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| AdvertisementInterval | int32         | Time interval between          |           1 | N/A              |
|                       |               | ADVERTISEMENTS                 |             |                  |
+-----------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/VrrpIntf
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/VrrpIntf/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/VrrpIntfs?CurrentMarker=<x>&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/VrrpIntf
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/VrrpIntf
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/VrrpIntf<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/VrrpIntf
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/VrrpIntf<uuid>


*FlexSwitch SDK API Supported:*
------------------------------------



- **GET**


::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.getVrrpIntf(IfIndex=ifindex, VRID=vrid)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **GET By ID**


::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.getVrrpIntfById(ObjectId=objectid)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'




- **GET ALL**


::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.getAllVrrpIntfs()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **CREATE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.createVrrpIntf(IfIndex=ifindex, VRID=vrid, PreemptMode=preemptmode, Priority=priority, VirtualIPv4Addr=virtualipv4addr, AcceptMode=acceptmode, AdvertisementInterval=advertisementinterval)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **DELETE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.deleteVrrpIntf(IfIndex=ifindex, VRID=vrid)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **DELETE By ID**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.deleteVrrpIntfById(ObjectId=objectid

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **UPDATE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.updateVrrpIntf(IfIndex=ifindex, VRID=vrid, PreemptMode=preemptmode, Priority=priority, VirtualIPv4Addr=virtualipv4addr, AcceptMode=acceptmode, AdvertisementInterval=advertisementinterval)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **UPDATE By ID**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.updateVrrpIntfById(ObjectId=objectidPreemptMode=preemptmode, Priority=priority, VirtualIPv4Addr=virtualipv4addr, AcceptMode=acceptmode, AdvertisementInterval=advertisementinterval)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
