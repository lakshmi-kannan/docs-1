OspfAreaEntry Object
=============================================================

*config/OspfAreaEntry*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AreaId **[KEY]**   | string        | A 32-bit integer uniquely      | N/A         | N/A                            |
|                    |               | identifying an area. Area ID   |             |                                |
|                    |               | 0.0.0.0 is used for the OSPF   |             |                                |
|                    |               | backbone.                      |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AreaSummary        | int32         | The variable ospfAreaSummary   | N/A         | sendAreaSummary(2),            |
|                    |               | controls the import of summary |             | noAreaSummary(1)               |
|                    |               | LSAs into stub and NSSA areas. |             |                                |
|                    |               | It has no effect on other      |             |                                |
|                    |               | areas.  If it is noAreaSummary |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AuthType           | int32         | The authentication type        | N/A         | none(0), simplePassword(1),    |
|                    |               | specified for an area.         |             | md5(2)                         |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| ImportAsExtern     | int32         | Indicates if an area is a stub | N/A         | importExternal(1),             |
|                    |               | area                           |             | importNoExternal(2),           |
|                    |               |                                |             | importNssa(3)                  |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| StubDefaultCost    | int32         | For ABR this cost indicates    |          10 | N/A                            |
|                    |               | default cost for summary LSA.  |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/OspfAreaEntry
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfAreaEntry/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfAreaEntrys?CurrentMarker=<x>\\&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/OspfAreaEntry
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/OspfAreaEntry
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/OspfAreaEntry<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/OspfAreaEntry
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/OspfAreaEntry<uuid>


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
		response, error = swtch.getOspfAreaEntry(AreaId=areaid)

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
		response, error = swtch.getOspfAreaEntryById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfAreaEntrys()

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
		response, error = swtch.createOspfAreaEntry(AreaId=areaid, AreaSummary=areasummary, AuthType=authtype, ImportAsExtern=importasextern, StubDefaultCost=stubdefaultcost)

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
		response, error = swtch.deleteOspfAreaEntry(AreaId=areaid)

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
		response, error = swtch.deleteOspfAreaEntryById(ObjectId=objectid

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
		response, error = swtch.updateOspfAreaEntry(AreaId=areaid, AreaSummary=areasummary, AuthType=authtype, ImportAsExtern=importasextern, StubDefaultCost=stubdefaultcost)

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
		response, error = swtch.updateOspfAreaEntryById(ObjectId=objectidAreaSummary=areasummary, AuthType=authtype, ImportAsExtern=importasextern, StubDefaultCost=stubdefaultcost)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
