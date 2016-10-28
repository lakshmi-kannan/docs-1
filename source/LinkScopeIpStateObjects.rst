LinkScopeIpState Object
=============================================================

*state/LinkScopeIp*
------------------------------------

- Multiple objects of this type can exist in a system.

+-----------------------+---------------+--------------------------------+-------------+------------------+
|  **PARAMETER NAME**   | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| LinkScopeIp **[KEY]** | string        | Link scope IP Address          | N/A         | N/A              |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| Used                  | bool          | states whether the ip being    | N/A         | N/A              |
|                       |               | used                           |             |                  |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| IfIndex               | int32         | System Generated Unique        | N/A         | N/A              |
|                       |               | Interface Id                   |             |                  |
+-----------------------+---------------+--------------------------------+-------------+------------------+
| IntfRef               | string        | Interface where the link scope | N/A         | N/A              |
|                       |               | ip is configured               |             |                  |
+-----------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/LinkScopeIp
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/LinkScopeIps?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/LinkScopeIpState/<uuid>


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
		response, error = swtch.getLinkScopeIpState(LinkScopeIp=linkscopeip)

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
		response, error = swtch.getLinkScopeIpStateById(ObjectId=objectid)

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
		response, error = swtch.getAllLinkScopeIpStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


