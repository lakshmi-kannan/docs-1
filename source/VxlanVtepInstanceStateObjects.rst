VxlanVtepInstanceState Object
=============================================================

*state/VxlanVtepInstance*
------------------------------------

- Multiple objects of this type can exist in a system.

+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
|  **PARAMETER NAME**   | **DATA TYPE** |                   **DESCRIPTION**                   | **DEFAULT** |        **VALID VALUES**        |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| Intf **[KEY]**        | string        | VTEP instance identifier                            | N/A         | N/A                            |
|                       |               | name. should be defined as                          |             |                                |
|                       |               | either vtep<id#> or <id#> if                        |             |                                |
|                       |               | the later then 'vtep' will be                       |             |                                |
|                       |               | prepended to the <id#> example                      |             |                                |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| Vni **[KEY]**         | uint32        | VXLAN Network ID                                    | N/A         | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| IfIndex               | int32         | Vtep IfIndex                                        | N/A         | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| VlanId                | uint16        | Vlan Id to encapsulate with                         | N/A         | N/A                            |
|                       |               | the vtep tunnel ethernet                            |             |                                |
|                       |               | header                                              |             |                                |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| VtepFsmPrevState      | string        | Previous state of the VTEP FSM                      | N/A         | N/A                            |
|                       |               | UNINITIALIZED/DISABLED/INIT/DETACHED/INTERFACE/NEXT |             |                                |
|                       |               | HOP INFO/RESOLVE NEXT HOP INFO/HW CONFIG/LISTENER   |             |                                |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| VtepFsmState          | string        | Current state of the VTEP FSM                       | N/A         | N/A                            |
|                       |               | UNINITIALIZED/DISABLED/INIT/DETACHED/INTERFACE/NEXT |             |                                |
|                       |               | HOP INFO/RESOLVE NEXT HOP INFO/HW CONFIG/LISTENER   |             |                                |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| DstUDP                | uint16        | vxlan udp port.  Deafult is the iana default udp    |        4789 | N/A                            |
|                       |               | port                                                |             |                                |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| RxFwdPkts             | uint64        | Rx Forwaded Packets                                 | N/A         | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| TTL                   | uint16        | TTL of the Vxlan tunnel                             |          64 | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| DstIp                 | string        | Destination IP address for the static VxLAN tunnel  | N/A         | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| RxDropPkts            | uint64        | Rx Dropped Packets                                  | N/A         | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| TOS                   | uint16        | Type of Service                                     |           0 | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| TxPkts                | uint64        | Tx Packets                                          | N/A         | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| InnerVlanHandlingMode | int32         | The inner vlan tag handling mode.                   |           0 | DISCARD_INNER_VLAN(0),         |
|                       |               |                                                     |             | NO_DISCARD_INNER_VLAN(1)       |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| IntfRef               | string        | Source interface where the source ip will be        | N/A         | N/A                            |
|                       |               | derived from.  If an interface is not supplied      |             |                                |
|                       |               | the src-ip will be used. This attribute takes       |             |                                |
|                       |               | presedence over src-ip attribute.                   |             |                                |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| Mtu                   | uint32        | Set the MTU to be applied to all VTEP within this   |        1550 | N/A                            |
|                       |               | VxLAN                                               |             |                                |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| OperState             | string        | Operational state of VXLAN MAC/IP layer             | DOWN        | UP, DOWN                       |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| RxPkts                | uint64        | Rx Packets                                          | N/A         | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| RxUnknownVni          | uint64        | Rx Unknown Vni in frame                             | N/A         | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+
| SrcIp                 | string        | Source IP address for the VxLAN tunnel              | 0.0.0.0     | N/A                            |
+-----------------------+---------------+-----------------------------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/VxlanVtepInstance
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/VxlanVtepInstances?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/VxlanVtepInstanceState/<uuid>


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
		response, error = swtch.getVxlanVtepInstanceState(Intf=intf, Vni=vni)

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
		response, error = swtch.getVxlanVtepInstanceStateById(ObjectId=objectid)

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
		response, error = swtch.getAllVxlanVtepInstanceStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


