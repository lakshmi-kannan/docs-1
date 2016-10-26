SfpState Object
=============================================================

*state/Sfp*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+----------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |      **DESCRIPTION**       | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+----------------------------+-------------+------------------+
| SfpId **[KEY]**    | int32         | SFP id                     |           0 | N/A              |
+--------------------+---------------+----------------------------+-------------+------------------+
| SfpSpeed           | string        | SFP speed in MBPS          | N/A         | N/A              |
+--------------------+---------------+----------------------------+-------------+------------------+
| SfpType            | string        | SFP type Copper/Optical    | N/A         | N/A              |
+--------------------+---------------+----------------------------+-------------+------------------+
| EEPROM             | string        | SFP eeprom                 | N/A         | N/A              |
+--------------------+---------------+----------------------------+-------------+------------------+
| SerialNum          | string        | SFP SerialNum              | N/A         | N/A              |
+--------------------+---------------+----------------------------+-------------+------------------+
| SfpLOS             | string        | SFP status RX LOS          | N/A         | N/A              |
+--------------------+---------------+----------------------------+-------------+------------------+
| SfpPresent         | string        | SFP status PRESENT/MISSING | N/A         | N/A              |
+--------------------+---------------+----------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/Sfp
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/Sfps?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/SfpState/<uuid>


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
		response, error = swtch.getSfpState(SfpId=sfpid)

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
		response, error = swtch.getSfpStateById(ObjectId=objectid)

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
		response, error = swtch.getAllSfpStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


