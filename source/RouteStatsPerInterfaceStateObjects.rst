RouteStatsPerInterfaceState Object
=============================================================

*state/RouteStatsPerInterface*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Intfref **[KEY]**  | string        | Interface of the next hop      | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| V4Routes           | string        | Brief summary info of ipv4     | N/A         | N/A              |
|                    |               | routes which have nexthop on   |             |                  |
|                    |               | this interface                 |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| V6Routes           | string        | Brief summary info of ipv6     | N/A         | N/A              |
|                    |               | routes which have nexthop on   |             |                  |
|                    |               | this interface                 |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/RouteStatsPerInterface
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/RouteStatsPerInterfaceState/<uuid>


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
		response, error = swtch.getRouteStatsPerInterfaceState(Intfref=intfref)

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
		response, error = swtch.getRouteStatsPerInterfaceStateById(ObjectId=objectid)

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
		response, error = swtch.getAllRouteStatsPerInterfaceStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


