IPv4IntfState Object
=============================================================

*state/IPv4Intf*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IntfRef **[KEY]**  | string        | System assigned interface      | N/A         | N/A              |
|                    |               | id of L2 interface             |             |                  |
|                    |               | (port/lag/vlan) to which this  |             |                  |
|                    |               | IPv4 object is linked          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| L2IntfId           | int32         | Id of the L2 interface. Port   | N/A         | N/A              |
|                    |               | number/lag id/vlan id.         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| LastDownEventTime  | string        | Timestamp corresponding to the | N/A         | N/A              |
|                    |               | last UP to DOWN operational    |             |                  |
|                    |               | state change event             |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumDownEvents      | int32         | Number of times the            | N/A         | N/A              |
|                    |               | operational state transitioned |             |                  |
|                    |               | from UP to DOWN                |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumUpEvents        | int32         | Number of times the            | N/A         | N/A              |
|                    |               | operational state transitioned |             |                  |
|                    |               | from DOWN to UP                |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OperState          | string        | Operational state of this IP   | N/A         | N/A              |
|                    |               | interface                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfIndex            | int32         | System assigned interface id   | N/A         | N/A              |
|                    |               | for this IPv4 interface        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IpAddr             | string        | Interface IP/Net mask in CIDR  | N/A         | N/A              |
|                    |               | format to provision on switch  |             |                  |
|                    |               | interface                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| L2IntfType         | string        | Type of L2 interface on        | N/A         | N/A              |
|                    |               | which IP has been configured   |             |                  |
|                    |               | (Port/Lag/Vlan)                |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| LastUpEventTime    | string        | Timestamp corresponding to the | N/A         | N/A              |
|                    |               | last DOWN to UP operational    |             |                  |
|                    |               | state change event             |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/IPv4Intf
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/IPv4Intfs?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/IPv4IntfState/<uuid>


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
		response, error = swtch.getIPv4IntfState(IntfRef=intfref)

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
		response, error = swtch.getIPv4IntfStateById(ObjectId=objectid)

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
		response, error = swtch.getAllIPv4IntfStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


