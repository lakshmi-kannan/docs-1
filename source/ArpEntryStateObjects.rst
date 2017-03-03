ArpEntryState Object
=============================================================

*state/ArpEntry*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IpAddr **[KEY]**   | string        | Neighbor's IP Address          | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Vlan               | string        | Vlan ID of the Router          | N/A         | N/A              |
|                    |               | Interface to which neighbor is |             |                  |
|                    |               | attached to                    |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ExpiryTimeLeft     | string        | Time left before entry expires | N/A         | N/A              |
|                    |               | in case neighbor departs       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Intf               | string        | Router Interface to which      | N/A         | N/A              |
|                    |               | neighbor is attached to        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| MacAddr            | string        | MAC address of the neighbor    | N/A         | N/A              |
|                    |               | machine with corresponding IP  |             |                  |
|                    |               | Address                        |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/ArpEntry
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/ArpEntrys?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/ArpEntryState/<uuid>


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
		response, error = swtch.getArpEntryState(IpAddr=ipaddr)

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
		response, error = swtch.getArpEntryStateById(ObjectId=objectid)

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
		response, error = swtch.getAllArpEntryStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


