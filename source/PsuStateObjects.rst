PsuState Object
=============================================================

*state/Psu*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+---------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |   **DESCRIPTION**   | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+---------------------+-------------+------------------+
| PsuId **[KEY]**    | int32         | PSU id              |           0 | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| FanId              | int32         | Fan Info            | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| LedId              | int32         | LED Info            | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| ModelNum           | string        | Model Number        | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| Pin                | int32         | Power in            | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| Pout               | int32         | power out           | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| AdminState         | string        | Admin UP/DOWN PSU   | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| Fan                | string        | Fan PRESENT/MISSING | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| Iin                | int32         | Current in          | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| Iout               | int32         | Current out         | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| SerialNum          | string        | Serial Number       | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| Vin                | int32         | Voltage in          | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+
| Vout               | int32         | Voltage out         | N/A         | N/A              |
+--------------------+---------------+---------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/Psu
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/Psus?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/PsuState/<uuid>


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
		response, error = swtch.getPsuState(PsuId=psuid)

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
		response, error = swtch.getPsuStateById(ObjectId=objectid)

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
		response, error = swtch.getAllPsuStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


