IPv4RouteState Object
=============================================================

*state/IPv4Route*
------------------------------------

- Multiple objects of this type can exist in a system.

+-------------------------+-------------------+--------------------------------+-------------+------------------+
|   **PARAMETER NAME**    |   **DATA TYPE**   |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+-------------------------+-------------------+--------------------------------+-------------+------------------+
| DestinationNw **[KEY]** | string            | IP address of the route        | N/A         | N/A              |
+-------------------------+-------------------+--------------------------------+-------------+------------------+
| RouteCreatedTime        | string            | Time when the route was added  | N/A         | N/A              |
+-------------------------+-------------------+--------------------------------+-------------+------------------+
| RouteUpdatedTime        | string            | Time when the route was last   | N/A         | N/A              |
|                         |                   | updated                        |             |                  |
+-------------------------+-------------------+--------------------------------+-------------+------------------+
| IsNetworkReachable      | bool              | Indicates whether this network | N/A         | N/A              |
|                         |                   | is reachable                   |             |                  |
+-------------------------+-------------------+--------------------------------+-------------+------------------+
| NextBestRoute           | NextBestRouteInfo |                                | N/A         | N/A              |
+-------------------------+-------------------+--------------------------------+-------------+------------------+
| NextHopList             | NextHopInfo       | List of next hops to reach     | N/A         | N/A              |
|                         |                   | this network                   |             |                  |
+-------------------------+-------------------+--------------------------------+-------------+------------------+
| PolicyList              | string            | List of policies applied on    | N/A         | N/A              |
|                         |                   | this route                     |             |                  |
+-------------------------+-------------------+--------------------------------+-------------+------------------+
| Protocol                | string            | Protocol type of the route     | N/A         | N/A              |
+-------------------------+-------------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/IPv4Route
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/IPv4Routes?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/IPv4RouteState/<uuid>


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
		response, error = swtch.getIPv4RouteState(DestinationNw=destinationnw)

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
		response, error = swtch.getIPv4RouteStateById(ObjectId=objectid)

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
		response, error = swtch.getAllIPv4RouteStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


