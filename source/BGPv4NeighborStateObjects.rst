BGPv4NeighborState Object
=============================================================

*state/BGPv4Neighbor*
------------------------------------

- Multiple objects of this type can exist in a system.

+---------------------------+---------------+--------------------------------+-------------+------------------+
|    **PARAMETER NAME**     | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| NeighborAddress **[KEY]** | string        | Address of the BGP neighbor    | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| IntfRef **[KEY]**         | string        | Interface of the BGP neighbor  | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| TotalPrefixes             | uint32        | Total number of prefixes       | N/A         | N/A              |
|                           |               | received from the BGP neighbor |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AddPathsRx                | bool          | Receive additional paths from  | N/A         | N/A              |
|                           |               | BGP neighbor                   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| ConnectRetryTime          | uint32        | Connect retry time to          | N/A         | N/A              |
|                           |               | connect to BGP neighbor after  |             |                  |
|                           |               | disconnect                     |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| PeerAS                    | string        | Peer AS of the BGP neighbor    | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| PeerType                  | int8          | Type of the peer               | N/A         | N/A              |
|                           |               | (internal/external)            |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RouteReflectorClusterId   | uint32        | Cluster Id of the internal     | N/A         | N/A              |
|                           |               | BGP neighbor route reflector   |             |                  |
|                           |               | client                         |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| Queues                    | BGPQueues     | Input/Output size of BGP       | N/A         | N/A              |
|                           |               | packet queues                  |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| SessionState              | uint32        | Session state of the BGP       | N/A         | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| SessionStateDuration      | string        | Time duration for which this   | N/A         | N/A              |
|                           |               | neighbor is in the current     |             |                  |
|                           |               | session state.                 |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AdjRIBInFilter            | string        | Policy that is applied for     | N/A         | N/A              |
|                           |               | Adj-RIB-In prefix filtering    |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AuthPassword              | string        | Password to connect to the BGP | N/A         | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| Messages                  | BGPMessages   | Rx/Tx counter for BGP update   | N/A         | N/A              |
|                           |               | and notification packets       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| UpdateSource              | string        | Source IP to connect to the    | N/A         | N/A              |
|                           |               | BGP neighbor                   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| Disabled                  | bool          | Enable/Disable the BGP         | N/A         | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| LocalAS                   | string        | Local AS of the BGP neighbor   | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MultiHopEnable            | bool          | Enable/Disable multi hop for   | N/A         | N/A              |
|                           |               | BGP neighbor                   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| Description               | string        | Description of the BGP         | N/A         | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RouteReflectorClient      | bool          | Set/Clear BGP neighbor as a    | N/A         | N/A              |
|                           |               | route reflector client         |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| BfdNeighborState          | string        | BFD state of the BGP neighbor  | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| PeerGroup                 | string        | Peer group of the BGP neighbor | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| HoldTime                  | uint32        | Hold time for the BGP neighbor | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixes               | uint32        | Maximum number of prefixes     | N/A         | N/A              |
|                           |               | that can be received from the  |             |                  |
|                           |               | BGP neighbor                   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixesDisconnect     | bool          | Disconnect the BGP peer        | N/A         | N/A              |
|                           |               | session when we receive the    |             |                  |
|                           |               | max prefixes from the neighbor |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MultiHopTTL               | uint8         | TTL for multi hop BGP neighbor | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| NextHopSelf               | bool          | Use neighbor source IP as the  | N/A         | N/A              |
|                           |               | next hop for IBGP neighbors    |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AddPathsMaxTx             | uint8         | Max number of additional paths | N/A         | N/A              |
|                           |               | that can be transmitted to BGP |             |                  |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AdjRIBOutFilter           | string        | Policy that is applied for     | N/A         | N/A              |
|                           |               | Adj-RIB-Out prefix filtering   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| KeepaliveTime             | uint32        | Keep alive time for the BGP    | N/A         | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixesRestartTimer   | uint8         | Time to wait before we start   | N/A         | N/A              |
|                           |               | BGP peer session when we       |             |                  |
|                           |               | receive max prefixes           |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixesThresholdPct   | uint8         | The percentage of maximum      | N/A         | N/A              |
|                           |               | prefixes before we start       |             |                  |
|                           |               | logging                        |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/BGPv4Neighbor
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/BGPv4Neighbors?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BGPv4NeighborState/<uuid>


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
		response, error = swtch.getBGPv4NeighborState(NeighborAddress=neighboraddress, IntfRef=intfref)

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
		response, error = swtch.getBGPv4NeighborStateById(ObjectId=objectid)

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
		response, error = swtch.getAllBGPv4NeighborStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


