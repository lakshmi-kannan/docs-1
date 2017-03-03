OspfGlobal Object
=============================================================

*config/OspfGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| Vrf **[KEY]**      | string        | VRF id for OSPF global config  | default     | N/A                            |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| RestartSupport     | int32         | *** This element is added for  | N/A         | plannedAndUnplanned(3),        |
|                    |               | future use. *** The router's   |             | none(1), plannedOnly(2)        |
|                    |               | support for OSPF graceful      |             |                                |
|                    |               | restart. Options include       |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| RouterId           | string        | A 32-bit integer uniquely      | 0.0.0.0     | N/A                            |
|                    |               | identifying the router in      |             |                                |
|                    |               | the Autonomous System. By      |             |                                |
|                    |               | convention                     |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| TOSSupport         | bool          | *** This element is added for  | false       | N/A                            |
|                    |               | future use. *** The router's   |             |                                |
|                    |               | support for type-of-service    |             |                                |
|                    |               | routing. This object is        |             |                                |
|                    |               | persistent and when written    |             |                                |
|                    |               | the entity SHOULD save         |             |                                |
|                    |               | the change to non-volatile     |             |                                |
|                    |               | storage.                       |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| ASBdrRtrStatus     | bool          | A flag to note whether this    | N/A         | N/A                            |
|                    |               | router is configured as an     |             |                                |
|                    |               | Autonomous System Border       |             |                                |
|                    |               | Router.  This object is        |             |                                |
|                    |               | persistent and when written    |             |                                |
|                    |               | the entity SHOULD save         |             |                                |
|                    |               | the change to non-volatile     |             |                                |
|                    |               | storage.                       |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminStat          | int32         | Indicates if OSPF is enabled   | N/A         | N/A                            |
|                    |               | globally                       |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| ReferenceBandwidth | uint32        | Reference bandwidth            |         100 | N/A                            |
|                    |               | in kilobits/second for         |             |                                |
|                    |               | calculating default interface  |             |                                |
|                    |               | metrics. Unit                  |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| RestartInterval    | int32         | *** This element is added for  | N/A         | N/A                            |
|                    |               | future use. *** Configured     |             |                                |
|                    |               | OSPF graceful restart timeout  |             |                                |
|                    |               | interval. This object is       |             |                                |
|                    |               | persistent and when written    |             |                                |
|                    |               | the entity SHOULD save         |             |                                |
|                    |               | the change to non-volatile     |             |                                |
|                    |               | storage.                       |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/OspfGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfGlobal/<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/OspfGlobal
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/OspfGlobal<uuid>


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
		response, error = swtch.getOspfGlobal(Vrf=vrf)

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
		response, error = swtch.getOspfGlobalById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfGlobals()

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
		response, error = swtch.updateOspfGlobal(Vrf=vrf, RestartSupport=restartsupport, RouterId=routerid, TOSSupport=tossupport, ASBdrRtrStatus=asbdrrtrstatus, AdminStat=adminstat, ReferenceBandwidth=referencebandwidth, RestartInterval=restartinterval)

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
		response, error = swtch.updateOspfGlobalById(ObjectId=objectidRestartSupport=restartsupport, RouterId=routerid, TOSSupport=tossupport, ASBdrRtrStatus=asbdrrtrstatus, AdminStat=adminstat, ReferenceBandwidth=referencebandwidth, RestartInterval=restartinterval)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
