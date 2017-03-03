IPV6AdjState Object
=============================================================

*state/IPV6Adj*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IntfRef **[KEY]**  | string        | Port where neighbor ip's are   | N/A         | N/A              |
|                    |               | learned                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ReceivedPackets    | int64         | Total Packets received by      | N/A         | N/A              |
|                    |               | local port                     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SendPackets        | int64         | Total Packets send from the    | N/A         | N/A              |
|                    |               | local port                     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| GlobalScopeIp      | string        | Local Port Global Scope ip     | N/A         | N/A              |
|                    |               | address                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfIndex            | int32         | System generated unique id for | N/A         | N/A              |
|                    |               | local port                     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| LinkScopeIp        | string        | Local Port link scope ip       | N/A         | N/A              |
|                    |               | address                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Neighbors          | NeighborEntry |                                | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/IPV6Adj
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/IPV6Adjs?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/IPV6AdjState/<uuid>


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
		response, error = swtch.getIPV6AdjState(IntfRef=intfref)

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
		response, error = swtch.getIPV6AdjStateById(ObjectId=objectid)

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
		response, error = swtch.getAllIPV6AdjStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


