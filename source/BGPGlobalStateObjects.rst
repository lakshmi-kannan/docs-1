BGPGlobalState Object
=============================================================

*state/BGPGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+---------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME**  | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+---------------------+---------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**       | string        | VRF id for BGP global config   | N/A         | N/A              |
+---------------------+---------------+--------------------------------+-------------+------------------+
| Totalv6Prefixes     | uint32        | Total number of IPv6           | N/A         | N/A              |
|                     |               | destinations received from     |             |                  |
|                     |               | neighbors                      |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+
| Disabled            | bool          | Enable/Disable BGP globally    | N/A         | N/A              |
+---------------------+---------------+--------------------------------+-------------+------------------+
| EBGPAllowMultipleAS | bool          | Enable/diable ECMP paths from  | N/A         | N/A              |
|                     |               | multiple ASes                  |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+
| Totalv4Prefixes     | uint32        | Total number of IPv4           | N/A         | N/A              |
|                     |               | destinations received from     |             |                  |
|                     |               | neighbors                      |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+
| RouterId            | string        | Router id for BGP global       | N/A         | N/A              |
|                     |               | config                         |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+
| TotalPaths          | uint32        | Total number of paths received | N/A         | N/A              |
|                     |               | from neighbors                 |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+
| UseMultiplePaths    | bool          | Enable/disable ECMP for BGP    | N/A         | N/A              |
+---------------------+---------------+--------------------------------+-------------+------------------+
| AS                  | string        | Local AS for BGP global config | N/A         | N/A              |
+---------------------+---------------+--------------------------------+-------------+------------------+
| EBGPMaxPaths        | uint32        | Max ECMP paths from External   | N/A         | N/A              |
|                     |               | BGP neighbors                  |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+
| IBGPMaxPaths        | uint32        | Max ECMP paths from Internal   | N/A         | N/A              |
|                     |               | BGP neighbors                  |             |                  |
+---------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/BGPGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BGPGlobalState/<uuid>


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
		response, error = swtch.getBGPGlobalState(Vrf=vrf)

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
		response, error = swtch.getBGPGlobalStateById(ObjectId=objectid)

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
		response, error = swtch.getAllBGPGlobalStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


