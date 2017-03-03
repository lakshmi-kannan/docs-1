ArpLinuxEntryState Object
=============================================================

*state/ArpLinuxEntry*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+-------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |     **DESCRIPTION**     | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+-------------------------+-------------+------------------+
| IpAddr **[KEY]**   | string        | Neighbor's IP Address   | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| HWType             | string        | Hardware Type           | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| IfName             | string        | Interface name          | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+
| MacAddr            | string        | MAC address of neighbor | N/A         | N/A              |
+--------------------+---------------+-------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/ArpLinuxEntry
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/ArpLinuxEntrys?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/ArpLinuxEntryState/<uuid>


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
		response, error = swtch.getArpLinuxEntryState(IpAddr=ipaddr)

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
		response, error = swtch.getArpLinuxEntryStateById(ObjectId=objectid)

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
		response, error = swtch.getAllArpLinuxEntryStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


