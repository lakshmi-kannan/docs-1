StpPort Object
=============================================================

*config/StpPort*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| IntfRef **[KEY]**  | string        | The port number of the port    | N/A         | N/A                            |
|                    |               | for which this entry contains  |             |                                |
|                    |               | Spanning Tree Protocol         |             |                                |
|                    |               | management information.        |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| Vlan **[KEY]**     | int32         | The value of instance of the   | N/A         | N/A                            |
|                    |               | vlan object                    |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminEdgePort      | int32         | The administrative value of    |           2 | false(2), true(1)              |
|                    |               | the Edge Port parameter.  A    |             |                                |
|                    |               | value of true(1) indicates     |             |                                |
|                    |               | that this port should be       |             |                                |
|                    |               | assumed as an edge-port and    |             |                                |
|                    |               | a value of false(2) indicates  |             |                                |
|                    |               | that this port should be       |             |                                |
|                    |               | assumed as a non-edge-port.    |             |                                |
|                    |               |  Setting this object will      |             |                                |
|                    |               | also cause the corresponding   |             |                                |
|                    |               | instance of OperEdgePort to    |             |                                |
|                    |               | change to the same value.      |             |                                |
|                    |               |  Note that even when this      |             |                                |
|                    |               | object's value is true the     |             |                                |
|                    |               | value of the corresponding     |             |                                |
|                    |               | instance of OperEdgePort can   |             |                                |
|                    |               | be false if a BPDU has been    |             |                                |
|                    |               | received.  The value of this   |             |                                |
|                    |               | object MUST be retained across |             |                                |
|                    |               | reinitializations of the       |             |                                |
|                    |               | management system.             |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminState         | string        | The enabled/disabled status of | UP          | UP, DOWN                       |
|                    |               | the port.                      |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| BpduGuard          | int32         | A Port as OperEdge which       |           2 | false(2), true(1)              |
|                    |               | receives BPDU with BpduGuard   |             |                                |
|                    |               | enabled will shut the port     |             |                                |
|                    |               | down.                          |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| BpduGuardInterval  | int32         | The interval time to which     |          15 | N/A                            |
|                    |               | a port will try to recover     |             |                                |
|                    |               | from BPDU Guard err-disable    |             |                                |
|                    |               | state.  If no BPDU frames are  |             |                                |
|                    |               | detected after this timeout    |             |                                |
|                    |               | plus 3 Times Hello Time then   |             |                                |
|                    |               | the port will transition back  |             |                                |
|                    |               | to Up state.  If condition     |             |                                |
|                    |               | is cleared manually then this  |             |                                |
|                    |               | operation is ignored.  If set  |             |                                |
|                    |               | to zero then timer is inactive |             |                                |
|                    |               | and recovery is based on       |             |                                |
|                    |               | manual intervention.           |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| PathCost           | int32         | The contribution of this       |           1 | N/A                            |
|                    |               | port to the path cost of       |             |                                |
|                    |               | paths towards the spanning     |             |                                |
|                    |               | tree root which include        |             |                                |
|                    |               | this port.  802.1D-1998        |             |                                |
|                    |               | recommends that the default    |             |                                |
|                    |               | value of this parameter be     |             |                                |
|                    |               | in inverse proportion to the   |             |                                |
|                    |               | speed of the attached LAN.     |             |                                |
|                    |               |  New implementations should    |             |                                |
|                    |               | support PathCost32. If the     |             |                                |
|                    |               | port path costs exceeds the    |             |                                |
|                    |               | maximum value of this object   |             |                                |
|                    |               | then this object should report |             |                                |
|                    |               | the maximum value; namely      |             |                                |
|                    |               | 65535.  Applications should    |             |                                |
|                    |               | try to read the PathCost32     |             |                                |
|                    |               | object if this object          |             |                                |
|                    |               | reports the maximum value.     |             |                                |
|                    |               |  Value of 1 will force node    |             |                                |
|                    |               | to auto discover the value     |             |                                |
|                    |               |        based on the ports      |             |                                |
|                    |               | capabilities.                  |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| ProtocolMigration  | int32         | When operating in RSTP         |           1 | false(2), true(1)              |
|                    |               | (version 2) mode writing       |             |                                |
|                    |               | true(1) to this object forces  |             |                                |
|                    |               | this port to transmit RSTP     |             |                                |
|                    |               | BPDUs. Any other operation on  |             |                                |
|                    |               | this object has no effect and  |             |                                |
|                    |               | it always returns false(2)     |             |                                |
|                    |               | when read.                     |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminPathCost      | int32         | The administratively assigned  |      200000 | N/A                            |
|                    |               | value for the contribution     |             |                                |
|                    |               | of this port to the path cost  |             |                                |
|                    |               | of paths toward the spanning   |             |                                |
|                    |               | tree root.  Writing a value of |             |                                |
|                    |               | '0' assigns the automatically  |             |                                |
|                    |               | calculated default Path Cost   |             |                                |
|                    |               | value to the port.  If the     |             |                                |
|                    |               | default Path Cost is being     |             |                                |
|                    |               | used this object returns '0'   |             |                                |
|                    |               | when read.  This complements   |             |                                |
|                    |               | the object PathCost or         |             |                                |
|                    |               | PathCost32 which returns the   |             |                                |
|                    |               | operational value of the path  |             |                                |
|                    |               | cost.    The value of this     |             |                                |
|                    |               | object MUST be retained across |             |                                |
|                    |               | reinitializations of the       |             |                                |
|                    |               | management system.             |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminPointToPoint  | int32         | The administrative             |           2 | forceTrue(0), forceFalse(1),   |
|                    |               | point-to-point status of       |             | auto(2)                        |
|                    |               | the LAN segment attached       |             |                                |
|                    |               | to this port using the         |             |                                |
|                    |               | enumeration values of the IEEE |             |                                |
|                    |               | 802.1w clause.  A value of     |             |                                |
|                    |               | forceTrue(0) indicates that    |             |                                |
|                    |               | this port should always be     |             |                                |
|                    |               | treated as if it is connected  |             |                                |
|                    |               | to a point-to-point link.      |             |                                |
|                    |               |  A value of forceFalse(1)      |             |                                |
|                    |               | indicates that this port       |             |                                |
|                    |               | should be treated as having    |             |                                |
|                    |               | a shared media connection.     |             |                                |
|                    |               | A value of auto(2) indicates   |             |                                |
|                    |               | that this port is considered   |             |                                |
|                    |               | to have a point-to-point link  |             |                                |
|                    |               | if it is an Aggregator and     |             |                                |
|                    |               | all of its    members are      |             |                                |
|                    |               | aggregatable or if the MAC     |             |                                |
|                    |               | entity is configured for full  |             |                                |
|                    |               | duplex operation               |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| BridgeAssurance    | int32         | When enabled BPDUs will be     |           2 | false(2), true(1)              |
|                    |               | transmitted out of all stp     |             |                                |
|                    |               | ports regardless of state.     |             |                                |
|                    |               |  When an stp port fails to     |             |                                |
|                    |               | receive a BPDU the port should |             |                                |
|                    |               |  transition to a Blocked       |             |                                |
|                    |               | state.  Upon reception of      |             |                                |
|                    |               | BDPU after shutdown  should    |             |                                |
|                    |               | transition port into the       |             |                                |
|                    |               | bridge.                        |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| PathCost32         | int32         | The contribution of this       |           1 | N/A                            |
|                    |               | port to the path cost of       |             |                                |
|                    |               | paths towards the spanning     |             |                                |
|                    |               | tree root which include this   |             |                                |
|                    |               | port.  802.1D-1998 recommends  |             |                                |
|                    |               | that the default value of      |             |                                |
|                    |               | this parameter be in inverse   |             |                                |
|                    |               | proportion to the speed of     |             |                                |
|                    |               | the attached LAN.  This object |             |                                |
|                    |               | replaces PathCost to support   |             |                                |
|                    |               | IEEE 802.1t. Value of 1 will   |             |                                |
|                    |               | force node to auto discover    |             |                                |
|                    |               | the value        based on the  |             |                                |
|                    |               | ports capabilities.            |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| Priority           | int32         | The value of the priority      |         128 | N/A                            |
|                    |               | field that is contained in the |             |                                |
|                    |               | first in network byte order    |             |                                |
|                    |               | octet of the 2 octet long      |             |                                |
|                    |               | Port ID.  The other octet of   |             |                                |
|                    |               | the Port ID is given by the    |             |                                |
|                    |               | value of StpPort. On bridges   |             |                                |
|                    |               | supporting IEEE 802.1t or IEEE |             |                                |
|                    |               | 802.1w                         |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/StpPort
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/StpPort/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/StpPorts?CurrentMarker=<x>\\&Count=<y>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/StpPort
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/StpPort<uuid>


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
		response, error = swtch.getStpPort(IntfRef=intfref, Vlan=vlan)

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
		response, error = swtch.getStpPortById(ObjectId=objectid)

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
		response, error = swtch.getAllStpPorts()

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
		response, error = swtch.updateStpPort(IntfRef=intfref, Vlan=vlan, AdminEdgePort=adminedgeport, AdminState=adminstate, BpduGuard=bpduguard, BpduGuardInterval=bpduguardinterval, PathCost=pathcost, ProtocolMigration=protocolmigration, AdminPathCost=adminpathcost, AdminPointToPoint=adminpointtopoint, BridgeAssurance=bridgeassurance, PathCost32=pathcost32, Priority=priority)

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
		response, error = swtch.updateStpPortById(ObjectId=objectidAdminEdgePort=adminedgeport, AdminState=adminstate, BpduGuard=bpduguard, BpduGuardInterval=bpduguardinterval, PathCost=pathcost, ProtocolMigration=protocolmigration, AdminPathCost=adminpathcost, AdminPointToPoint=adminpointtopoint, BridgeAssurance=bridgeassurance, PathCost32=pathcost32, Priority=priority)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
