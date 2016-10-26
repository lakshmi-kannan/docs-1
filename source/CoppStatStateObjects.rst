CoppStatState Object
=============================================================

*state/CoppStat*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Protocol **[KEY]** | string        | Protocol type for which CoPP   | N/A         | N/A              |
|                    |               | is configured.                 |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RedPackets         | int64         | Dropped packets. Packets       | N/A         | N/A              |
|                    |               | marked with red for tri color  |             |                  |
|                    |               | policer.                       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| BurstRate          | int32         | Burst rate (packets) for       | N/A         | N/A              |
|                    |               | policer.                       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| GreenPackets       | int64         | Packets marked with green for  | N/A         | N/A              |
|                    |               | tri color policer.             |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| PeakRate           | int32         | Peak rate (packets) for        | N/A         | N/A              |
|                    |               | policer.                       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/CoppStat
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/CoppStats?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/CoppStatState/<uuid>


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
		response, error = swtch.getCoppStatState(Protocol=protocol)

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
		response, error = swtch.getCoppStatStateById(ObjectId=objectid)

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
		response, error = swtch.getAllCoppStatStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


