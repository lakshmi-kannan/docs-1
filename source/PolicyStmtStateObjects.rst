PolicyStmtState Object
=============================================================

*state/PolicyStmt*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Name **[KEY]**     | string        | PolicyStmtState                | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| PolicyList         | string        | List of policies using this    | N/A         | N/A              |
|                    |               | policy statement               |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Action             | string        | Action corresponding to this   | N/A         | N/A              |
|                    |               | policy statement               |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Conditions         | string        | List of conditions added to    | N/A         | N/A              |
|                    |               | this policy statement          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| MatchConditions    | string        | Specifies whether to match     | N/A         | N/A              |
|                    |               | all/any of the conditions of   |             |                  |
|                    |               | this policy statement          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/PolicyStmt
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/PolicyStmts?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/PolicyStmtState/<uuid>


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
		response, error = swtch.getPolicyStmtState(Name=name)

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
		response, error = swtch.getPolicyStmtStateById(ObjectId=objectid)

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
		response, error = swtch.getAllPolicyStmtStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


