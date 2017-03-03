RouteStatsPerProtocolState Object
=============================================================

*state/RouteStatsPerProtocol*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+------------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** |  **DATA TYPE**   |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+------------------+--------------------------------+-------------+------------------+
| Protocol **[KEY]** | string           | Protocol type of the route     | N/A         | N/A              |
+--------------------+------------------+--------------------------------+-------------+------------------+
| V4Routes           | RouteInfoSummary | Brief summary info of ipv4     | N/A         | N/A              |
|                    |                  | routes of this protocol type   |             |                  |
+--------------------+------------------+--------------------------------+-------------+------------------+
| V6Routes           | RouteInfoSummary | Brief summary info of ipv6     | N/A         | N/A              |
|                    |                  | routes of this protocol type   |             |                  |
+--------------------+------------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/RouteStatsPerProtocol
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/RouteStatsPerProtocolState/<uuid>


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
		response, error = swtch.getRouteStatsPerProtocolState(Protocol=protocol)

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
		response, error = swtch.getRouteStatsPerProtocolStateById(ObjectId=objectid)

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
		response, error = swtch.getAllRouteStatsPerProtocolStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


