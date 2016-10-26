OspfIfEntryState Object
=============================================================

*state/OspfIfEntry*
------------------------------------

- Multiple objects of this type can exist in a system.

+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
|     **PARAMETER NAME**     | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfIpAddress **[KEY]**      | string        | The IP address of this OSPF    | N/A         | N/A                            |
|                            |               | interface.                     |             |                                |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| AddressLessIf **[KEY]**    | int32         | For the purpose of easing the  | N/A         | N/A                            |
|                            |               | instancing of addressed and    |             |                                |
|                            |               | addressless interfaces; this   |             |                                |
|                            |               | variable takes the value 0 on  |             |                                |
|                            |               | interfaces with IP addresses   |             |                                |
|                            |               | and the corresponding value of |             |                                |
|                            |               | ifIndex for interfaces having  |             |                                |
|                            |               | no IP address.                 |             |                                |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfBackupDesignatedRouterId | string        | The Router ID of the backup    | N/A         | N/A                            |
|                            |               | designated router.             |             |                                |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfDesignatedRouter         | string        | The IP address of the          | N/A         | N/A                            |
|                            |               | designated router.             |             |                                |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfDesignatedRouterId       | string        | The Router ID of the           | N/A         | N/A                            |
|                            |               | designated router.             |             |                                |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfBackupDesignatedRouter   | string        | The IP address of the backup   | N/A         | N/A                            |
|                            |               | designated router.             |             |                                |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfEvents                   | uint32        | The number of times this       | N/A         | N/A                            |
|                            |               | OSPF interface has changed     |             |                                |
|                            |               | its state or an error has      |             |                                |
|                            |               | occurred.  Discontinuities in  |             |                                |
|                            |               | the value of this counter can  |             |                                |
|                            |               | occur at re-initialization of  |             |                                |
|                            |               | the management system          |             |                                |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfLsaCount                 | uint32        | The total number of link-local | N/A         | N/A                            |
|                            |               | link state advertisements in   |             |                                |
|                            |               | this interface's link-local    |             |                                |
|                            |               | link state database.           |             |                                |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfState                    | int32         | The OSPF Interface State.      | N/A         | otherDesignatedRouter(7),      |
|                            |               |                                |             | backupDesignatedRouter(6),     |
|                            |               |                                |             | loopback(2), down(1),          |
|                            |               |                                |             | designatedRouter(5),           |
|                            |               |                                |             | waiting(3), pointToPoint(4)    |
+----------------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/OspfIfEntry
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/OspfIfEntrys?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfIfEntryState/<uuid>


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
		response, error = swtch.getOspfIfEntryState(IfIpAddress=ifipaddress, AddressLessIf=addresslessif)

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
		response, error = swtch.getOspfIfEntryStateById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfIfEntryStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


