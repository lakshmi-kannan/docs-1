TemperatureSensor Object
=============================================================

*config/TemperatureSensor*
------------------------------------

- Multiple objects of this type can exist in a system.

+------------------------+---------------+--------------------------------+-------------+------------------+
|   **PARAMETER NAME**   | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+------------------------+---------------+--------------------------------+-------------+------------------+
| Name **[KEY]**         | string        | Temperature Sensor Name        | N/A         | N/A              |
+------------------------+---------------+--------------------------------+-------------+------------------+
| PMClassAAdminState     | string        | PM Class-A Admin State         | Enable      | Enable, Disable  |
+------------------------+---------------+--------------------------------+-------------+------------------+
| HigherWarningThreshold | float64       | Higher Warning Threshold for   | N/A         | N/A              |
|                        |               | TCA                            |             |                  |
+------------------------+---------------+--------------------------------+-------------+------------------+
| HigherAlarmThreshold   | float64       | Higher Alarm Threshold for TCA | N/A         | N/A              |
+------------------------+---------------+--------------------------------+-------------+------------------+
| LowerAlarmThreshold    | float64       | Lower Alarm Threshold for TCA  | N/A         | N/A              |
+------------------------+---------------+--------------------------------+-------------+------------------+
| LowerWarningThreshold  | float64       | Lower Warning Threshold for    | N/A         | N/A              |
|                        |               | TCA                            |             |                  |
+------------------------+---------------+--------------------------------+-------------+------------------+
| PMClassBAdminState     | string        | PM Class-B Admin State         | Enable      | Enable, Disable  |
+------------------------+---------------+--------------------------------+-------------+------------------+
| PMClassCAdminState     | string        | PM Class-C Admin State         | Enable      | Enable, Disable  |
+------------------------+---------------+--------------------------------+-------------+------------------+
| AdminState             | string        | Enable/Disable                 | Enable      | Enable, Disable  |
+------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/TemperatureSensor
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/TemperatureSensor/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/TemperatureSensors?CurrentMarker=<x>&Count=<y>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/TemperatureSensor
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/TemperatureSensor<uuid>


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
		response, error = swtch.getTemperatureSensor(Name=name)

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
		response, error = swtch.getTemperatureSensorById(ObjectId=objectid)

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
		response, error = swtch.getAllTemperatureSensors()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'




- **UPDATE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.updateTemperatureSensor(Name=name, PMClassAAdminState=pmclassaadminstate, HigherWarningThreshold=higherwarningthreshold, HigherAlarmThreshold=higheralarmthreshold, LowerAlarmThreshold=loweralarmthreshold, LowerWarningThreshold=lowerwarningthreshold, PMClassBAdminState=pmclassbadminstate, PMClassCAdminState=pmclasscadminstate, AdminState=adminstate)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **UPDATE By ID**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.updateTemperatureSensorById(ObjectId=objectidPMClassAAdminState=pmclassaadminstate, HigherWarningThreshold=higherwarningthreshold, HigherAlarmThreshold=higheralarmthreshold, LowerAlarmThreshold=loweralarmthreshold, LowerWarningThreshold=lowerwarningthreshold, PMClassBAdminState=pmclassbadminstate, PMClassCAdminState=pmclasscadminstate, AdminState=adminstate)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
