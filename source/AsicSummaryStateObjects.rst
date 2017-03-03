AsicSummaryState Object
=============================================================

*state/AsicSummary*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ModuleId **[KEY]** | uint8         | Module identifier              | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumPortsDown       | int32         | Summary stating number of      | N/A         | N/A              |
|                    |               | ports that have operstate DOWN |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumV4Adjs          | int32         | Summary stating number of IPv4 | N/A         | N/A              |
|                    |               | adjacencies configured in the  |             |                  |
|                    |               | asic                           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumV6Intfs         | int32         | Summary stating number of IPv6 | N/A         | N/A              |
|                    |               | interfaces configured in the   |             |                  |
|                    |               | asic                           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumV6Routes        | int32         | Summary stating number of IPv6 | N/A         | N/A              |
|                    |               | routes configured in the asic  |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumVlans           | int32         | Summary stating number of      | N/A         | N/A              |
|                    |               | vlans configured in the asic   |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumECMPRoutes      | int32         | Summary stating number of ECMP | N/A         | N/A              |
|                    |               | routes configured in the asic  |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumPortsUp         | int32         | Summary stating number of      | N/A         | N/A              |
|                    |               | ports that have operstate UP   |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumV4Intfs         | int32         | Summary stating number of IPv4 | N/A         | N/A              |
|                    |               | interfaces configured in the   |             |                  |
|                    |               | asic                           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumV4Routes        | int32         | Summary stating number of IPv4 | N/A         | N/A              |
|                    |               | routes configured in the asic  |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumV6Adjs          | int32         | Summary stating number of IPv6 | N/A         | N/A              |
|                    |               | adjacencies configured in the  |             |                  |
|                    |               | asic                           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/AsicSummary
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/AsicSummaryState/<uuid>


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
		response, error = swtch.getAsicSummaryState(ModuleId=moduleid)

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
		response, error = swtch.getAsicSummaryStateById(ObjectId=objectid)

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
		response, error = swtch.getAllAsicSummaryStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


