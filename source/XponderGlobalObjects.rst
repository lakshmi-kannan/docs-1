XponderGlobal Object
=============================================================

*config/XponderGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+---------------------+---------------+--------------------------------+----------------------------+--------------------------------+
| **PARAMETER NAME**  | **DATA TYPE** |        **DESCRIPTION**         |        **DEFAULT**         |        **VALID VALUES**        |
+---------------------+---------------+--------------------------------+----------------------------+--------------------------------+
| XponderId **[KEY]** | uint8         | Xponder module identifier      |                          0 | N/A                            |
+---------------------+---------------+--------------------------------+----------------------------+--------------------------------+
| XponderDescription  | string        | User configurable description  | This is a Voyager platform | N/A                            |
|                     |               | string for the xponder module  |                            |                                |
+---------------------+---------------+--------------------------------+----------------------------+--------------------------------+
| XponderMode         | string        | Global operational mode of     | OutOfService               | InServiceWire, InServiceRegen, |
|                     |               | Xponder module                 |                            | InServiceOverSub,              |
|                     |               |                                |                            | InServicePacketOptical,        |
|                     |               |                                |                            | OutOfService                   |
+---------------------+---------------+--------------------------------+----------------------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/XponderGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/XponderGlobal/<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/XponderGlobal
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/XponderGlobal<uuid>


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
		response, error = swtch.getXponderGlobal(XponderId=xponderid)

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
		response, error = swtch.getXponderGlobalById(ObjectId=objectid)

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
		response, error = swtch.getAllXponderGlobals()

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
		response, error = swtch.updateXponderGlobal(XponderId=xponderid, XponderDescription=xponderdescription, XponderMode=xpondermode)

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
		response, error = swtch.updateXponderGlobalById(ObjectId=objectidXponderDescription=xponderdescription, XponderMode=xpondermode)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
