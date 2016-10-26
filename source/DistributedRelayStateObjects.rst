DistributedRelayState Object
=============================================================

*state/DistributedRelay*
------------------------------------

- Multiple objects of this type can exist in a system.

+------------------------------------+---------------+---------------------------------------+-------------+------------------+
|         **PARAMETER NAME**         | **DATA TYPE** |            **DESCRIPTION**            | **DEFAULT** | **VALID VALUES** |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| DrniName **[KEY]**                 | string        | The unique identifier                 | N/A         | N/A              |
|                                    |               | allocated to this Distributed         |             |                  |
|                                    |               | Relay by the local System.            |             |                  |
|                                    |               | This attribute identifies a           |             |                  |
|                                    |               | Distributed Relay instance            |             |                  |
|                                    |               | among the subordinate managed         |             |                  |
|                                    |               | objects of the containing             |             |                  |
|                                    |               | object.                               |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| ConvAdminGateway                   | uint32        | There are 4096                        | N/A         | N/A              |
|                                    |               | aDrniConvAdminGateway[]               |             |                  |
|                                    |               | variables                             |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| EncapMethod                        | string        | This managed object is                | N/A         | N/A              |
|                                    |               | applicable only when Network /        |             |                  |
|                                    |               | IPL sharing by time (9.3.2.1)         |             |                  |
|                                    |               | or Network / IPL sharing by           |             |                  |
|                                    |               | tag (9.3.2.2) or Network /            |             |                  |
|                                    |               | IPL sharing by encapsulation          |             |                  |
|                                    |               | (9.3.2.3) is supported.               |             |                  |
|                                    |               | The object identifies the             |             |                  |
|                                    |               | value representing the                |             |                  |
|                                    |               | encapsulation method that is          |             |                  |
|                                    |               | used to transport IPL frames          |             |                  |
|                                    |               | to the Neighbor Portal System         |             |                  |
|                                    |               | when the IPL and network              |             |                  |
|                                    |               | link are sharing the same             |             |                  |
|                                    |               | physical link. It consists            |             |                  |
|                                    |               | of the 3-octet OUI or CID             |             |                  |
|                                    |               | identifying the organization          |             |                  |
|                                    |               | that is responsible for               |             |                  |
|                                    |               | this encapsulation and one            |             |                  |
|                                    |               | following octet used to               |             |                  |
|                                    |               | identify the encapsulation            |             |                  |
|                                    |               | method defined by that                |             |                  |
|                                    |               | organization. Table 9-11              |             |                  |
|                                    |               | provides the IEEE 802.1 OUI           |             |                  |
|                                    |               | (00-80-C2) encapsulation              |             |                  |
|                                    |               | method encodings. A Default           |             |                  |
|                                    |               | value of 0x00-80-C2-00                |             |                  |
|                                    |               | indicates that the IPL is             |             |                  |
|                                    |               | using a separate physical or          |             |                  |
|                                    |               | Aggregation link. A value of          |             |                  |
|                                    |               | 1 indicates that Network / IPL        |             |                  |
|                                    |               | sharing by time (9.3.2.1) is          |             |                  |
|                                    |               | used. A value of 2 indicates          |             |                  |
|                                    |               | that the encapsulation method         |             |                  |
|                                    |               | used is the same as the one           |             |                  |
|                                    |               | used by network frames and            |             |                  |
|                                    |               | that Network / IPL sharing by         |             |                  |
|                                    |               | tag (9.3.2.2) is used                 |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| GatewayAlgorithm                   | string        | This object identifies the            | N/A         | N/A              |
|                                    |               | algorithm used by the DR              |             |                  |
|                                    |               | Function to assign frames to a        |             |                  |
|                                    |               | Gateway Conversation ID. Table        |             |                  |
|                                    |               | 9-7 provides the IEEE 802.1           |             |                  |
|                                    |               | OUI (00                               |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| IntfRef                            | string        | Read-write Interface                  | N/A         | N/A              |
|                                    |               | Identifier of the Aggregator          |             |                  |
|                                    |               | Port assigned to this                 |             |                  |
|                                    |               | Distributed Relay                     |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| NeighborAdminDRCPState             | string        | A string of 8 bits                    | N/A         | N/A              |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| PortConversationControl            | bool          | A read-write Boolean value that       | N/A         | N/A              |
|                                    |               | controls the operation of the         |             |                  |
|                                    |               | updateDRFHomeState (9.4.11).          |             |                  |
|                                    |               | When set to TRUE the Home             |             |                  |
|                                    |               | Gateway Vector is set equal to        |             |                  |
|                                    |               | Drni_Portal_System_Port_Conversation. |             |                  |
|                                    |               | Setting this object to TRUE is only   |             |                  |
|                                    |               | possible when the Gateway algorithm   |             |                  |
|                                    |               | and the Port algorithm use the same   |             |                  |
|                                    |               | distributions methods. The default is |             |                  |
|                                    |               | FALSE                                 |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| ThreePortalSystem                  | bool          | A read-write Boolean value indicating | N/A         | N/A              |
|                                    |               | whether this Portal System is part of |             |                  |
|                                    |               | a Portal consisting of three Portal   |             |                  |
|                                    |               | Systems or not. Value 1 stands for a  |             |                  |
|                                    |               | Portal of three Portal Systems        |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| IPLEncapMap                        | uint32        | This managed object is applicable     | N/A         | N/A              |
|                                    |               | only when Network / IPL sharing       |             |                  |
|                                    |               | by tag (9.3.2.2) or Network / IPL     |             |                  |
|                                    |               | sharing by encapsulation (9.3.2.3)    |             |                  |
|                                    |               | is supported. Each entry represents   |             |                  |
|                                    |               | the value of the identifier used      |             |                  |
|                                    |               | for an IPL frame associated with      |             |                  |
|                                    |               | that Gateway Conversation ID for the  |             |                  |
|                                    |               | encapsulation method specified in     |             |                  |
|                                    |               | 7.4.1.1.17. There are 1024 possible   |             |                  |
|                                    |               | Conversation Ids in a three portal    |             |                  |
|                                    |               | system                                |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| IntfRefList                        | string        | Read-write list of the Interface      | N/A         | N/A              |
|                                    |               | Identifiers of the Ports to the       |             |                  |
|                                    |               | Intra-Portal Links assigned to this   |             |                  |
|                                    |               | Distributed Relay. Each Interface     |             |                  |
|                                    |               | Identifier                            |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| NeighborAdminConvGatewayListDigest | uint8         | The value for the digest of the       | N/A         | N/A              |
|                                    |               | prioritized Gateway Conversation      |             |                  |
|                                    |               | ID-to-Gateway assignments of the      |             |                  |
|                                    |               | Neighbor Portal System                |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| PortalPriority                     | uint16        | A 2 octet read-write value indicating | N/A         | N/A              |
|                                    |               | the priority value associated with    |             |                  |
|                                    |               | the Portals System ID. Also used as   |             |                  |
|                                    |               | the Actors System Priority (6.3.2)    |             |                  |
|                                    |               | for the emulated system.              |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| PortalSystemNumber                 | uint8         | A read-write identifier of this       | N/A         | N/A              |
|                                    |               | particular Portal System within a     |             |                  |
|                                    |               | Portal. It is the responsibility of   |             |                  |
|                                    |               | the network administrator to ensure   |             |                  |
|                                    |               | that these numbers are unique among   |             |                  |
|                                    |               | the Portal Systems with the same      |             |                  |
|                                    |               | aDrniPortalAddr (7.4.1.1.4)           |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| Description                        | string        | A human-readable text string          | N/A         | N/A              |
|                                    |               | containing information about the      |             |                  |
|                                    |               | Distribute Relay. This string is      |             |                  |
|                                    |               | read-only. The contents are vendor    |             |                  |
|                                    |               | specific                              |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| NeighborAdminConvPortListDigest    | uint8         | The value for the digest of the       | N/A         | N/A              |
|                                    |               | prioritized Port Conversation         |             |                  |
|                                    |               | ID-to-Aggregation Port assignments of |             |                  |
|                                    |               | the Neighbor Portal System            |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| PortalAddress                      | string        | A read-write identifier of a          | N/A         | [0-9a-fA-F]{2}(  |
|                                    |               | particular Portal. Portal-Addr has to |             |                  |
|                                    |               | be unique among at least all of the   |             |                  |
|                                    |               | potential Portal Systems to which a   |             |                  |
|                                    |               | given Portal System might be attached |             |                  |
|                                    |               | via an IPL Intra-Portal Link. Also    |             |                  |
|                                    |               | used as the Actors System ID (6.3.2)  |             |                  |
|                                    |               | for the emulated system               |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| DRGatewayConversationPasses        | uint8         | A read-only current operational       | N/A         | N/A              |
|                                    |               | vector of Boolean values              |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| IntraPortalPortProtocolDA          | string        | A 6-octet read-write MAC Address      | N/A         | [0-9a-fA-F]{2}(  |
|                                    |               | value specifying the DA to be used    |             |                  |
|                                    |               | when sending DRCPDUs                  |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| NeighborGatewayAlgorithm           | string        | TThis object identifies the value for | N/A         | N/A              |
|                                    |               | the Gateway algorithm of the Neighbor |             |                  |
|                                    |               | Portal System                         |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| NeighborPortAlgorithm              | string        | This object identifies the value for  | N/A         | N/A              |
|                                    |               | the Port Algorithm of the Neighbor    |             |                  |
|                                    |               | Portal System                         |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| NetEncapMap                        | uint32        | This managed object is applicable     | N/A         | N/A              |
|                                    |               | only when Network / IPL sharing by    |             |                  |
|                                    |               | tag (9.3.2.2) is supported. Each      |             |                  |
|                                    |               | entry represents the translated       |             |                  |
|                                    |               | value of the identifier used for a    |             |                  |
|                                    |               | network frame associated with that    |             |                  |
|                                    |               | Gateway Conversation ID when the      |             |                  |
|                                    |               | method specified in 7.4.1.1.17 is the |             |                  |
|                                    |               | Network / IPL sharing by tag method   |             |                  |
|                                    |               | specified in 9.3.2.2 and the network  |             |                  |
|                                    |               | frames need to share the tag space    |             |                  |
|                                    |               | used by IPL frames                    |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+
| PSI                                | bool          | A read-only Boolean value providing   | N/A         | N/A              |
|                                    |               | the value of PSI                      |             |                  |
+------------------------------------+---------------+---------------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/DistributedRelay
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/DistributedRelays?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/DistributedRelayState/<uuid>


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
		response, error = swtch.getDistributedRelayState(DrniName=drniname)

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
		response, error = swtch.getDistributedRelayStateById(ObjectId=objectid)

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
		response, error = swtch.getAllDistributedRelayStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


