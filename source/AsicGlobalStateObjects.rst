AsicGlobalState Object
=============================================================

*state/AsicGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ModuleId **[KEY]** | uint8         | Module identifier              | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ModuleTemp         | float64       | Current module temperature     | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| PartNumber         | string        | Part number of underlying      | N/A         | N/A              |
|                    |               | switching asic                 |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RevisionId         | string        | Revision ID of underlying      | N/A         | N/A              |
|                    |               | switching asic                 |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| VendorId           | string        | Vendor identification value    | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/AsicGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/AsicGlobalState/<uuid>


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
		response, error = swtch.getAsicGlobalState(ModuleId=moduleid)

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
		response, error = swtch.getAsicGlobalStateById(ObjectId=objectid)

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
		response, error = swtch.getAllAsicGlobalStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


