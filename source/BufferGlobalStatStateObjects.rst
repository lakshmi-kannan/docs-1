BufferGlobalStatState Object
=============================================================

*state/BufferGlobalStat*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+-----------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |       **DESCRIPTION**       | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+-----------------------------+-------------+------------------+
| DeviceId **[KEY]** | uint32        | Device id                   | N/A         | N/A              |
+--------------------+---------------+-----------------------------+-------------+------------------+
| IngressBufferStat  | uint64        | Ingress buffer stats        | N/A         | N/A              |
+--------------------+---------------+-----------------------------+-------------+------------------+
| BufferStat         | uint64        | Buffer stats for the device | N/A         | N/A              |
+--------------------+---------------+-----------------------------+-------------+------------------+
| EgressBufferStat   | uint64        | Egress Buffer stats         | N/A         | N/A              |
+--------------------+---------------+-----------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/BufferGlobalStat
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/BufferGlobalStats?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BufferGlobalStatState/<uuid>


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
		response, error = swtch.getBufferGlobalStatState(DeviceId=deviceid)

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
		response, error = swtch.getBufferGlobalStatStateById(ObjectId=objectid)

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
		response, error = swtch.getAllBufferGlobalStatStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


