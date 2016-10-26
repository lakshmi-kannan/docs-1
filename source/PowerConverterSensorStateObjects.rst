PowerConverterSensorState Object
=============================================================

*state/PowerConverterSensor*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+-----------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |       **DESCRIPTION**       | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+-----------------------------+-------------+------------------+
| Name **[KEY]**     | string        | Power Converter Sensor Name | N/A         | N/A              |
+--------------------+---------------+-----------------------------+-------------+------------------+
| CurrentPower       | float64       | Current Output Power Value  | N/A         | N/A              |
+--------------------+---------------+-----------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/PowerConverterSensor
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/PowerConverterSensors?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/PowerConverterSensorState/<uuid>


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
		response, error = swtch.getPowerConverterSensorState(Name=name)

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
		response, error = swtch.getPowerConverterSensorStateById(ObjectId=objectid)

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
		response, error = swtch.getAllPowerConverterSensorStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


