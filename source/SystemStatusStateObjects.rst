SystemStatusState Object
=============================================================

*state/SystemStatus*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Name **[KEY]**     | string        | Name of the system             | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumActionCalls     | string        | Number of action api calls     | N/A         | N/A              |
|                    |               | made                           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumCreateCalls     | string        | Number of create api calls     | N/A         | N/A              |
|                    |               | made                           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumGetCalls        | string        | Number of get api calls made   | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| UpTime             | string        | Uptime of this system          | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| FlexDaemons        | DaemonState   | Daemon states                  | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumDeleteCalls     | string        | Number of delete api calls     | N/A         | N/A              |
|                    |               | made                           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| NumUpdateCalls     | string        | Number of update api calls     | N/A         | N/A              |
|                    |               | made                           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Ready              | bool          | System is ready to accept api  | N/A         | N/A              |
|                    |               | calls                          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Reason             | string        | Reason if system not ready     | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/SystemStatus
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/SystemStatusState/<uuid>


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
		response, error = swtch.getSystemStatusState(Name=name)

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
		response, error = swtch.getSystemStatusStateById(ObjectId=objectid)

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
		response, error = swtch.getAllSystemStatusStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


