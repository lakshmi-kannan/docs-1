OspfGlobalState Object
=============================================================

*state/OspfGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| RouterId **[KEY]** | string        | A 32-bit integer uniquely      | N/A         | N/A                            |
|                    |               | identifying the router in      |             |                                |
|                    |               | the Autonomous System. By      |             |                                |
|                    |               | convention                     |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| OpaqueLsaSupport   | bool          | The router's support for       | N/A         | N/A                            |
|                    |               | Opaque LSA types.              |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| RestartExitReason  | int32         | Describes the outcome of the   | N/A         | inProgress(2), none(1),        |
|                    |               | last attempt at a graceful     |             | timedOut(4), completed(3),     |
|                    |               | restart.  If the value is      |             | topologyChanged(5)             |
|                    |               | 'none'                         |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| VersionNumber      | int32         | The current version number of  | N/A         | version2(2)                    |
|                    |               | the OSPF protocol is 2.        |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AreaBdrRtrStatus   | bool          | A flag to note whether this    | N/A         | N/A                            |
|                    |               | router is an Area Border       |             |                                |
|                    |               | Router.                        |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| ExternLsaCount     | uint32        | The number of external         | N/A         | N/A                            |
|                    |               | (LS type-5) link state         |             |                                |
|                    |               | advertisements in the link     |             |                                |
|                    |               | state database.                |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/OspfGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfGlobalState/<uuid>


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
		response, error = swtch.getOspfGlobalState(RouterId=routerid)

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
		response, error = swtch.getOspfGlobalStateById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfGlobalStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


