BGPv6RouteState Object
=============================================================

*state/BGPv6Route*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Network **[KEY]**  | string        | Network address of the IPv6    | N/A         | N/A              |
|                    |               | destination                    |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| CIDRLen **[KEY]**  | uint16        | CIDR length of the IPv6        | N/A         | N/A              |
|                    |               | destination                    |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Paths              | PathInfo      |                                | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/BGPv6Route
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/BGPv6Routes?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BGPv6RouteState/<uuid>


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
		response, error = swtch.getBGPv6RouteState(Network=network, CIDRLen=cidrlen)

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
		response, error = swtch.getBGPv6RouteStateById(ObjectId=objectid)

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
		response, error = swtch.getAllBGPv6RouteStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


