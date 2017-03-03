FanState Object
=============================================================

*state/Fan*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| FanId **[KEY]**    | int32         | Fan unit id                    |           0 | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| LedId              | int32         | LED Info                       | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Model              | string        | Model of Fan                   | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OperDirection      | string        | Air flow caused because of fan | N/A         | B2F, F2B         |
|                    |               | rotation                       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OperMode           | string        | Operational state of Fan       | N/A         | ON, OFF          |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OperSpeed          | int32         | Fan operational speed in rpm   | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SerialNum          | string        | Serial Number                  | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Status             | string        | Fan status                     | N/A         | N/A              |
|                    |               | PRESENT/MISSING/FAILED/NORMAL  |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/Fan
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/Fans?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/FanState/<uuid>


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
		response, error = swtch.getFanState(FanId=fanid)

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
		response, error = swtch.getFanStateById(ObjectId=objectid)

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
		response, error = swtch.getAllFanStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


