OspfIfEntry Object
=============================================================

*config/OspfIfEntry*
------------------------------------

- Multiple objects of this type can exist in a system.

+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
|   **PARAMETER NAME**    | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfIpAddress **[KEY]**   | string        | The IP address of this OSPF    | N/A         | N/A                            |
|                         |               | interface.                     |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| AddressLessIf **[KEY]** | int32         | For the purpose of easing the  | N/A         | N/A                            |
|                         |               | instancing of addressed and    |             |                                |
|                         |               | addressless interfaces; this   |             |                                |
|                         |               | variable takes the value 0 on  |             |                                |
|                         |               | interfaces with IP addresses   |             |                                |
|                         |               | and the corresponding value of |             |                                |
|                         |               | ifIndex for interfaces having  |             |                                |
|                         |               | no IP address.                 |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfPollInterval          | int32         | The larger time interval       | N/A         | N/A                            |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfRetransInterval       | int32         | The number of seconds between  | N/A         | N/A                            |
|                         |               | link state advertisement       |             |                                |
|                         |               | retransmissions                |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfRtrPriority           | int32         | The priority of this           | N/A         | N/A                            |
|                         |               | interface.  Used in            |             |                                |
|                         |               | multi-access networks          |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfTransitDelay          | int32         | The estimated number of        | N/A         | N/A                            |
|                         |               | seconds it takes to transmit a |             |                                |
|                         |               | link state update packet over  |             |                                |
|                         |               | this interface.  Note that     |             |                                |
|                         |               | the minimal value SHOULD be 1  |             |                                |
|                         |               | second.                        |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfType                  | string        | The OSPF interface type. By    | N/A         | broadcast, nbma, pointToPoint, |
|                         |               | way of a default               |             | pointToMultipoint              |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfAdminStat             | int32         | Indiacates if OSPF is enabled  | N/A         | N/A                            |
|                         |               | on this interface              |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfAreaId                | string        | A 32-bit integer uniquely      | N/A         | N/A                            |
|                         |               | identifying the area to which  |             |                                |
|                         |               | the interface connects.  Area  |             |                                |
|                         |               | ID 0.0.0.0 is used for the     |             |                                |
|                         |               | OSPF backbone.                 |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfHelloInterval         | int32         | The length of time             |          10 | N/A                            |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfRtrDeadInterval       | int32         | The number of seconds that     |          40 | N/A                            |
|                         |               | a router's Hello packets       |             |                                |
|                         |               | have not been seen before      |             |                                |
|                         |               | its neighbors declare the      |             |                                |
|                         |               | router down. This should be    |             |                                |
|                         |               | some multiple of the Hello     |             |                                |
|                         |               | interval.  This value must     |             |                                |
|                         |               | be the same for all routers    |             |                                |
|                         |               | attached to a common network.  |             |                                |
+-------------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/OspfIfEntry
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfIfEntry/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfIfEntrys?CurrentMarker=<x>&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/OspfIfEntry
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/OspfIfEntry
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/OspfIfEntry<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/OspfIfEntry
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/OspfIfEntry<uuid>


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
		response, error = swtch.getOspfIfEntry(IfIpAddress=ifipaddress, AddressLessIf=addresslessif)

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
		response, error = swtch.getOspfIfEntryById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfIfEntrys()

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
		response, error = swtch.createOspfIfEntry(IfIpAddress=ifipaddress, AddressLessIf=addresslessif, IfPollInterval=ifpollinterval, IfRetransInterval=ifretransinterval, IfRtrPriority=ifrtrpriority, IfTransitDelay=iftransitdelay, IfType=iftype, IfAdminStat=ifadminstat, IfAreaId=ifareaid, IfHelloInterval=ifhellointerval, IfRtrDeadInterval=ifrtrdeadinterval)

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
		response, error = swtch.deleteOspfIfEntry(IfIpAddress=ifipaddress, AddressLessIf=addresslessif)

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
		response, error = swtch.deleteOspfIfEntryById(ObjectId=objectid

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
		response, error = swtch.updateOspfIfEntry(IfIpAddress=ifipaddress, AddressLessIf=addresslessif, IfPollInterval=ifpollinterval, IfRetransInterval=ifretransinterval, IfRtrPriority=ifrtrpriority, IfTransitDelay=iftransitdelay, IfType=iftype, IfAdminStat=ifadminstat, IfAreaId=ifareaid, IfHelloInterval=ifhellointerval, IfRtrDeadInterval=ifrtrdeadinterval)

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
		response, error = swtch.updateOspfIfEntryById(ObjectId=objectidIfPollInterval=ifpollinterval, IfRetransInterval=ifretransinterval, IfRtrPriority=ifrtrpriority, IfTransitDelay=iftransitdelay, IfType=iftype, IfAdminStat=ifadminstat, IfAreaId=ifareaid, IfHelloInterval=ifhellointerval, IfRtrDeadInterval=ifrtrdeadinterval)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
