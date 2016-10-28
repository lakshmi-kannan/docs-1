PlatformState Object
=============================================================

*state/Platform*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+-------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |     **DESCRIPTION**     | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+-------------------------+-------------+------------------+
| ObjName **[KEY]**  | string        | ObjName                 | Platform    | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| Manufacturer       | string        | Manufacturer            | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| PlatformName       | string        | Platform Number         | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| ProductName        | string        | Product Number          | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| Release            | string        | Relese version          | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| SerialNum          | string        | Serial Number           | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| Vendor             | string        | Vendor                  | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| Version            | string        | Platform Driver version | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/Platform
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/PlatformState/<uuid>


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
		response, error = swtch.getPlatformState(ObjName=objname)

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
		response, error = swtch.getPlatformStateById(ObjectId=objectid)

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
		response, error = swtch.getAllPlatformStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


