OspfNbrEntryState Object
=============================================================

*state/OspfNbrEntry*
------------------------------------

- Multiple objects of this type can exist in a system.

+-------------------------------+---------------+--------------------------------+-------------+--------------------------------+
|      **PARAMETER NAME**       | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+-------------------------------+---------------+--------------------------------+-------------+--------------------------------+
| NbrIpAddr **[KEY]**           | string        | The IP address this neighbor   | N/A         | N/A                            |
|                               |               | is using in its IP source      |             |                                |
|                               |               | address.  Note that            |             |                                |
+-------------------------------+---------------+--------------------------------+-------------+--------------------------------+
| NbrAddressLessIndex **[KEY]** | int32         | On an interface having an IP   | N/A         | N/A                            |
|                               |               | address                        |             |                                |
+-------------------------------+---------------+--------------------------------+-------------+--------------------------------+
| NbrHelloSuppressed            | bool          | *** This element is added      | N/A         | N/A                            |
|                               |               | for future use. *** Indicates  |             |                                |
|                               |               | whether Hellos are being       |             |                                |
|                               |               | suppressed to the neighbor.    |             |                                |
+-------------------------------+---------------+--------------------------------+-------------+--------------------------------+
| NbrOptions                    | int32         | A bit mask corresponding to    | N/A         | N/A                            |
|                               |               | the neighbor's options field.  |             |                                |
|                               |               | Bit 0                          |             |                                |
+-------------------------------+---------------+--------------------------------+-------------+--------------------------------+
| NbrRtrId                      | string        | A 32-bit integer (represented  | N/A         | N/A                            |
|                               |               | as a type IpAddress) uniquely  |             |                                |
|                               |               | identifying the neighboring    |             |                                |
|                               |               | router in the Autonomous       |             |                                |
|                               |               | System.                        |             |                                |
+-------------------------------+---------------+--------------------------------+-------------+--------------------------------+
| NbrState                      | string        | The state of the relationship  | N/A         | exchangeStart(5), loading(7),  |
|                               |               | with this neighbor.            |             | attempt(2), exchange(6),       |
|                               |               |                                |             | down(1), init(3), full(8),     |
|                               |               |                                |             | twoWay(4)                      |
+-------------------------------+---------------+--------------------------------+-------------+--------------------------------+
| NbrEvents                     | uint32        | The number of times this       | N/A         | N/A                            |
|                               |               | neighbor relationship has      |             |                                |
|                               |               | changed state or an error has  |             |                                |
|                               |               | occurred.  Discontinuities in  |             |                                |
|                               |               | the value of this counter can  |             |                                |
|                               |               | occur at re-initialization of  |             |                                |
|                               |               | the management system          |             |                                |
+-------------------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/OspfNbrEntry
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/OspfNbrEntrys?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfNbrEntryState/<uuid>


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
		response, error = swtch.getOspfNbrEntryState(NbrIpAddr=nbripaddr, NbrAddressLessIndex=nbraddresslessindex)

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
		response, error = swtch.getOspfNbrEntryStateById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfNbrEntryStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


