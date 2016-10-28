BfdSessionState Object
=============================================================

*state/BfdSession*
------------------------------------

- Multiple objects of this type can exist in a system.

+---------------------------+---------------+--------------------------------+-------------+------------------+
|    **PARAMETER NAME**     | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| IpAddr **[KEY]**          | string        | Neighbor IP address            | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| NumRxPackets              | uint32        | Number of control packets      | N/A         | N/A              |
|                           |               | received                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RegisteredProtocols       | string        | Registered owners              | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RemoteSessionState        | string        | Neighbor state                 | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| SentAuthSeq               | uint32        | Sent authentication sequence   | N/A         | N/A              |
|                           |               | number                         |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| SessionId                 | int32         | Session index                  | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AuthSeqKnown              | bool          | Authentication sequence known  | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| NumTxPackets              | uint32        | Number of control packets sent | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| InterfaceSpecific         | bool          | This session is tied to an     | N/A         | N/A              |
|                           |               | interface                      |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| LocalMacAddr              | string        | My MAC address                 | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| PerLinkSession            | bool          | This is a perlink session on   | N/A         | N/A              |
|                           |               | LAG                            |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| ReceivedAuthSeq           | uint32        | Received authentication        | N/A         | N/A              |
|                           |               | sequence number                |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RemoteDiscriminator       | uint32        | Neighbor discriminator         | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RemoteDemandMode          | bool          | Neighbor demand mode           | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RequiredMinRxInterval     | string        | My required minimum rx         | N/A         | N/A              |
|                           |               | interval                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| UpDuration                | string        | Duration of this session in up | N/A         | N/A              |
|                           |               | state                          |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| DetectionMultiplier       | uint32        | My detection multiplier        | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| LocalDiscriminator        | uint32        | My discriminator               | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RemoteMacAddr             | string        | Neighbor MAC address           | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RemoteMinRxInterval       | string        | Neighbor minimum rx interval   | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| SessionState              | string        | My state                       | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| DesiredMinTxInterval      | string        | My desired minimum tx interval | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| LocalDiagType             | string        | My diagnostic                  | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| ParamName                 | string        | Session parameters config      | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RemoteDetectionMultiplier | uint32        | Neighbor detection multiplier  | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| ToDownCount               | uint32        | Number of times this session   | N/A         | N/A              |
|                           |               | have moved to down state       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| ToUpCount                 | uint32        | Number of times this session   | N/A         | N/A              |
|                           |               | have moved to up state         |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AuthType                  | string        | My Authentication type         | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| DemandMode                | bool          | My demand mode                 | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| IntfRef                   | string        | Interface on which this        | N/A         | N/A              |
|                           |               | session is running             |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/BfdSession
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/BfdSessions?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BfdSessionState/<uuid>


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
		response, error = swtch.getBfdSessionState(IpAddr=ipaddr)

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
		response, error = swtch.getBfdSessionStateById(ObjectId=objectid)

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
		response, error = swtch.getAllBfdSessionStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


