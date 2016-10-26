DHCPRelayClientState Object
=============================================================

*state/DHCPRelayClient*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| MacAddr **[KEY]**  | string        | Host Hardware/Mac Address      | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OfferedIp          | string        | Ip Address offered by DHCP     | N/A         | N/A              |
|                    |               | Server                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RequestedIp        | string        | Ip Address request from client | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerOffer        | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | server offer message           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerResponses    | int32         | Total Number of responses      | N/A         | N/A              |
|                    |               | received from server           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| AcceptedIp         | string        | Ip Address which client        | N/A         | N/A              |
|                    |               | accepted                       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientResponses    | int32         | Total Number of server         | N/A         | N/A              |
|                    |               | response relayed to client     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| GatewayIp          | string        | Ip Address which client needs  | N/A         | N/A              |
|                    |               | to use                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientRequests     | int32         | Total Number of client request | N/A         | N/A              |
|                    |               | message relayed to server      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerIp           | string        | Configured DHCP Server         | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerRequests     | int32         | Total Number of requests       | N/A         | N/A              |
|                    |               | relayed to server              |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientDiscover     | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client discover message to     |             |                  |
|                    |               | dhcp server                    |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientRequest      | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client request message         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerAck          | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | server ack message             |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/DHCPRelayClient
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/DHCPRelayClients?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/DHCPRelayClientState/<uuid>


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
		response, error = swtch.getDHCPRelayClientState(MacAddr=macaddr)

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
		response, error = swtch.getDHCPRelayClientStateById(ObjectId=objectid)

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
		response, error = swtch.getAllDHCPRelayClientStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


