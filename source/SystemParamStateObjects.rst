SystemParamState Object
=============================================================

*state/SystemParam*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**      | string        | System Vrf                     | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| MgmtIp             | string        | Management Ip of System        | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SwVersion          | string        | FlexSwitch Version Information | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SwitchMac          | string        | Switch Mac Address             | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Description        | string        | System Description             | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Distro             | string        | Linux distro running on this   | N/A         | N/A              |
|                    |               | system                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Hostname           | string        | System Host Name               | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Kernel             | string        | Kernel version running on this | N/A         | N/A              |
|                    |               | system                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/SystemParam
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/SystemParams?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/SystemParamState/<uuid>


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
		response, error = swtch.getSystemParamState(Vrf=vrf)

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
		response, error = swtch.getSystemParamStateById(ObjectId=objectid)

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
		response, error = swtch.getAllSystemParamStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


