BfdSessionParamState Object
=============================================================

*state/BfdSessionParam*
------------------------------------

- Multiple objects of this type can exist in a system.

+---------------------------+---------------+--------------------------------+-------------+------------------+
|    **PARAMETER NAME**     | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| Name **[KEY]**            | string        | Session parameters             | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RequiredMinRxInterval     | string        | Required minimum rx interval   | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AuthenticationEnabled     | bool          | Authentication enabled         | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| DemandEnabled             | bool          | Demand mode enabled            | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RequiredMinEchoRxInterval | string        | Required minimum echo rx       | N/A         | N/A              |
|                           |               | interval                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| DesiredMinTxInterval      | string        | Desired minimum tx interval    | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| LocalMultiplier           | int32         | Detection multiplier           | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| NumSessions               | int32         | Number of sessions using these | N/A         | N/A              |
|                           |               | params                         |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AuthenticationData        | string        | Authentication password        | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AuthenticationKeyId       | int32         | Authentication key id          | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AuthenticationType        | string        | Authentication type            | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/BfdSessionParam
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/BfdSessionParams?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BfdSessionParamState/<uuid>


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
		response, error = swtch.getBfdSessionParamState(Name=name)

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
		response, error = swtch.getBfdSessionParamStateById(ObjectId=objectid)

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
		response, error = swtch.getAllBfdSessionParamStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


