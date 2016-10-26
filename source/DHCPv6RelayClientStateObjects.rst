DHCPv6RelayClientState Object
=============================================================

*state/DHCPv6RelayClient*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| MacAddr **[KEY]**  | string        | Host Hardware/Mac Address      | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientInfoRequest  | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client info-request message    |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientRequests     | int32         | Total Number of client request | N/A         | N/A              |
|                    |               | message relayed to server      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientSolicit      | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client solicit message to dhcp |             |                  |
|                    |               | server                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| GatewayIp          | string        | Ip Address which client needs  | N/A         | N/A              |
|                    |               | to use                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| AcceptedIp         | string        | Ip Address which client        | N/A         | N/A              |
|                    |               | accepted                       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientDecline      | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client decline message         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientRequest      | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client request message         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OfferedIp          | string        | Ip Address offered by DHCP     | N/A         | N/A              |
|                    |               | Server                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerAdvertise    | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | server advertise message       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerReconfigure  | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | server reconfigure message     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerRequests     | int32         | Total Number of requests       | N/A         | N/A              |
|                    |               | relayed to server              |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientConfirm      | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client confirm message to dhcp |             |                  |
|                    |               | server                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientRebind       | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client rebind message to dhcp  |             |                  |
|                    |               | server                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientRelease      | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client release message         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientResponses    | int32         | Total Number of server         | N/A         | N/A              |
|                    |               | response relayed to client     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RequestedIp        | string        | Ip Address request from client | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerIp           | string        | Configured DHCP Server         | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ClientRenew        | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | client renew message to dhcp   |             |                  |
|                    |               | server                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerReply        | string        | Most recent time stamp of      | N/A         | N/A              |
|                    |               | server reply message           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| ServerResponses    | int32         | Total Number of responses      | N/A         | N/A              |
|                    |               | received from server           |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/DHCPv6RelayClient
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/DHCPv6RelayClients?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/DHCPv6RelayClientState/<uuid>


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
		response, error = swtch.getDHCPv6RelayClientState(MacAddr=macaddr)

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
		response, error = swtch.getDHCPv6RelayClientStateById(ObjectId=objectid)

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
		response, error = swtch.getAllDHCPv6RelayClientStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


