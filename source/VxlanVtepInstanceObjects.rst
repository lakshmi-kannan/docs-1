VxlanVtepInstance Object
=============================================================

*config/VxlanVtepInstance*
------------------------------------

- Multiple objects of this type can exist in a system.

+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
|  **PARAMETER NAME**   | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| Vni **[KEY]**         | uint32        | VXLAN Network ID               | N/A         | N/A                            |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| Intf **[KEY]**        | string        | VTEP instance identifier       | N/A         | N/A                            |
|                       |               | name. should be defined as     |             |                                |
|                       |               | either vtep<id#> or <id#> if   |             |                                |
|                       |               | the later then 'vtep' will be  |             |                                |
|                       |               | prepended to the <id#> example |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| DstIp                 | string        | Destination IP address for the | N/A         | N/A                            |
|                       |               | static VxLAN tunnel            |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| InnerVlanHandlingMode | int32         | The inner vlan tag handling    |           0 | DISCARD_INNER_VLAN(0),         |
|                       |               | mode.                          |             | NO_DISCARD_INNER_VLAN(1)       |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| Mtu                   | uint32        | Set the MTU to be applied to   |        1450 | N/A                            |
|                       |               | all VTEP within this VxLAN     |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| TOS                   | uint16        | Type of Service                |           0 | N/A                            |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| VlanId                | uint16        | Vlan Id to encapsulate with    | N/A         | N/A                            |
|                       |               | the vtep tunnel ethernet       |             |                                |
|                       |               | header                         |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminState            | string        | Administrative state of VXLAN  | DOWN        | UP, DOWN                       |
|                       |               | MAC/IP layer                   |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| DstUDP                | uint16        | vxlan udp port.  Deafult is    |        4789 | N/A                            |
|                       |               | the iana default udp port      |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| IntfRef               | string        | Source interface where the     | N/A         | N/A                            |
|                       |               | source ip will be derived      |             |                                |
|                       |               | from.  If an interface is      |             |                                |
|                       |               | not supplied the src-ip        |             |                                |
|                       |               | will be used. This attribute   |             |                                |
|                       |               | takes presedence over src-ip   |             |                                |
|                       |               | attribute.                     |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| SrcIp                 | string        | Source IP address for the      | 0.0.0.0     | N/A                            |
|                       |               | VxLAN tunnel                   |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| TTL                   | uint16        | TTL of the Vxlan tunnel        |          64 | N/A                            |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/VxlanVtepInstance
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/VxlanVtepInstance/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/VxlanVtepInstances?CurrentMarker=<x>\\&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/VxlanVtepInstance
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/VxlanVtepInstance
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/VxlanVtepInstance<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/VxlanVtepInstance
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/VxlanVtepInstance<uuid>


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
		response, error = swtch.getVxlanVtepInstance(Vni=vni, Intf=intf)

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
		response, error = swtch.getVxlanVtepInstanceById(ObjectId=objectid)

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
		response, error = swtch.getAllVxlanVtepInstances()

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
		response, error = swtch.createVxlanVtepInstance(Vni=vni, Intf=intf, DstIp=dstip, InnerVlanHandlingMode=innervlanhandlingmode, Mtu=mtu, TOS=tos, VlanId=vlanid, AdminState=adminstate, DstUDP=dstudp, IntfRef=intfref, SrcIp=srcip, TTL=ttl)

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
		response, error = swtch.deleteVxlanVtepInstance(Vni=vni, Intf=intf)

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
		response, error = swtch.deleteVxlanVtepInstanceById(ObjectId=objectid

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
		response, error = swtch.updateVxlanVtepInstance(Vni=vni, Intf=intf, DstIp=dstip, InnerVlanHandlingMode=innervlanhandlingmode, Mtu=mtu, TOS=tos, VlanId=vlanid, AdminState=adminstate, DstUDP=dstudp, IntfRef=intfref, SrcIp=srcip, TTL=ttl)

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
		response, error = swtch.updateVxlanVtepInstanceById(ObjectId=objectidDstIp=dstip, InnerVlanHandlingMode=innervlanhandlingmode, Mtu=mtu, TOS=tos, VlanId=vlanid, AdminState=adminstate, DstUDP=dstudp, IntfRef=intfref, SrcIp=srcip, TTL=ttl)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
