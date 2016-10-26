StpBridgeInstanceState Object
=============================================================

*state/StpBridgeInstance*
------------------------------------

- Multiple objects of this type can exist in a system.

+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
|   **PARAMETER NAME**    | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| Vlan **[KEY]**          | uint16        | Each bridge is associated      | N/A         | N/A                            |
|                         |               | with a domain.  Typically this |             |                                |
|                         |               | domain is represented as the   |             |                                |
|                         |               | vlan; The default domain is    |             |                                |
|                         |               | typically 1                    |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| DesignatedRoot          | string        | The bridge identifier of the   | N/A         | N/A                            |
|                         |               | root of the spanning tree as   |             |                                |
|                         |               | determined by the Spanning     |             |                                |
|                         |               | Tree Protocol as executed      |             |                                |
|                         |               | by this node.  This value is   |             |                                |
|                         |               | used as the Root Identifier    |             |                                |
|                         |               | parameter in all Configuration |             |                                |
|                         |               | Bridge PDUs originated by this |             |                                |
|                         |               | node.                          |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| HelloTime               | int32         | The amount of time between the | N/A         | N/A                            |
|                         |               | transmission of Configuration  |             |                                |
|                         |               | bridge PDUs by this node on    |             |                                |
|                         |               | any port when it is the root   |             |                                |
|                         |               | of the spanning tree or trying |             |                                |
|                         |               | to become so in units of       |             |                                |
|                         |               | hundredths of a second.  This  |             |                                |
|                         |               | is the actual value that this  |             |                                |
|                         |               | bridge is currently using.     |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfIndex                 | int32         | The value of the instance of   | N/A         | N/A                            |
|                         |               | the ifIndex object for the     |             |                                |
|                         |               | bridge                         |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| MaxAge                  | int32         | The maximum age of Spanning    | N/A         | N/A                            |
|                         |               | Tree Protocol information      |             |                                |
|                         |               | learned from the network       |             |                                |
|                         |               | on any port before it          |             |                                |
|                         |               | is discarded in units of       |             |                                |
|                         |               | hundredths of a second.  This  |             |                                |
|                         |               | is the actual value that this  |             |                                |
|                         |               | bridge is currently using.     |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| RootPort                | int32         | The port number of the port    | N/A         | N/A                            |
|                         |               | that offers the lowest cost    |             |                                |
|                         |               | path from this bridge to the   |             |                                |
|                         |               | root bridge.                   |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TimeSinceTopologyChange | uint32        | The time (in hundredths of a   | N/A         | N/A                            |
|                         |               | second) since the last time a  |             |                                |
|                         |               | topology change was detected   |             |                                |
|                         |               | by the bridge entity. For RSTP |             |                                |
|                         |               | this reports the time since    |             |                                |
|                         |               | the tcWhile timer for any port |             |                                |
|                         |               | on this Bridge was nonzero.    |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TopChanges              | uint32        | The total number of topology   | N/A         | N/A                            |
|                         |               | changes detected by this       |             |                                |
|                         |               | bridge since the management    |             |                                |
|                         |               | entity was last reset or       |             |                                |
|                         |               | initialized.                   |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BridgeHelloTime         | int32         | The amount of time between the | N/A         | N/A                            |
|                         |               | transmission of Configuration  |             |                                |
|                         |               | bridge PDUs by this node on    |             |                                |
|                         |               | any port when it is the root   |             |                                |
|                         |               | of the spanning tree or trying |             |                                |
|                         |               | to become so in units of       |             |                                |
|                         |               | hundredths of a second.  This  |             |                                |
|                         |               | is the provisioned value of    |             |                                |
|                         |               | the local bridge   .           |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TxHoldCount             | int32         | TODO                           | N/A         | N/A                            |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| Priority                | int32         | The value of the write-able    | N/A         | N/A                            |
|                         |               | portion of the Bridge ID i.e.  |             |                                |
|                         |               | the first two octets of the    |             |                                |
|                         |               | 8 octet long Bridge ID.  The   |             |                                |
|                         |               | other last 6 octets of the     |             |                                |
|                         |               | Bridge ID are given by the     |             |                                |
|                         |               | value of Address. On bridges   |             |                                |
|                         |               | supporting IEEE 802.1t or IEEE |             |                                |
|                         |               | 802.1w permissible values are  |             |                                |
|                         |               | 0-61440 in steps of 4096.      |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| ProtocolSpecification   | int32         | An indication of what version  | N/A         | ieee8021d(3), unknown(1),      |
|                         |               | of the Spanning Tree Protocol  |             | decLb100(2)                    |
|                         |               | is being run.  The value       |             |                                |
|                         |               | 'decLb100(2)' indicates the    |             |                                |
|                         |               | DEC LANbridge 100 Spanning     |             |                                |
|                         |               | Tree protocol. IEEE 802.1D     |             |                                |
|                         |               | implementations will return    |             |                                |
|                         |               | 'ieee8021d(3)'. If future      |             |                                |
|                         |               | versions of the IEEE Spanning  |             |                                |
|                         |               | Tree Protocol that are         |             |                                |
|                         |               | incompatible with the current  |             |                                |
|                         |               | version are released a new     |             |                                |
|                         |               | value will be defined.         |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| HoldTime                | int32         | This time value determines     | N/A         | N/A                            |
|                         |               | the interval length during     |             |                                |
|                         |               | which no more than two         |             |                                |
|                         |               | Configuration bridge PDUs      |             |                                |
|                         |               | shall be transmitted by this   |             |                                |
|                         |               | node in units of hundredths of |             |                                |
|                         |               | a second.                      |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BridgeForwardDelay      | int32         | This time value measured       | N/A         | N/A                            |
|                         |               | in units of hundredths of      |             |                                |
|                         |               | a second controls how fast     |             |                                |
|                         |               | a port changes its spanning    |             |                                |
|                         |               | state when moving towards the  |             |                                |
|                         |               | Forwarding state.  The value   |             |                                |
|                         |               | determines how long the port   |             |                                |
|                         |               | stays in each of the Listening |             |                                |
|                         |               | and Learning states which      |             |                                |
|                         |               | precede the Forwarding state.  |             |                                |
|                         |               |  This value is also used       |             |                                |
|                         |               | when a topology change has     |             |                                |
|                         |               | been detected and is underway  |             |                                |
|                         |               | to age all dynamic entries     |             |                                |
|                         |               | in the Forwarding Database.    |             |                                |
|                         |               | [Note This is the provisioned  |             |                                |
|                         |               | value of the local bridge in   |             |                                |
|                         |               | contrast to ForwardDelay which |             |                                |
|                         |               | is the value that this bridge  |             |                                |
|                         |               | and all others would start     |             |                                |
|                         |               | using if/when this bridge were |             |                                |
|                         |               | to become the root.]           |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BridgeHoldTime          | int32         | This time value determines     | N/A         | N/A                            |
|                         |               | the interval length during     |             |                                |
|                         |               | which no more than two         |             |                                |
|                         |               | Configuration bridge PDUs      |             |                                |
|                         |               | shall be transmitted by this   |             |                                |
|                         |               | node in units of hundredths    |             |                                |
|                         |               | of a second. This is the       |             |                                |
|                         |               | provisioned value of the local |             |                                |
|                         |               | bridge                         |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| RootCost                | int32         | The cost of the path to the    | N/A         | N/A                            |
|                         |               | root as seen from this bridge. |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| Address                 | string        | The bridge identifier of the   | N/A         | N/A                            |
|                         |               | root of the spanning tree as   |             |                                |
|                         |               | determined by the Spanning     |             |                                |
|                         |               | Tree Protocol as executed      |             |                                |
|                         |               | by this node.  This value is   |             |                                |
|                         |               | used as the Root Identifier    |             |                                |
|                         |               | parameter in all Configuration |             |                                |
|                         |               | Bridge PDUs originated by this |             |                                |
|                         |               | node.                          |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| ForwardDelay            | int32         | This time value measured       | N/A         | N/A                            |
|                         |               | in units of hundredths of      |             |                                |
|                         |               | a second controls how fast     |             |                                |
|                         |               | a port changes its spanning    |             |                                |
|                         |               | state when moving towards the  |             |                                |
|                         |               | Forwarding state.  The value   |             |                                |
|                         |               | determines how long the port   |             |                                |
|                         |               | stays in each of the Listening |             |                                |
|                         |               | and Learning states which      |             |                                |
|                         |               | precede the Forwarding state.  |             |                                |
|                         |               |  This value is also used       |             |                                |
|                         |               | when a topology change has     |             |                                |
|                         |               | been detected and is underway  |             |                                |
|                         |               | to age all dynamic entries     |             |                                |
|                         |               | in the Forwarding Database.    |             |                                |
|                         |               | [Note that this value is       |             |                                |
|                         |               | the one that this bridge is    |             |                                |
|                         |               | currently using in contrast    |             |                                |
|                         |               | to ForwardDelay which is the   |             |                                |
|                         |               | value that this bridge and     |             |                                |
|                         |               | all others would start using   |             |                                |
|                         |               | if/when this bridge were to    |             |                                |
|                         |               | become the root.]              |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BridgeMaxAge            | int32         | The maximum age of Spanning    | N/A         | N/A                            |
|                         |               | Tree Protocol information      |             |                                |
|                         |               | learned from the network       |             |                                |
|                         |               | on any port before it          |             |                                |
|                         |               | is discarded in units of       |             |                                |
|                         |               | hundredths of a second.  This  |             |                                |
|                         |               | is the provisioned value of    |             |                                |
|                         |               | the local bridge.              |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/StpBridgeInstance
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/StpBridgeInstances?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/StpBridgeInstanceState/<uuid>


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
		response, error = swtch.getStpBridgeInstanceState(Vlan=vlan)

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
		response, error = swtch.getStpBridgeInstanceStateById(ObjectId=objectid)

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
		response, error = swtch.getAllStpBridgeInstanceStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


