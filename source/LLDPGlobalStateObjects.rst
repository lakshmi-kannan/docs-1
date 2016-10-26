LLDPGlobalState Object
=============================================================

*state/LLDPGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**      | string        | Vrf where LLDP Global Config   | N/A         | N/A              |
|                    |               | is running                     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Enable             | bool          | Enable/Disable LLDP Globally   | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Neighbors          | int32         | Total lldp Neighbors learned   | N/A         | N/A              |
|                    |               | on the system                  |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| TotalRxFrames      | int32         | Total no.of lldp frames        | N/A         | N/A              |
|                    |               | received by the system         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| TotalTxFrames      | int32         | Total no.of lldp frames send   | N/A         | N/A              |
|                    |               | out by the system              |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| TranmitInterval    | int32         | LLDP Re-Transmit Interval in   | N/A         | N/A              |
|                    |               | seconds                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/LLDPGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/LLDPGlobalState/<uuid>


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
		response, error = swtch.getLLDPGlobalState(Vrf=vrf)

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
		response, error = swtch.getLLDPGlobalStateById(ObjectId=objectid)

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
		response, error = swtch.getAllLLDPGlobalStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


