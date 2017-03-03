VxlanInstanceState Object
=============================================================

*state/VxlanInstance*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Vni **[KEY]**      | uint32        | VXLAN Network Id               | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OperState          | string        | Operational state of VXLAN     | DOWN        | UP, DOWN         |
|                    |               | layer                          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| VlanId             | uint16        | Vlan associated with the       | N/A         | N/A              |
|                    |               | Access targets.  Used in       |             |                  |
|                    |               | conjunction with a given VTEP  |             |                  |
|                    |               | inner-vlan-handling-mode       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/VxlanInstance
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/VxlanInstances?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/VxlanInstanceState/<uuid>


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
		response, error = swtch.getVxlanInstanceState(Vni=vni)

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
		response, error = swtch.getVxlanInstanceStateById(ObjectId=objectid)

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
		response, error = swtch.getAllVxlanInstanceStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


