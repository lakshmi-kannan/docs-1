OspfIPv4RouteState Object
=============================================================

*state/OspfIPv4Route*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| DestId **[KEY]**   | string        | Dest ip                        | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| AddrMask **[KEY]** | string        | netmask                        | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| DestType **[KEY]** | string        | destination type               | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumOfPaths         | int32         | Total number of paths          | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OptCapabilities    | int32         | capabilities                   | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| AreaId             | string        | area id for the route          | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| LSOrigin           | OspfLsaKey    | Ls dabatase key                | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NextHops           | OspfNextHop   | Nexthops for this route        | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| PathType           | string        | Path type such as direct /     | N/A         | N/A              |
|                    |               | connected / ext                |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Type2Cost          | int32         | Type2 cost used for external   | N/A         | N/A              |
|                    |               | routes.                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Cost               | int32         | Cost to reach the destination  | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/OspfIPv4Route
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/OspfIPv4Routes?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfIPv4RouteState/<uuid>


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
		response, error = swtch.getOspfIPv4RouteState(DestId=destid, AddrMask=addrmask, DestType=desttype)

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
		response, error = swtch.getOspfIPv4RouteStateById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfIPv4RouteStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


