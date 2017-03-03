PolicyDefinition Object
=============================================================

*config/PolicyDefinition*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+------------------------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** |        **DATA TYPE**         |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+------------------------------+--------------------------------+-------------+------------------+
| Name **[KEY]**     | string                       | Policy Name                    | N/A         | N/A              |
+--------------------+------------------------------+--------------------------------+-------------+------------------+
| MatchType          | string                       | Specifies whether to match     | all         | all, any         |
|                    |                              | all/any of the statements      |             |                  |
|                    |                              | within this policy             |             |                  |
+--------------------+------------------------------+--------------------------------+-------------+------------------+
| PolicyType         | string                       | Specifies the intended         | ALL         | BGP, OSPF, ALL   |
|                    |                              | protocol application for the   |             |                  |
|                    |                              | policy                         |             |                  |
+--------------------+------------------------------+--------------------------------+-------------+------------------+
| Priority           | int32                        | Priority of the policy w.r.t   | N/A         | N/A              |
|                    |                              | other policies configured      |             |                  |
+--------------------+------------------------------+--------------------------------+-------------+------------------+
| StatementList      | PolicyDefinitionStmtPriority | Specifies list of statements   | N/A         | N/A              |
|                    |                              | along with their precedence    |             |                  |
|                    |                              | order.                         |             |                  |
+--------------------+------------------------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/PolicyDefinition
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/PolicyDefinition/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/PolicyDefinitions?CurrentMarker=<x>\\&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/PolicyDefinition
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/PolicyDefinition
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/PolicyDefinition<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/PolicyDefinition
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/PolicyDefinition<uuid>


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
		response, error = swtch.getPolicyDefinition(Name=name)

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
		response, error = swtch.getPolicyDefinitionById(ObjectId=objectid)

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
		response, error = swtch.getAllPolicyDefinitions()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **CREATE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.createPolicyDefinition(Name=name, MatchType=matchtype, PolicyType=policytype, Priority=priority, StatementList=statementlist)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **DELETE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.deletePolicyDefinition(Name=name)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **DELETE By ID**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.deletePolicyDefinitionById(ObjectId=objectid

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **UPDATE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.updatePolicyDefinition(Name=name, MatchType=matchtype, PolicyType=policytype, Priority=priority, StatementList=statementlist)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **UPDATE By ID**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.updatePolicyDefinitionById(ObjectId=objectidMatchType=matchtype, PolicyType=policytype, Priority=priority, StatementList=statementlist)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
