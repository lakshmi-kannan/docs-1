DistributedRelay Object
=============================================================

*config/DistributedRelay*
------------------------------------

- Multiple objects of this type can exist in a system.

+---------------------------+---------------+--------------------------------+-------------------+------------------+
|    **PARAMETER NAME**     | **DATA TYPE** |        **DESCRIPTION**         |    **DEFAULT**    | **VALID VALUES** |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| DrniName **[KEY]**        | string        | The unique identifier          | N/A               | N/A              |
|                           |               | allocated to this Distributed  |                   |                  |
|                           |               | Relay by the local System.     |                   |                  |
|                           |               | This attribute identifies a    |                   |                  |
|                           |               | Distributed Relay instance     |                   |                  |
|                           |               | among the subordinate managed  |                   |                  |
|                           |               | objects of the containing      |                   |                  |
|                           |               | object.                        |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| EncapMethod               | string        | This managed object is         | 00-80-C2-01       | N/A              |
|                           |               | applicable only when Network / |                   |                  |
|                           |               | IPL sharing by time (9.3.2.1)  |                   |                  |
|                           |               | or Network / IPL sharing by    |                   |                  |
|                           |               | tag (9.3.2.2) or Network /     |                   |                  |
|                           |               | IPL sharing by encapsulation   |                   |                  |
|                           |               | (9.3.2.3) is supported.        |                   |                  |
|                           |               | The object identifies the      |                   |                  |
|                           |               | value representing the         |                   |                  |
|                           |               | encapsulation method that is   |                   |                  |
|                           |               | used to transport IPL frames   |                   |                  |
|                           |               | to the Neighbor Portal System  |                   |                  |
|                           |               | when the IPL and network       |                   |                  |
|                           |               | link are sharing the same      |                   |                  |
|                           |               | physical link. It consists     |                   |                  |
|                           |               | of the 3-octet OUI or CID      |                   |                  |
|                           |               | identifying the organization   |                   |                  |
|                           |               | that is responsible for        |                   |                  |
|                           |               | this encapsulation and one     |                   |                  |
|                           |               | following octet used to        |                   |                  |
|                           |               | identify the encapsulation     |                   |                  |
|                           |               | method defined by that         |                   |                  |
|                           |               | organization. Table 9-11       |                   |                  |
|                           |               | provides the IEEE 802.1 OUI    |                   |                  |
|                           |               | (00-80-C2) encapsulation       |                   |                  |
|                           |               | method encodings. A Default    |                   |                  |
|                           |               | value of 0x00-80-C2-00         |                   |                  |
|                           |               | indicates that the IPL is      |                   |                  |
|                           |               | using a separate physical or   |                   |                  |
|                           |               | Aggregation link. A value of   |                   |                  |
|                           |               | 1 indicates that Network / IPL |                   |                  |
|                           |               | sharing by time (9.3.2.1) is   |                   |                  |
|                           |               | used. A value of 2 indicates   |                   |                  |
|                           |               | that the encapsulation method  |                   |                  |
|                           |               | used is the same as the one    |                   |                  |
|                           |               | used by network frames and     |                   |                  |
|                           |               | that Network / IPL sharing by  |                   |                  |
|                           |               | tag (9.3.2.2) is used          |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| GatewayAlgorithm          | string        | This object identifies the     | 00-80-C2-01       | N/A              |
|                           |               | algorithm used by the DR       |                   |                  |
|                           |               | Function to assign frames to a |                   |                  |
|                           |               | Gateway Conversation ID. Table |                   |                  |
|                           |               | 9-7 provides the IEEE 802.1    |                   |                  |
|                           |               | OUI (00                        |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| IntfRef                   | string        | Read-write Interface           | N/A               | N/A              |
|                           |               | Identifier of the Aggregator   |                   |                  |
|                           |               | Port assigned to this          |                   |                  |
|                           |               | Distributed Relay              |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| NeighborGatewayAlgorithm  | string        | TThis object identifies        | 00-80-C2-01       | N/A              |
|                           |               | the value for the Gateway      |                   |                  |
|                           |               | algorithm of the Neighbor      |                   |                  |
|                           |               | Portal System                  |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| NeighborPortAlgorithm     | string        | This object identifies the     | 00-80-C2-01       | N/A              |
|                           |               | value for the Port Algorithm   |                   |                  |
|                           |               | of the Neighbor Portal System  |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| PortalPriority            | uint16        | A 2octet read-write value      |             32768 | N/A              |
|                           |               | indicating the priority value  |                   |                  |
|                           |               | associated with the Portals    |                   |                  |
|                           |               | System ID. Also used as the    |                   |                  |
|                           |               | Actors System Priority (6.3.2) |                   |                  |
|                           |               | for the emulated system.       |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| IntfReflist               | string        | Read-write list of the         | N/A               | N/A              |
|                           |               | Interface Identifiers of the   |                   |                  |
|                           |               | Ports to the Intra-Portal      |                   |                  |
|                           |               | Links assigned to this         |                   |                  |
|                           |               | Distributed Relay. Each        |                   |                  |
|                           |               | Interface Identifier           |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| IntraPortalPortProtocolDA | string        | A 6-octet read-write MAC       | 01-80-C2-00-00-03 | N/A              |
|                           |               | Address value specifying the   |                   |                  |
|                           |               | DA to be used when sending     |                   |                  |
|                           |               | DRCPDUs                        |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| NeighborAdminDRCPState    | string        | A string of 8 bits             |          00000000 | N/A              |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| PortalAddress             | string        | A read-write identifier        | N/A               | N/A              |
|                           |               | of a particular Portal.        |                   |                  |
|                           |               | Portal-Addr has to be unique   |                   |                  |
|                           |               | among at least all of the      |                   |                  |
|                           |               | potential Portal Systems to    |                   |                  |
|                           |               | which a given Portal System    |                   |                  |
|                           |               | might be attached via an       |                   |                  |
|                           |               | IPL Intra-Portal Link. Also    |                   |                  |
|                           |               | used as the Actors System      |                   |                  |
|                           |               | ID (6.3.2) for the emulated    |                   |                  |
|                           |               | system                         |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| PortalSystemNumber        | uint8         | A read-write identifier of     | N/A               | N/A              |
|                           |               | this particular Portal System  |                   |                  |
|                           |               | within a Portal. It is the     |                   |                  |
|                           |               | responsibility of the network  |                   |                  |
|                           |               | administrator to ensure that   |                   |                  |
|                           |               | these numbers are unique       |                   |                  |
|                           |               | among the Portal Systems       |                   |                  |
|                           |               | with the same aDrniPortalAddr  |                   |                  |
|                           |               | (7.4.1.1.4)                    |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+
| ThreePortalSystem         | bool          | A read-write Boolean value     | false             | N/A              |
|                           |               | indicating whether this Portal |                   |                  |
|                           |               | System is part of a Portal     |                   |                  |
|                           |               | consisting of three Portal     |                   |                  |
|                           |               | Systems or not. Value 1 stands |                   |                  |
|                           |               | for a Portal of three Portal   |                   |                  |
|                           |               | Systems                        |                   |                  |
+---------------------------+---------------+--------------------------------+-------------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/DistributedRelay
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/DistributedRelay/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/DistributedRelays?CurrentMarker=<x>\\&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/DistributedRelay
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/DistributedRelay
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/DistributedRelay<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/DistributedRelay
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/DistributedRelay<uuid>


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
		response, error = swtch.getDistributedRelay(DrniName=drniname)

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
		response, error = swtch.getDistributedRelayById(ObjectId=objectid)

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
		response, error = swtch.getAllDistributedRelays()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **CREATE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.createDistributedRelay(DrniName=drniname, EncapMethod=encapmethod, GatewayAlgorithm=gatewayalgorithm, IntfRef=intfref, NeighborGatewayAlgorithm=neighborgatewayalgorithm, NeighborPortAlgorithm=neighborportalgorithm, PortalPriority=portalpriority, IntfReflist=intfreflist, IntraPortalPortProtocolDA=intraportalportprotocolda, NeighborAdminDRCPState=neighboradmindrcpstate, PortalAddress=portaladdress, PortalSystemNumber=portalsystemnumber, ThreePortalSystem=threeportalsystem)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **DELETE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.deleteDistributedRelay(DrniName=drniname)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **DELETE By ID**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.deleteDistributedRelayById(ObjectId=objectid

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **UPDATE**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.updateDistributedRelay(DrniName=drniname, EncapMethod=encapmethod, GatewayAlgorithm=gatewayalgorithm, IntfRef=intfref, NeighborGatewayAlgorithm=neighborgatewayalgorithm, NeighborPortAlgorithm=neighborportalgorithm, PortalPriority=portalpriority, IntfReflist=intfreflist, IntraPortalPortProtocolDA=intraportalportprotocolda, NeighborAdminDRCPState=neighboradmindrcpstate, PortalAddress=portaladdress, PortalSystemNumber=portalsystemnumber, ThreePortalSystem=threeportalsystem)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


- **UPDATE By ID**

::

	import sys
	import os
	from flexswitchV2 import FlexSwitch

	if __name__ == '__main__':
		switchIP := "192.168.56.101"
		swtch = FlexSwitch (switchIP, 8080)  # Instantiate object to talk to flexSwitch
		response, error = swtch.updateDistributedRelayById(ObjectId=objectidEncapMethod=encapmethod, GatewayAlgorithm=gatewayalgorithm, IntfRef=intfref, NeighborGatewayAlgorithm=neighborgatewayalgorithm, NeighborPortAlgorithm=neighborportalgorithm, PortalPriority=portalpriority, IntfReflist=intfreflist, IntraPortalPortProtocolDA=intraportalportprotocolda, NeighborAdminDRCPState=neighboradmindrcpstate, PortalAddress=portaladdress, PortalSystemNumber=portalsystemnumber, ThreePortalSystem=threeportalsystem)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
