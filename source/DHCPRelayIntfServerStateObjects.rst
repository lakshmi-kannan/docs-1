DHCPRelayIntfServerState Object
=============================================================

*state/DHCPRelayIntfServer*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IntfRef **[KEY]**  | string        | Interface Index for which      | N/A         | N/A              |
|                    |               | state is required to be        |             |                  |
|                    |               | collected                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerIp **[KEY]** | string        | Server IP on the interface for | N/A         | N/A              |
|                    |               | which state is required to be  |             |                  |
|                    |               | collected                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Request            | int32         | Total number of requests to    | N/A         | N/A              |
|                    |               | Server                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Responses          | int32         | Total number of responses from | N/A         | N/A              |
|                    |               | Server                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/DHCPRelayIntfServer
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/DHCPRelayIntfServerState/<uuid>


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
		response, error = swtch.getDHCPRelayIntfServerState(IntfRef=intfref, ServerIp=serverip)

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
		response, error = swtch.getDHCPRelayIntfServerStateById(ObjectId=objectid)

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
		response, error = swtch.getAllDHCPRelayIntfServerStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


