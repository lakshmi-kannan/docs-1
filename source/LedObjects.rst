Led Object
=============================================================

*config/Led*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+-----------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** | **DESCRIPTION** | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+-----------------+-------------+------------------+
| LedId **[KEY]**    | int32         | LED id          |           0 | N/A              |
+--------------------+---------------+-----------------+-------------+------------------+
| LedAdmin           | string        | LED ON/OFF      | N/A         | N/A              |
+--------------------+---------------+-----------------+-------------+------------------+
| LedSetColor        | string        | LED set color   | N/A         | N/A              |
+--------------------+---------------+-----------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/Led
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/Led/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/Leds?CurrentMarker=<x>\\&Count=<y>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/Led
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/Led<uuid>


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
		response, error = swtch.getLed(LedId=ledid)

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
		response, error = swtch.getLedById(ObjectId=objectid)

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
		response, error = swtch.getAllLeds()

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
		response, error = swtch.updateLed(LedId=ledid, LedAdmin=ledadmin, LedSetColor=ledsetcolor)

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
		response, error = swtch.updateLedById(ObjectId=objectidLedAdmin=ledadmin, LedSetColor=ledsetcolor)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
