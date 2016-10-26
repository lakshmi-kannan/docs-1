SystemParam Object
=============================================================

*config/SystemParam*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**      | string        | System Vrf                     | default     | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Description        | string        | System Description             | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Hostname           | string        | System Host Name               | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| MgmtIp             | string        | Management Ip of System        | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SwVersion          | string        | FlexSwitch Version Information | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SwitchMac          | string        | Switch Mac Address             | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/SystemParam
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/SystemParam/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/SystemParams?CurrentMarker=<x>&Count=<y>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/SystemParam
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/SystemParam<uuid>


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
		response, error = swtch.getSystemParam(Vrf=vrf)

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
		response, error = swtch.getSystemParamById(ObjectId=objectid)

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
		response, error = swtch.getAllSystemParams()

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
		response, error = swtch.updateSystemParam(Vrf=vrf, Description=description, Hostname=hostname, MgmtIp=mgmtip, SwVersion=swversion, SwitchMac=switchmac)

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
		response, error = swtch.updateSystemParamById(ObjectId=objectidDescription=description, Hostname=hostname, MgmtIp=mgmtip, SwVersion=swversion, SwitchMac=switchmac)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
