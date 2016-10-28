OspfLsdbEntryState Object
=============================================================

*state/OspfLsdbEntry*
------------------------------------

- Multiple objects of this type can exist in a system.

+------------------------+---------------+--------------------------------+-------------+--------------------------------+
|   **PARAMETER NAME**   | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+------------------------+---------------+--------------------------------+-------------+--------------------------------+
| LsdbLsid **[KEY]**     | string        | The Link State ID is an LS     | N/A         | N/A                            |
|                        |               | Type Specific field containing |             |                                |
|                        |               | either a Router ID or an IP    |             |                                |
|                        |               | address; it identifies the     |             |                                |
|                        |               | piece of the routing domain    |             |                                |
|                        |               | that is being described by the |             |                                |
|                        |               | advertisement.                 |             |                                |
+------------------------+---------------+--------------------------------+-------------+--------------------------------+
| LsdbRouterId **[KEY]** | string        | The 32-bit number that         | N/A         | N/A                            |
|                        |               | uniquely identifies the        |             |                                |
|                        |               | originating router in the      |             |                                |
|                        |               | Autonomous System.             |             |                                |
+------------------------+---------------+--------------------------------+-------------+--------------------------------+
| LsdbType **[KEY]**     | int32         | The type of the link state     | N/A         | routerLink(1),                 |
|                        |               | advertisement. Each link       |             | asSummaryLink(4),              |
|                        |               | state type has a separate      |             | asExternalLink(5),             |
|                        |               | advertisement format.  Note    |             | nssaExternalLink(7),           |
|                        |               |                                |             | networkLink(2),                |
|                        |               |                                |             | multicastLink(6),              |
|                        |               |                                |             | summaryLink(3),                |
|                        |               |                                |             | areaOpaqueLink(10)             |
+------------------------+---------------+--------------------------------+-------------+--------------------------------+
| LsdbAreaId **[KEY]**   | string        | The 32-bit identifier of the   | N/A         | N/A                            |
|                        |               | area from which the LSA was    |             |                                |
|                        |               | received.                      |             |                                |
+------------------------+---------------+--------------------------------+-------------+--------------------------------+
| LsdbChecksum           | int32         | This field is the checksum of  | N/A         | N/A                            |
|                        |               | the complete contents of the   |             |                                |
|                        |               | advertisement                  |             |                                |
+------------------------+---------------+--------------------------------+-------------+--------------------------------+
| LsdbSequence           | int32         | The sequence number field      | N/A         | N/A                            |
|                        |               | is a signed 32-bit integer.    |             |                                |
|                        |               |  It starts with the value      |             |                                |
|                        |               | '80000001'h                    |             |                                |
+------------------------+---------------+--------------------------------+-------------+--------------------------------+
| LsdbAdvertisement      | string        | The entire link state          | N/A         | N/A                            |
|                        |               | advertisement                  |             |                                |
+------------------------+---------------+--------------------------------+-------------+--------------------------------+
| LsdbAge                | int32         | This field is the age of the   | N/A         | N/A                            |
|                        |               | link state advertisement in    |             |                                |
|                        |               | seconds.                       |             |                                |
+------------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/OspfLsdbEntry
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/OspfLsdbEntrys?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfLsdbEntryState/<uuid>


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
		response, error = swtch.getOspfLsdbEntryState(LsdbLsid=lsdblsid, LsdbRouterId=lsdbrouterid, LsdbType=lsdbtype, LsdbAreaId=lsdbareaid)

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
		response, error = swtch.getOspfLsdbEntryStateById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfLsdbEntryStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


