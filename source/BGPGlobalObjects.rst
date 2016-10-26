BGPGlobal Object
=============================================================

*config/BGPGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+---------------------+------------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME**  |  **DATA TYPE**   |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+---------------------+------------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**       | string           | VRF id for BGP global config   | default     | N/A              |
+---------------------+------------------+--------------------------------+-------------+------------------+
| ASNum               | string           | Local AS for BGP global        |             | N/A              |
|                     |                  | config. Both AsPlain and AsDot |             |                  |
|                     |                  | formats are supported.         |             |                  |
+---------------------+------------------+--------------------------------+-------------+------------------+
| Disabled            | bool             | Enable/Disable BGP globally    | false       | N/A              |
+---------------------+------------------+--------------------------------+-------------+------------------+
| IBGPMaxPaths        | uint32           | Max ECMP paths from Internal   |           0 | N/A              |
|                     |                  | BGP neighbors                  |             |                  |
+---------------------+------------------+--------------------------------+-------------+------------------+
| RouterId            | string           | Router id for BGP global       | 0.0.0.0     | N/A              |
|                     |                  | config                         |             |                  |
+---------------------+------------------+--------------------------------+-------------+------------------+
| UseMultiplePaths    | bool             | Enable/disable ECMP for BGP    | false       | N/A              |
+---------------------+------------------+--------------------------------+-------------+------------------+
| EBGPAllowMultipleAS | bool             | Enable/diable ECMP paths from  | false       | N/A              |
|                     |                  | multiple ASes                  |             |                  |
+---------------------+------------------+--------------------------------+-------------+------------------+
| EBGPMaxPaths        | uint32           | Max ECMP paths from External   |           0 | N/A              |
|                     |                  | BGP neighbors                  |             |                  |
+---------------------+------------------+--------------------------------+-------------+------------------+
| Redistribution      | SourcePolicyList | Provide redistribution         | []          | N/A              |
|                     |                  | policies for BGP from          |             |                  |
|                     |                  | different sources              |             |                  |
+---------------------+------------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/BGPGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BGPGlobal/<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/BGPGlobal
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/BGPGlobal<uuid>


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
		response, error = swtch.getBGPGlobal(Vrf=vrf)

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
		response, error = swtch.getBGPGlobalById(ObjectId=objectid)

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
		response, error = swtch.getAllBGPGlobals()

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
		response, error = swtch.updateBGPGlobal(Vrf=vrf, ASNum=asnum, Disabled=disabled, IBGPMaxPaths=ibgpmaxpaths, RouterId=routerid, UseMultiplePaths=usemultiplepaths, EBGPAllowMultipleAS=ebgpallowmultipleas, EBGPMaxPaths=ebgpmaxpaths, Redistribution=redistribution)

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
		response, error = swtch.updateBGPGlobalById(ObjectId=objectidASNum=asnum, Disabled=disabled, IBGPMaxPaths=ibgpmaxpaths, RouterId=routerid, UseMultiplePaths=usemultiplepaths, EBGPAllowMultipleAS=ebgpallowmultipleas, EBGPMaxPaths=ebgpmaxpaths, Redistribution=redistribution)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
