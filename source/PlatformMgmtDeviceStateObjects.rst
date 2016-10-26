PlatformMgmtDeviceState Object
=============================================================

*state/PlatformMgmtDevice*
------------------------------------

- Only one object of this type can exist in a system.

+----------------------+---------------+-----------------------------+-------------+------------------+
|  **PARAMETER NAME**  | **DATA TYPE** |       **DESCRIPTION**       | **DEFAULT** | **VALID VALUES** |
+----------------------+---------------+-----------------------------+-------------+------------------+
| DeviceName **[KEY]** | string        | Device Name                 | BMC         | N/A              |
+----------------------+---------------+-----------------------------+-------------+------------------+
| CPUUsage             | string        | CPU Usage                   | N/A         | N/A              |
+----------------------+---------------+-----------------------------+-------------+------------------+
| Description          | string        | Platform Description        | N/A         | N/A              |
+----------------------+---------------+-----------------------------+-------------+------------------+
| MemoryUsage          | string        | Memory Usage                | N/A         | N/A              |
+----------------------+---------------+-----------------------------+-------------+------------------+
| ResetReason          | string        | Reset Reason                | N/A         | N/A              |
+----------------------+---------------+-----------------------------+-------------+------------------+
| Uptime               | string        | Uptime and load description | N/A         | N/A              |
+----------------------+---------------+-----------------------------+-------------+------------------+
| Version              | string        | Version                     | N/A         | N/A              |
+----------------------+---------------+-----------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/PlatformMgmtDevice
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/PlatformMgmtDeviceState/<uuid>


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
		response, error = swtch.getPlatformMgmtDeviceState(DeviceName=devicename)

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
		response, error = swtch.getPlatformMgmtDeviceStateById(ObjectId=objectid)

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
		response, error = swtch.getAllPlatformMgmtDeviceStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


