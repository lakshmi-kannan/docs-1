LogicalIntfState Object
=============================================================

*state/LogicalIntf*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Name **[KEY]**     | string        | Name of logical interface      | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfOutErrors        | int64         | RFC2233 Total number of        | N/A         | N/A              |
|                    |               | packets discarded and not      |             |                  |
|                    |               | transmitted due to packet      |             |                  |
|                    |               | errors                         |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfOutOctets        | int64         | RFC2233 Total number of octets | N/A         | N/A              |
|                    |               | transmitted on this port       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| OperState          | string        | Operational state of logical   | N/A         | N/A              |
|                    |               | interface                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SrcMac             | string        | Source Mac assigned to the     | N/A         | N/A              |
|                    |               | interface                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfInDiscards       | int64         | RFC2233 Total number of        | N/A         | N/A              |
|                    |               | inbound packets that were      |             |                  |
|                    |               | discarded                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfInOctets         | int64         | RFC2233 Total number of octets | N/A         | N/A              |
|                    |               | received on this port          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfInUnknownProtos  | int64         | RFC2233 Total number of        | N/A         | N/A              |
|                    |               | inbound packets discarded due  |             |                  |
|                    |               | to unknown protocol            |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfOutDiscards      | int64         | RFC2233 Total number of error  | N/A         | N/A              |
|                    |               | free packets discarded and not |             |                  |
|                    |               | transmitted                    |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfOutUcastPkts     | int64         | RFC2233 Total number of        | N/A         | N/A              |
|                    |               | unicast packets transmitted on |             |                  |
|                    |               | this port                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfInErrors         | int64         | RFC2233 Total number of        | N/A         | N/A              |
|                    |               | inbound packets that contained |             |                  |
|                    |               | an error                       |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfInUcastPkts      | int64         | RFC2233 Total number of        | N/A         | N/A              |
|                    |               | unicast packets received on    |             |                  |
|                    |               | this port                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IfIndex            | int32         | System assigned interface id   | N/A         | N/A              |
|                    |               | for this logical interface     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/LogicalIntf
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/LogicalIntfs?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/LogicalIntfState/<uuid>


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
		response, error = swtch.getLogicalIntfState(Name=name)

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
		response, error = swtch.getLogicalIntfStateById(ObjectId=objectid)

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
		response, error = swtch.getAllLogicalIntfStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


