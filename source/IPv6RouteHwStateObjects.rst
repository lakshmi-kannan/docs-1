IPv6RouteHwState Object
=============================================================

*state/IPv6RouteHw*
------------------------------------

- Multiple objects of this type can exist in a system.

+-------------------------+---------------+--------------------------------+-------------+------------------+
|   **PARAMETER NAME**    | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| DestinationNw **[KEY]** | string        | IP address of the route in     | N/A         | N/A              |
|                         |               | CIDR format                    |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| RouteUpdatedTime        | string        | Time when the route was last   | N/A         | N/A              |
|                         |               | updated                        |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| NextHopIps              | string        | next hop ip list for the route | N/A         | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| RouteCreatedTime        | string        | Time when the route was added  | N/A         | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/IPv6RouteHw
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/IPv6RouteHws?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/IPv6RouteHwState/<uuid>


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
		response, error = swtch.getIPv6RouteHwState(DestinationNw=destinationnw)

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
		response, error = swtch.getIPv6RouteHwStateById(ObjectId=objectid)

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
		response, error = swtch.getAllIPv6RouteHwStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


