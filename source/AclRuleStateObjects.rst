AclRuleState Object
=============================================================

*state/AclRule*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RuleName **[KEY]** | string        | Acl rule name                  | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| AclType            | string        | Type can be IP/MAC/SVI         | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| HitCount           | uint64        | No of  packets hit the rule if | N/A         | N/A              |
|                    |               | applied.                       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| HwPresence         | string        | Check if the rule is installed | N/A         | N/A              |
|                    |               | in hardware. Applied/Not       |             |                  |
|                    |               | Applied/Failed                 |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IntfList           | string        | list of IntfRef can be         | N/A         | N/A              |
|                    |               | port/lag object                |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/AclRule
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/AclRules?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/AclRuleState/<uuid>


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
		response, error = swtch.getAclRuleState(RuleName=rulename)

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
		response, error = swtch.getAclRuleStateById(ObjectId=objectid)

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
		response, error = swtch.getAllAclRuleStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


