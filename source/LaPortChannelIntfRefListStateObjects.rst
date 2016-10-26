LaPortChannelIntfRefListState Object
=============================================================

*state/LaPortChannelIntfRefList*
------------------------------------

- Multiple objects of this type can exist in a system.

+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
|     **PARAMETER NAME**     | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |             **VALID VALUES**              |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| IntfRef **[KEY]**          | string        | Reference to aggregate member  | N/A         | N/A                                       |
|                            |               | interface                      |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LampInPdu                  | uint64        | Number of LAMPDU received      | N/A         | N/A                                       |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LampOutPdu                 | uint64        | Number of LAMPDU transmited    | N/A         | N/A                                       |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| OperKey                    | uint16        | Current operational value      | N/A         | N/A                                       |
|                            |               | of the key for the aggregate   |             |                                           |
|                            |               | interface                      |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| OperState                  | string        | The operation state            | N/A         | N/A                                       |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| PartnerCdsChurnCount       | uint64        | If supported the number        | N/A         | N/A                                       |
|                            |               | of times the Actor CDS         |             |                                           |
|                            |               | Churn state has entered the    |             |                                           |
|                            |               | ACTOR_CDS_CHURN state          |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| PartnerChangeCount         | uint64        | Number of times the Partners   | N/A         | N/A                                       |
|                            |               | perception of the LAG ID for   |             |                                           |
|                            |               | the  Aggregation Port has      |             |                                           |
|                            |               | changed.                       |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| Timeout                    | int32         | The timeout type (short or     | N/A         | SHORT(1), LONG(0)                         |
|                            |               | long) used by the participant  |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| Activity                   | int32         | Indicates participant is       | N/A         | ACTIVE(0), PASSIVE(1)                     |
|                            |               | active or passive              |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| DrniName                   | string        | Defines the Lag is owned by    | N/A         | N/A                                       |
|                            |               | the Distributed Relay Object   |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LacpInMissMatchPkts        | uint64        | Numeer of LACPDU which are     | N/A         | N/A                                       |
|                            |               | received with mismatched info  |             |                                           |
|                            |               | from Peer                      |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LampOutResponsePdu         | uint64        | Number of LAMPDU Response      | N/A         | N/A                                       |
|                            |               | received                       |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| PartnerChurnCount          | uint64        | Number of times the Partner    | N/A         | N/A                                       |
|                            |               | State machine has entered the  |             |                                           |
|                            |               | ACTOR_CHURN state              |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| Synchronization            | int32         | Indicates whether the          | N/A         | OUT_SYNC(1), IN_SYNC(0)                   |
|                            |               | participant is in-sync or      |             |                                           |
|                            |               | out-of-sync                    |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| MuxMachine                 | int32         | Current MUX Machine State      | N/A         | MUX_COLLECTING(3),                        |
|                            |               |                                |             | MUX_COLLECTING_DISTRIBUTING_DEFAULTED(7), |
|                            |               |                                |             | MUX_COLLECTING_DISTRIBUTING(5),           |
|                            |               |                                |             | MUX_DISTRIBUTING_DEFAULTED(6),            |
|                            |               |                                |             | MUX_ATTACHED(2), MUX_DETACHED(0),         |
|                            |               |                                |             | MUX_DISTRIBUTING(4), MUX_WAITING(1)       |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| MuxReason                  | string        | Reason for the most recent MUX | N/A         | N/A                                       |
|                            |               | state change                   |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| PartnerId                  | string        | MAC address representing the   | N/A         | [0-9a-fA-F]{2}(                           |
|                            |               | protocol partners interface    |             |                                           |
|                            |               | system ID                      |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| PartnerSyncTransitionCount | uint64        | Number of times the Partners   | N/A         | N/A                                       |
|                            |               | Mux state machine has entered  |             |                                           |
|                            |               | the  IN_SYNC state.            |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| ActorChurnMachine          | int32         | Actor Churn Detection Machine  | N/A         | CHURN_NO_CHURN(0), CHURN_CHURN(1)         |
|                            |               | State                          |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| DebugId                    | uint32        | Debug Information Id           | N/A         | N/A                                       |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LagIntfRef                 | string        | Id of the lag group to which   | N/A         | N/A                                       |
|                            |               | this port is associated with   |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| PartnerCdsChurnMachine     | int32         | If supported Partner CDS Churn | N/A         | CHURN_NO_CHURN(0), CHURN_CHURN(1)         |
|                            |               | Machine State                  |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| PartnerChurnMachine        | int32         | Partner Churn Detection        | N/A         | CHURN_NO_CHURN(0), CHURN_CHURN(1)         |
|                            |               | Machine State                  |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| Collecting                 | bool          | If true                        | N/A         | N/A                                       |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LacpInPkts                 | uint64        | Number of LACPDUs received     | N/A         | N/A                                       |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| RxMachine                  | int32         | Current Rx Machine State       | N/A         | RX_CURRENT(0), RX_PORT_DISABLE(5),        |
|                            |               |                                |             | RX_DEFAULTED(2), RX_LACP_DISABLED(4),     |
|                            |               |                                |             | RX_EXPIRED(1), RX_INITIALIZE(3)           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| ActorCdsChurnMachine       | int32         | If supported Actor CDS Churn   | N/A         | CHURN_NO_CHURN(0), CHURN_CHURN(1)         |
|                            |               | Machine State                  |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| ActorSyncTransitionCount   | uint64        | Number of times the Actors Mux | N/A         | N/A                                       |
|                            |               | state machine has entered the  |             |                                           |
|                            |               | IN_SYNC state.                 |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LacpErrors                 | uint64        | Number of LACPDU Errors; sum   | N/A         | N/A                                       |
|                            |               | of all Rx Errors               |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LacpOutPkts                | uint64        | Number of LACPDUs transmitted  | N/A         | N/A                                       |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LacpUnknownErrors          | uint64        | Carry the Slow Protocols       | N/A         | N/A                                       |
|                            |               | Ethernet Type value (IEEE Std  |             |                                           |
|                            |               | 802.3-2008                     |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LampInResponsePdu          | uint64        | Number of LAMPDU Response      | N/A         | N/A                                       |
|                            |               | received                       |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| ActorChurnCount            | uint64        | Number of times the Actor      | N/A         | N/A                                       |
|                            |               | State machine has entered the  |             |                                           |
|                            |               | ACTOR_CHURN state              |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| Defaulted                  | bool          | When no partner information is | N/A         | N/A                                       |
|                            |               | exchanged port will come up in |             |                                           |
|                            |               | a defaulted state              |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| IfIndex                    | int32         | Interface member of the LACP   | N/A         | N/A                                       |
|                            |               | aggregate                      |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| PartnerKey                 | uint16        | Operational value of the       | N/A         | N/A                                       |
|                            |               | protocol partners key          |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| RxTime                     | uint32        | Time at which the last LACPDU  | N/A         | N/A                                       |
|                            |               | was received by a given port   |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| ActorCdsChurnCount         | uint64        | If supported the number        | N/A         | N/A                                       |
|                            |               | of times the Actor CDS         |             |                                           |
|                            |               | Churn state has entered the    |             |                                           |
|                            |               | ACTOR_CDS_CHURN state          |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| ActorChangeCount           | uint64        | Number of times the Actors     | N/A         | N/A                                       |
|                            |               | perception of the LAG ID for   |             |                                           |
|                            |               | the  Aggregation Port has      |             |                                           |
|                            |               | changed.                       |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| Aggregatable               | bool          | A true value indicates that    | N/A         | N/A                                       |
|                            |               | the participant will allow     |             |                                           |
|                            |               | the link to be used as part of |             |                                           |
|                            |               | the aggregate. A false value   |             |                                           |
|                            |               | indicates the link should be   |             |                                           |
|                            |               | used as an individual link     |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| Distributing               | bool          | When true                      | N/A         | N/A                                       |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| DrniSynced                 | bool          | Identify that the Distributed  | N/A         | N/A                                       |
|                            |               | Relay is in sync with neighbor |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LacpRxErrors               | uint64        | The number of frames received  | N/A         | N/A                                       |
|                            |               | that carry the Slow Protocols  |             |                                           |
|                            |               | Ethernet Type value (IEEE Std  |             |                                           |
|                            |               | 802.3-2008                     |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| LacpTxErrors               | uint64        | Number of LACPDU transmit      | N/A         | N/A                                       |
|                            |               | packet errors                  |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+
| SystemId                   | string        | MAC address that defines       | N/A         | [0-9a-fA-F]{2}(                           |
|                            |               | the local system ID for the    |             |                                           |
|                            |               | aggregate interface            |             |                                           |
+----------------------------+---------------+--------------------------------+-------------+-------------------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/LaPortChannelIntfRefList
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/LaPortChannelIntfRefLists?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/LaPortChannelIntfRefListState/<uuid>


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
		response, error = swtch.getLaPortChannelIntfRefListState(IntfRef=intfref)

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
		response, error = swtch.getLaPortChannelIntfRefListStateById(ObjectId=objectid)

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
		response, error = swtch.getAllLaPortChannelIntfRefListStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


