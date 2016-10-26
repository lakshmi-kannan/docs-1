DHCPv6RelayIntfState Object
=============================================================

*state/DHCPv6RelayIntf*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IntfRef **[KEY]**  | string        | Interface for which state is   | N/A         | N/A              |
|                    |               | required to be collected       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| TotalDhcpServerRx  | int32         | Total number of server         | N/A         | N/A              |
|                    |               | requests made by relay agent   |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| TotalDhcpServerTx  | int32         | Total number of server         | N/A         | N/A              |
|                    |               | responses received by relay    |             |                  |
|                    |               | agent                          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| TotalDrops         | int32         | Total number of DHCP Packets   | N/A         | N/A              |
|                    |               | dropped by relay agent         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| TotalDhcpClientRx  | int32         | Total number of client         | N/A         | N/A              |
|                    |               | requests that came to relay    |             |                  |
|                    |               | agent                          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| TotalDhcpClientTx  | int32         | Total number of client         | N/A         | N/A              |
|                    |               | responses send out by relay    |             |                  |
|                    |               | agent                          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/DHCPv6RelayIntf
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/DHCPv6RelayIntfs?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/DHCPv6RelayIntfState/<uuid>


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
		response, error = swtch.getDHCPv6RelayIntfState(IntfRef=intfref)

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
		response, error = swtch.getDHCPv6RelayIntfStateById(ObjectId=objectid)

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
		response, error = swtch.getAllDHCPv6RelayIntfStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


