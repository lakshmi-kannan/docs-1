LaPortChannel Object
=============================================================

*config/LaPortChannel*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         |    **DEFAULT**    |        **VALID VALUES**        |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| IntfRef **[KEY]**  | string        | Id of the lag group            | N/A               | N/A                            |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| LacpMode           | int32         | ACTIVE is to initiate the      |                 0 | ACTIVE(0), PASSIVE(1)          |
|                    |               | transmission of LACP packets.  |                   |                                |
|                    |               | PASSIVE is to wait for peer to |                   |                                |
|                    |               | initiate the transmission of   |                   |                                |
|                    |               | LACP packets.                  |                   |                                |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| MinLinks           | uint16        | Specifies the mininum number   |                 1 | N/A                            |
|                    |               | of member interfaces that must |                   |                                |
|                    |               | be active for the aggregate    |                   |                                |
|                    |               | interface to be available      |                   |                                |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| SystemIdMac        | string        | The MAC address portion of     | 00-00-00-00-00-00 | N/A                            |
|                    |               | the nodes System ID. This      |                   |                                |
|                    |               | is combined with the system    |                   |                                |
|                    |               | priority to construct the      |                   |                                |
|                    |               | 8-octet system-id              |                   |                                |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| SystemPriority     | uint16        | Sytem priority used by the     |             32768 | N/A                            |
|                    |               | node on this LAG interface.    |                   |                                |
|                    |               | Lower value is higher priority |                   |                                |
|                    |               | for determining which node is  |                   |                                |
|                    |               | the controlling system.        |                   |                                |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| AdminState         | string        | Convenient way to              | UP                | UP, DOWN                       |
|                    |               | disable/enable a lag group.    |                   |                                |
|                    |               | The behaviour should be such   |                   |                                |
|                    |               | that all traffic should stop.  |                   |                                |
|                    |               | LACP frames should continue to |                   |                                |
|                    |               | be processed                   |                   |                                |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| IntfRefList        | string        | List of current member         | N/A               | N/A                            |
|                    |               | interfaces for the aggregate   |                   |                                |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| LagHash            | int32         | The tx hashing algorithm used  |                 0 | LAYER2(0), LAYER3_4(2),        |
|                    |               | by the lag group               |                   | LAYER2_3(1)                    |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| LagType            | int32         | Sets the type of LAG           |                 0 | LACP(0), STATIC(1)             |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+
| Interval           | int32         | Set the period between         |                 1 | SLOW(1), FAST(0)               |
|                    |               | LACP messages -- uses the      |                   |                                |
|                    |               | lacp-period-type enumeration.  |                   |                                |
+--------------------+---------------+--------------------------------+-------------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/LaPortChannel
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/LaPortChannel/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/LaPortChannels?CurrentMarker=<x>\\&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/LaPortChannel
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/LaPortChannel
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/LaPortChannel<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/LaPortChannel
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/LaPortChannel<uuid>


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
		response, error = swtch.getLaPortChannel(IntfRef=intfref)

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
		response, error = swtch.getLaPortChannelById(ObjectId=objectid)

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
		response, error = swtch.getAllLaPortChannels()

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
		response, error = swtch.createLaPortChannel(IntfRef=intfref, LacpMode=lacpmode, MinLinks=minlinks, SystemIdMac=systemidmac, SystemPriority=systempriority, AdminState=adminstate, IntfRefList=intfreflist, LagHash=laghash, LagType=lagtype, Interval=interval)

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
		response, error = swtch.deleteLaPortChannel(IntfRef=intfref)

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
		response, error = swtch.deleteLaPortChannelById(ObjectId=objectid

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
		response, error = swtch.updateLaPortChannel(IntfRef=intfref, LacpMode=lacpmode, MinLinks=minlinks, SystemIdMac=systemidmac, SystemPriority=systempriority, AdminState=adminstate, IntfRefList=intfreflist, LagHash=laghash, LagType=lagtype, Interval=interval)

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
		response, error = swtch.updateLaPortChannelById(ObjectId=objectidLacpMode=lacpmode, MinLinks=minlinks, SystemIdMac=systemidmac, SystemPriority=systempriority, AdminState=adminstate, IntfRefList=intfreflist, LagHash=laghash, LagType=lagtype, Interval=interval)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
