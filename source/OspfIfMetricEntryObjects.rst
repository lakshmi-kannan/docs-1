OspfIfMetricEntry Object
=============================================================

*config/OspfIfMetricEntry*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------------------+---------------+--------------------------------+-------------+------------------+
|       **PARAMETER NAME**       | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------------------+---------------+--------------------------------+-------------+------------------+
| IfMetricAddressLessIf          | int32         | For the purpose of easing the  | N/A         | N/A              |
| **[KEY]**                      |               | instancing of addressed and    |             |                  |
|                                |               | addressless interfaces; this   |             |                  |
|                                |               | variable takes the value 0 on  |             |                  |
|                                |               | interfaces with IP addresses   |             |                  |
|                                |               | and the value of ifIndex       |             |                  |
|                                |               | for interfaces having no IP    |             |                  |
|                                |               | address.  On row creation      |             |                  |
+--------------------------------+---------------+--------------------------------+-------------+------------------+
| IfMetricIpAddress **[KEY]**    | string        | The IP address of this OSPF    | N/A         | N/A              |
|                                |               | interface.  On row creation    |             |                  |
+--------------------------------+---------------+--------------------------------+-------------+------------------+
| IfMetricTOS **[KEY]**          | int32         | The Type of Service metric     | N/A         | N/A              |
|                                |               | being referenced. On row       |             |                  |
|                                |               | creation                       |             |                  |
+--------------------------------+---------------+--------------------------------+-------------+------------------+
| IfMetricValue                  | int32         | The metric of using this Type  | N/A         | N/A              |
|                                |               | of Service on this interface.  |             |                  |
|                                |               | The default value of the TOS 0 |             |                  |
|                                |               | metric is 10^8 / ifSpeed.      |             |                  |
+--------------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/OspfIfMetricEntry
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfIfMetricEntry/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/OspfIfMetricEntrys?CurrentMarker=<x>\\&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/OspfIfMetricEntry
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/OspfIfMetricEntry
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/OspfIfMetricEntry<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/OspfIfMetricEntry
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/OspfIfMetricEntry<uuid>


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
		response, error = swtch.getOspfIfMetricEntry(IfMetricAddressLessIf=ifmetricaddresslessif, IfMetricIpAddress=ifmetricipaddress, IfMetricTOS=ifmetrictos)

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
		response, error = swtch.getOspfIfMetricEntryById(ObjectId=objectid)

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
		response, error = swtch.getAllOspfIfMetricEntrys()

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
		response, error = swtch.createOspfIfMetricEntry(IfMetricAddressLessIf=ifmetricaddresslessif, IfMetricIpAddress=ifmetricipaddress, IfMetricTOS=ifmetrictos, IfMetricValue=ifmetricvalue)

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
		response, error = swtch.deleteOspfIfMetricEntry(IfMetricAddressLessIf=ifmetricaddresslessif, IfMetricIpAddress=ifmetricipaddress, IfMetricTOS=ifmetrictos)

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
		response, error = swtch.deleteOspfIfMetricEntryById(ObjectId=objectid

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
		response, error = swtch.updateOspfIfMetricEntry(IfMetricAddressLessIf=ifmetricaddresslessif, IfMetricIpAddress=ifmetricipaddress, IfMetricTOS=ifmetrictos, IfMetricValue=ifmetricvalue)

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
		response, error = swtch.updateOspfIfMetricEntryById(ObjectId=objectidIfMetricValue=ifmetricvalue)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
