LLDPIntf Object
=============================================================

*config/LLDPIntf*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+----------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |   **VALID VALUES**   |
+--------------------+---------------+--------------------------------+-------------+----------------------+
| IntfRef **[KEY]**  | string        | IfIndex where lldp needs is    | None        | N/A                  |
|                    |               | enabled/disabled               |             |                      |
+--------------------+---------------+--------------------------------+-------------+----------------------+
| TxRxMode           | string        | Transmit/Receive mode          | TxRx        | TxOnly, RxOnly, TxRx |
|                    |               | configruration for the LLDP    |             |                      |
|                    |               | agent specific to an interface |             |                      |
+--------------------+---------------+--------------------------------+-------------+----------------------+
| Enable             | bool          | Enable/Disable lldp config Per | true        | N/A                  |
|                    |               | Port                           |             |                      |
+--------------------+---------------+--------------------------------+-------------+----------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/LLDPIntf
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/LLDPIntf/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/LLDPIntfs?CurrentMarker=<x>&Count=<y>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/LLDPIntf
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/LLDPIntf<uuid>


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
		response, error = swtch.getLLDPIntf(IntfRef=intfref)

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
		response, error = swtch.getLLDPIntfById(ObjectId=objectid)

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
		response, error = swtch.getAllLLDPIntfs()

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
		response, error = swtch.updateLLDPIntf(IntfRef=intfref, TxRxMode=txrxmode, Enable=enable)

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
		response, error = swtch.updateLLDPIntfById(ObjectId=objectidTxRxMode=txrxmode, Enable=enable)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
