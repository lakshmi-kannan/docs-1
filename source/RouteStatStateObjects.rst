RouteStatState Object
=============================================================

*state/RouteStat*
------------------------------------

- Only one object of this type can exist in a system.

+---------------------------+-----------------------+--------------------------------+-------------+------------------+
|    **PARAMETER NAME**     |     **DATA TYPE**     |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+---------------------------+-----------------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**             | string                | System Vrf                     | default     | N/A              |
+---------------------------+-----------------------+--------------------------------+-------------+------------------+
| PerProtocolRouteCountList | PerProtocolRouteCount | Per Protocol routes stats      | N/A         | N/A              |
+---------------------------+-----------------------+--------------------------------+-------------+------------------+
| TotalRouteCount           | int32                 | Total number of routes on the  | N/A         | N/A              |
|                           |                       | system                         |             |                  |
+---------------------------+-----------------------+--------------------------------+-------------+------------------+
| V4RouteCount              | int32                 | Total number of IPv4 routes on | N/A         | N/A              |
|                           |                       | the system                     |             |                  |
+---------------------------+-----------------------+--------------------------------+-------------+------------------+
| V6RouteCount              | int32                 | Total number of IPv6 routes on | N/A         | N/A              |
|                           |                       | the system                     |             |                  |
+---------------------------+-----------------------+--------------------------------+-------------+------------------+
| ECMPRouteCount            | int32                 | ECMP routes on the system      | N/A         | N/A              |
+---------------------------+-----------------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/RouteStat
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/RouteStatState/<uuid>


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
		response, error = swtch.getRouteStatState(Vrf=vrf)

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
		response, error = swtch.getRouteStatStateById(ObjectId=objectid)

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
		response, error = swtch.getAllRouteStatStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


