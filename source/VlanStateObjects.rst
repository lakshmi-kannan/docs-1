VlanState Object
=============================================================

*state/Vlan*
------------------------------------

- Multiple objects of this type can exist in a system.

+------------------------+---------------+--------------------------------+-------------+------------------+
|   **PARAMETER NAME**   | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+------------------------+---------------+--------------------------------+-------------+------------------+
| VlanId **[KEY]**       | int32         | 802.1Q tag/Vlan ID for vlan    | N/A         | N/A              |
|                        |               | being provisioned              |             |                  |
+------------------------+---------------+--------------------------------+-------------+------------------+
| IfIndex                | int32         | System assigned interface id   | N/A         | N/A              |
|                        |               | for this vlan interface        |             |                  |
+------------------------+---------------+--------------------------------+-------------+------------------+
| OperState              | string        | Operational state of vlan      | N/A         | N/A              |
|                        |               | interface                      |             |                  |
+------------------------+---------------+--------------------------------+-------------+------------------+
| SysInternalDescription | string        | This is a system generated     | N/A         | N/A              |
|                        |               | string that explains the       |             |                  |
|                        |               | operstate value                |             |                  |
+------------------------+---------------+--------------------------------+-------------+------------------+
| VlanName               | string        | System assigned vlan name      | N/A         | N/A              |
+------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/Vlan
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/Vlans?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/VlanState/<uuid>


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
		response, error = swtch.getVlanState(VlanId=vlanid)

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
		response, error = swtch.getVlanStateById(ObjectId=objectid)

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
		response, error = swtch.getAllVlanStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


