DaemonState Object
=============================================================

*state/Daemon*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Name **[KEY]**     | string        | Daemon name                    | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| State              | string        | State of the daemon            | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Enable             | bool          | If the daemon configured to be | N/A         | N/A              |
|                    |               | enabled                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| StartTime          | string        | Daemon start time              | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Reason             | string        | Reason for current state of    | N/A         | N/A              |
|                    |               | the daemon                     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RestartCount       | int32         | Number of times this daemon    | N/A         | N/A              |
|                    |               | has been restarted             |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RestartReason      | string        | Last restart reason            | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RestartTime        | string        | Last restart time              | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| KeepAlive          | string        | KeepAlive state of the daemon  | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/Daemon
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/Daemons?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/DaemonState/<uuid>


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
		response, error = swtch.getDaemonState(Name=name)

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
		response, error = swtch.getDaemonStateById(ObjectId=objectid)

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
		response, error = swtch.getAllDaemonStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


