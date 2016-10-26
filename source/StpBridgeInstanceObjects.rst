StpBridgeInstance Object
=============================================================

*config/StpBridgeInstance*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------------+-------------------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         |    **DEFAULT**    |       **VALID VALUES**        |
+--------------------+---------------+--------------------------------+-------------------+-------------------------------+
| Vlan **[KEY]**     | uint16        | Each bridge is associated      | N/A               | N/A                           |
|                    |               | with a domain.  Typically this |                   |                               |
|                    |               | domain is represented as the   |                   |                               |
|                    |               | vlan; The default domain is    |                   |                               |
|                    |               |                           4095 |                   |                               |
+--------------------+---------------+--------------------------------+-------------------+-------------------------------+
| ForceVersion       | int32         | Stp Version                    |                 2 | stp(1), rstp-pvst(2), mstp(3) |
+--------------------+---------------+--------------------------------+-------------------+-------------------------------+
| ForwardDelay       | int32         | The value that all bridges     |                15 | N/A                           |
|                    |               | use for ForwardDelay when      |                   |                               |
|                    |               | this bridge is acting as the   |                   |                               |
|                    |               | root.  Note that 802.1D-1998   |                   |                               |
|                    |               | specifies that the range for   |                   |                               |
|                    |               | this parameter is related      |                   |                               |
|                    |               | to the value of MaxAge.  The   |                   |                               |
|                    |               | granularity of this timer is   |                   |                               |
|                    |               | specified by 802.1D-1998 to be |                   |                               |
|                    |               | 1 second.  An agent may return |                   |                               |
|                    |               | a badValue error if a set is   |                   |                               |
|                    |               | attempted to a value that is   |                   |                               |
|                    |               | not a whole number of seconds. |                   |                               |
+--------------------+---------------+--------------------------------+-------------------+-------------------------------+
| HelloTime          | int32         | The value that all bridges     |                 2 | N/A                           |
|                    |               | use for HelloTime when this    |                   |                               |
|                    |               | bridge is acting as the root.  |                   |                               |
|                    |               |  The granularity of this timer |                   |                               |
|                    |               | is specified by 802.1D-1998    |                   |                               |
|                    |               | to be 1 second.  An agent may  |                   |                               |
|                    |               | return a badValue error if a   |                   |                               |
|                    |               | set is attempted    to a value |                   |                               |
|                    |               | that is not a whole number of  |                   |                               |
|                    |               | seconds.                       |                   |                               |
+--------------------+---------------+--------------------------------+-------------------+-------------------------------+
| MaxAge             | int32         | The value that all bridges use |                20 | N/A                           |
|                    |               | for MaxAge when this bridge is |                   |                               |
|                    |               | acting as the root.  Note that |                   |                               |
|                    |               | 802.1D-1998 specifies that     |                   |                               |
|                    |               | the range for this parameter   |                   |                               |
|                    |               | is related to the value of     |                   |                               |
|                    |               | HelloTime.  The granularity    |                   |                               |
|                    |               | of this timer is specified by  |                   |                               |
|                    |               | 802.1D-1998 to be 1 second.    |                   |                               |
|                    |               | An agent may return a badValue |                   |                               |
|                    |               | error if a set is attempted    |                   |                               |
|                    |               | to a value that is not a whole |                   |                               |
|                    |               | number of seconds.             |                   |                               |
+--------------------+---------------+--------------------------------+-------------------+-------------------------------+
| Priority           | int32         | The value of the write-able    |             32768 | N/A                           |
|                    |               | portion of the Bridge ID i.e.  |                   |                               |
|                    |               | the first two octets of the    |                   |                               |
|                    |               | 8 octet long Bridge ID.  The   |                   |                               |
|                    |               | other last 6 octets of the     |                   |                               |
|                    |               | Bridge ID are given by the     |                   |                               |
|                    |               | value of Address. On bridges   |                   |                               |
|                    |               | supporting IEEE 802.1t or IEEE |                   |                               |
|                    |               | 802.1w permissible values are  |                   |                               |
|                    |               | 0-61440 in steps of 4096.      |                   |                               |
|                    |               | Extended Priority is enabled   |                   |                               |
|                    |               | when the lower 12 bits are set |                   |                               |
|                    |               | using the Bridges VLAN id      |                   |                               |
+--------------------+---------------+--------------------------------+-------------------+-------------------------------+
| TxHoldCount        | int32         | Configures the number of       |                 6 | N/A                           |
|                    |               | BPDUs that can be sent before  |                   |                               |
|                    |               | pausing for 1 second.          |                   |                               |
+--------------------+---------------+--------------------------------+-------------------+-------------------------------+
| Address            | string        | The bridge identifier of the   | 00-00-00-00-00-00 | N/A                           |
|                    |               | root of the spanning tree as   |                   |                               |
|                    |               | determined by the Spanning     |                   |                               |
|                    |               | Tree Protocol as executed      |                   |                               |
|                    |               | by this node.  This value is   |                   |                               |
|                    |               | used as the Root Identifier    |                   |                               |
|                    |               | parameter in all Configuration |                   |                               |
|                    |               | Bridge PDUs originated by this |                   |                               |
|                    |               | node.                          |                   |                               |
+--------------------+---------------+--------------------------------+-------------------+-------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/StpBridgeInstance
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/StpBridgeInstance/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/StpBridgeInstances?CurrentMarker=<x>&Count=<y>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/StpBridgeInstance
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/StpBridgeInstance<uuid>


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
		response, error = swtch.getStpBridgeInstance(Vlan=vlan)

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
		response, error = swtch.getStpBridgeInstanceById(ObjectId=objectid)

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
		response, error = swtch.getAllStpBridgeInstances()

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
		response, error = swtch.updateStpBridgeInstance(Vlan=vlan, ForceVersion=forceversion, ForwardDelay=forwarddelay, HelloTime=hellotime, MaxAge=maxage, Priority=priority, TxHoldCount=txholdcount, Address=address)

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
		response, error = swtch.updateStpBridgeInstanceById(ObjectId=objectidForceVersion=forceversion, ForwardDelay=forwarddelay, HelloTime=hellotime, MaxAge=maxage, Priority=priority, TxHoldCount=txholdcount, Address=address)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
