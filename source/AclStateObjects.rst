AclState Object
=============================================================

*state/Acl*
------------------------------------

- Multiple objects of this type can exist in a system.

+---------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME**  | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+---------------------+---------------+--------------------------------+-------------+------------------+
| AclName **[KEY]**   | string        | Acl name to be used to refer   | N/A         | N/A              |
|                     |               | to this ACL                    |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+
| Direction **[KEY]** | string        |                                | N/A         | N/A              |
+---------------------+---------------+--------------------------------+-------------+------------------+
| RuleNameList        | string        | List of acl rules  to be       | N/A         | N/A              |
|                     |               | applied to this ACL. This      |             |                  |
|                     |               | should match with Acl rule key |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+
| IntfList            | string        | list of IntfRef can be         | N/A         | N/A              |
|                     |               | port/lag object                |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/Acl
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/Acls?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/AclState/<uuid>


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
		response, error = swtch.getAclState(AclName=aclname, Direction=direction)

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
		response, error = swtch.getAclStateById(ObjectId=objectid)

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
		response, error = swtch.getAllAclStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


