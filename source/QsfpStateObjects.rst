QsfpState Object
=============================================================

*state/Qsfp*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+----------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |   **DESCRIPTION**    | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+----------------------+-------------+------------------+
| QsfpId **[KEY]**   | int32         | QSFP Id              | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| UDF1               | float64       | User defined field 1 | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| VendorName         | string        | Vendor Name          | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| VendorRevision     | string        | Vendor Revision      | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| DataCode           | string        | Data Code            | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| MinBER             | float64       | Minimum BER          | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| UDF0               | float64       | User defined field 0 | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| CurrBER            | float64       | Current BER          | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| UDF3               | float64       | User defined field 3 | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| VendorOUI          | string        | Vendor OUI           | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| Temperature        | float64       | Current temperature  | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| AccBER             | float64       | Accumulated BER      | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| MaxBER             | float64       | Maximum BER          | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| Present            | bool          | Present or Not Value | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| VendorSerialNumber | string        | Vendor Serial Number | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| Voltage            | float64       | Current Voltage      | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| UDF2               | float64       | User defined field 2 | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+
| VendorPartNumber   | string        | Vendor Part Number   | N/A         | N/A              |
+--------------------+---------------+----------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/Qsfp
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/Qsfps?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/QsfpState/<uuid>


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
		response, error = swtch.getQsfpState(QsfpId=qsfpid)

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
		response, error = swtch.getQsfpStateById(ObjectId=objectid)

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
		response, error = swtch.getAllQsfpStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


