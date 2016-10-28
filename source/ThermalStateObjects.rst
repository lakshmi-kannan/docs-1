ThermalState Object
=============================================================

*state/Thermal*
------------------------------------

- Multiple objects of this type can exist in a system.

+---------------------------+---------------+--------------------------------+-------------+------------------+
|    **PARAMETER NAME**     | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| ThermalId **[KEY]**       | int32         | Thermal sensor id              |           0 | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| Location                  | string        | Thermal sensor location        | N/A         | N/A              |
|                           |               | CPU/PSU/Motherboard            |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| LowerWatermarkTemperature | string        | Temperature warning            | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| ShutdownTemperature       | string        | Temperature panic              | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| Temperature               | string        | Temperature current            | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| UpperWatermarkTemperature | string        | Temperature error              | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/Thermal
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/Thermals?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/ThermalState/<uuid>


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
		response, error = swtch.getThermalState(ThermalId=thermalid)

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
		response, error = swtch.getThermalStateById(ObjectId=objectid)

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
		response, error = swtch.getAllThermalStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


