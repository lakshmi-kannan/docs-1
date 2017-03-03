BfdGlobalState Object
=============================================================

*state/BfdGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+----------------------+---------------+--------------------------------+-------------+------------------+
|  **PARAMETER NAME**  | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+----------------------+---------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**        | string        | VRF id for which global BFD    | N/A         | N/A              |
|                      |               | state is requested             |             |                  |
+----------------------+---------------+--------------------------------+-------------+------------------+
| NumUpSessions        | uint32        | Number of BFD sessions in up   | N/A         | N/A              |
|                      |               | state                          |             |                  |
+----------------------+---------------+--------------------------------+-------------+------------------+
| Enable               | bool          | Global BFD state in this VRF   | N/A         | N/A              |
+----------------------+---------------+--------------------------------+-------------+------------------+
| NumAdminDownSessions | uint32        | Number of BFD sessions in      | N/A         | N/A              |
|                      |               | admin down state               |             |                  |
+----------------------+---------------+--------------------------------+-------------+------------------+
| NumDownSessions      | uint32        | Number of BFD sessions in down | N/A         | N/A              |
|                      |               | state                          |             |                  |
+----------------------+---------------+--------------------------------+-------------+------------------+
| NumTotalSessions     | uint32        | Total number of BFD sessions   | N/A         | N/A              |
+----------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/BfdGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BfdGlobalState/<uuid>


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
		response, error = swtch.getBfdGlobalState(Vrf=vrf)

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
		response, error = swtch.getBfdGlobalStateById(ObjectId=objectid)

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
		response, error = swtch.getAllBfdGlobalStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


