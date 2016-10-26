NDPGlobalState Object
=============================================================

*state/NDPGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+-----------------------------+---------------+--------------------------------+-------------+------------------+
|     **PARAMETER NAME**      | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**               | string        | System Vrf                     | default     | N/A              |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| Neighbors                   | int32         | Total Neighbors learned on the | N/A         | N/A              |
|                             |               | system                         |             |                  |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| ReachableTime               | int32         | The time a neighbor is         | N/A         | N/A              |
|                             |               | considered reachable after     |             |                  |
|                             |               | receiving a reachability       |             |                  |
|                             |               | confirmation in ms             |             |                  |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| RetransmitInterval          | int32         | The time between               | N/A         | N/A              |
|                             |               | retransmissions of Neighbor    |             |                  |
|                             |               | Solicitation messages to a     |             |                  |
|                             |               | neighbor when resolving the    |             |                  |
|                             |               | address or when probing the    |             |                  |
|                             |               | reachability of a neighbor in  |             |                  |
|                             |               | ms                             |             |                  |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| RouterAdvertisementInterval | int32         | Delay between each router      | N/A         | N/A              |
|                             |               | advertisements in seconds      |             |                  |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| TotalRxPackets              | int64         | Total no.of ndp packets        | N/A         | N/A              |
|                             |               | received by the system         |             |                  |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| TotalTxPackets              | int64         | Total no.of ndp packets send   | N/A         | N/A              |
|                             |               | out by the system              |             |                  |
+-----------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/NDPGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/NDPGlobalState/<uuid>


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
		response, error = swtch.getNDPGlobalState(Vrf=vrf)

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
		response, error = swtch.getNDPGlobalStateById(ObjectId=objectid)

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
		response, error = swtch.getAllNDPGlobalStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


