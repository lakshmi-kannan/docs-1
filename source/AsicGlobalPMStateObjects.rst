AsicGlobalPMState Object
=============================================================

*state/AsicGlobalPM*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ModuleId **[KEY]** | uint8         | Module identifier              | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Resource **[KEY]** | string        | Resource identifier            | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClassAPMData       | PMData        | PM Data corresponding to PM    | N/A         | N/A              |
|                    |               | Class A                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClassBPMData       | PMData        | PM Data corresponding to PM    | N/A         | N/A              |
|                    |               | Class B                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClassCPMData       | PMData        | PM Data corresponding to PM    | N/A         | N/A              |
|                    |               | Class C                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/AsicGlobalPM
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/AsicGlobalPMState/<uuid>


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
		response, error = swtch.getAsicGlobalPMState(ModuleId=moduleid, Resource=resource)

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
		response, error = swtch.getAsicGlobalPMStateById(ObjectId=objectid)

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
		response, error = swtch.getAllAsicGlobalPMStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


