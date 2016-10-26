ConfigLogState Object
=============================================================

*state/ConfigLog*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| API **[KEY]**      | string        | Name of the API called         | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SeqNum **[KEY]**   | uint32        | Sequence number of the API     | N/A         | N/A              |
|                    |               | call                           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Time **[KEY]**     | string        | When the API was called        | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Data               | string        | User provided data             | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Operation          | string        | Oprtation executed on this API | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Result             | string        | Result of the API call         | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| UserAddr           | string        | Host address from where the    | N/A         | N/A              |
|                    |               | call was made                  |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| UserName           | string        | User who made the call         | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/ConfigLog
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/ConfigLogs?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/ConfigLogState/<uuid>


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
		response, error = swtch.getConfigLogState(API=api, SeqNum=seqnum, Time=time)

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
		response, error = swtch.getConfigLogStateById(ObjectId=objectid)

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
		response, error = swtch.getAllConfigLogStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


