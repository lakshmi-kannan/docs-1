LacpGlobalState Object
=============================================================

*state/LacpGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+------------------------------+---------------+--------------------------------+-------------+------------------+
|      **PARAMETER NAME**      | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**                | string        | global system object defining  | default     | N/A              |
|                              |               | the global state of LACPD.     |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| AdminState                   | string        | Administrative state of LACPD  | DOWN        | UP, DOWN         |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| DistributedRelayAttachedList | string        | List of Distributed Relay      | N/A         | N/A              |
|                              |               | objects who are attached to    |             |                  |
|                              |               | an Aggregator in the form of   |             |                  |
|                              |               | DRName-AggName                 |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| DistributedRelayList         | string        | List of Distributed Relay      | N/A         | N/A              |
|                              |               | objects                        |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| DistributedRelayUpList       | string        | List of Distributed Relay      | N/A         | N/A              |
|                              |               | objects whose Aggregator is in |             |                  |
|                              |               | Oper State Up                  |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| LacpTotalRxPkts              | uint64        | Total Rx pkts accross all LACP | N/A         | N/A              |
|                              |               | Ports                          |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| LacpTotalTxPkts              | uint64        | Total Tx pkts accross all LACP | N/A         | N/A              |
|                              |               | Ports                          |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| AggList                      | string        | List of Aggregation objects    | N/A         | N/A              |
|                              |               | that have been created         |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| AggOperStateUpList           | string        | List of Aggregation objects    | N/A         | N/A              |
|                              |               | which have at least one port   |             |                  |
|                              |               | in Distributed State           |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| LacpErrorsInPkts             | uint64        | Total number of Error pkts     | N/A         | N/A              |
|                              |               | received; Unknown or Illegal   |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+
| LacpMissMatchPkts            | uint64        | Total number of pkts           | N/A         | N/A              |
|                              |               | received which have received   |             |                  |
|                              |               | missmatched info from peer     |             |                  |
+------------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/LacpGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/LacpGlobalState/<uuid>


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
		response, error = swtch.getLacpGlobalState(Vrf=vrf)

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
		response, error = swtch.getLacpGlobalStateById(ObjectId=objectid)

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
		response, error = swtch.getAllLacpGlobalStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


