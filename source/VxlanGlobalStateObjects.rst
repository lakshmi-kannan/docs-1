VxlanGlobalState Object
=============================================================

*state/VxlanGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**      | string        | global system object defining  | default     | N/A              |
|                    |               | the global state of VXLAND.    |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumVteps           | uint64        | Number of Vteps provisioned    | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OperState          | string        | Oper state of VXLAND           | DOWN        | UP, DOWN         |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RxInvalidVtepCnt   | uint64        | Number of invalid VXLAN VTEP   | N/A         | N/A              |
|                    |               | frames received                |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/VxlanGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/VxlanGlobalState/<uuid>


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
		response, error = swtch.getVxlanGlobalState(Vrf=vrf)

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
		response, error = swtch.getVxlanGlobalStateById(ObjectId=objectid)

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
		response, error = swtch.getAllVxlanGlobalStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


