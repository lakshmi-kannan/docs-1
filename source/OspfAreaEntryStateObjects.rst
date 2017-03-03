OspfAreaEntryState Object
=============================================================

*state/OspfAreaEntry*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| AreaId **[KEY]**   | string        | A 32-bit integer uniquely      | N/A         | N/A              |
|                    |               | identifying an area. Area ID   |             |                  |
|                    |               | 0.0.0.0 is used for the OSPF   |             |                  |
|                    |               | backbone.                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| AreaLsaCount       | uint32        | The total number of link state | N/A         | N/A              |
|                    |               | advertisements in this area's  |             |                  |
|                    |               | link state database            |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| AsBdrRtrCount      | uint32        | The total number of Autonomous | N/A         | N/A              |
|                    |               | System Border Routers          |             |                  |
|                    |               | reachable within this area.    |             |                  |
|                    |               | This is initially zero and is  |             |                  |
|                    |               | calculated in each SPF pass.   |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SpfRuns            | uint32        | The number of times that the   | N/A         | N/A              |
|                    |               | intra-area route table has     |             |                  |
|                    |               | been calculated using this     |             |                  |
|                    |               | area's link state database.    |             |                  |
|                    |               |  This is typically done        |             |                  |
|                    |               | using Dijkstra's algorithm.    |             |                  |
|                    |               | Discontinuities in the value   |             |                  |
|                    |               | of this counter can occur      |             |                  |
|                    |               | at re-initialization of the    |             |                  |
|                    |               | management system              |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| AreaBdrRtrCount    | uint32        | The total number of Area       | N/A         | N/A              |
|                    |               | Border Routers reachable       |             |                  |
|                    |               | within this area.  This        |             |                  |
|                    |               | is initially zero and is       |             |                  |
|                    |               | calculated in each Shortest    |             |                  |
|                    |               | Path First (SPF) pass.         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/OspfAreaEntry
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/OspfAreaEntrys?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfAreaEntryState/<uuid>


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
		response, error = swtch.getOspfAreaEntryState(AreaId=areaid)

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
		response, error = swtch.getOspfAreaEntryStateById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfAreaEntryStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


