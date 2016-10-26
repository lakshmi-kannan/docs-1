VrrpIntfState Object
=============================================================

*state/VrrpIntf*
------------------------------------

- Multiple objects of this type can exist in a system.

+-------------------------+---------------+--------------------------------+-------------+------------------+
|   **PARAMETER NAME**    | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| VRID **[KEY]**          | int32         | Virtual Router's Unique        | N/A         | N/A              |
|                         |               | Identifier                     |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| IfIndex **[KEY]**       | int32         | Interface index for which VRRP | N/A         | N/A              |
|                         |               | state is requested             |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| AdvertisementInterval   | int32         | Time interval between          | N/A         | N/A              |
|                         |               | Advertisements                 |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| IntfIpAddr              | string        | Ip Address of Interface where  | N/A         | N/A              |
|                         |               | VRRP is configured             |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| PreemptMode             | bool          | States Whether Preempt is      | N/A         | N/A              |
|                         |               | Supported or not               |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| SkewTime                | int32         | Time to skew Master Down       | N/A         | N/A              |
|                         |               | Interval                       |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| VirtualIPv4Addr         | string        | Ip Address of Virtual Router   | N/A         | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| MasterDownTimer         | int32         | Time interval for Backup to    | N/A         | N/A              |
|                         |               | declare Master down            |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| Priority                | int32         | Virtual router's Priority      | N/A         | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| VirtualRouterMACAddress | string        | VRRP router's Mac Address      | N/A         | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| VrrpState               | string        | Current vrrp state i.e. backup | N/A         | N/A              |
|                         |               | or master                      |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/VrrpIntf
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/VrrpIntfs?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/VrrpIntfState/<uuid>


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
		response, error = swtch.getVrrpIntfState(VRID=vrid, IfIndex=ifindex)

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
		response, error = swtch.getVrrpIntfStateById(ObjectId=objectid)

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
		response, error = swtch.getAllVrrpIntfStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


