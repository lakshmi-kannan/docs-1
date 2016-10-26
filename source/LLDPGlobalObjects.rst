LLDPGlobal Object
=============================================================

*config/LLDPGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+----------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |   **VALID VALUES**   |
+--------------------+---------------+--------------------------------+-------------+----------------------+
| Vrf **[KEY]**      | string        | LLDP Global Config For Default | default     | N/A                  |
|                    |               | VRF                            |             |                      |
+--------------------+---------------+--------------------------------+-------------+----------------------+
| Enable             | bool          | Enable/Disable LLDP Globally   | false       | N/A                  |
+--------------------+---------------+--------------------------------+-------------+----------------------+
| SnoopAndDrop       | bool          | Operational mode to determine  | false       | N/A                  |
|                    |               | whether LLDP traffic is        |             |                      |
|                    |               | bi-directionally forwarded.    |             |                      |
|                    |               | This configuration is only     |             |                      |
|                    |               | available on select platforms  |             |                      |
+--------------------+---------------+--------------------------------+-------------+----------------------+
| TranmitInterval    | int32         | LLDP Re-Transmit Interval in   |          30 | N/A                  |
|                    |               | seconds                        |             |                      |
+--------------------+---------------+--------------------------------+-------------+----------------------+
| TxRxMode           | string        | Transmit/Receive mode          | TxRx        | TxOnly, RxOnly, TxRx |
|                    |               | configruration for the LLDP    |             |                      |
|                    |               | agent                          |             |                      |
+--------------------+---------------+--------------------------------+-------------+----------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/LLDPGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/LLDPGlobal/<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/LLDPGlobal
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/LLDPGlobal<uuid>


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
		response, error = swtch.getLLDPGlobal(Vrf=vrf)

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
		response, error = swtch.getLLDPGlobalById(ObjectId=objectid)

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
		response, error = swtch.getAllLLDPGlobals()

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
		response, error = swtch.updateLLDPGlobal(Vrf=vrf, Enable=enable, SnoopAndDrop=snoopanddrop, TranmitInterval=tranmitinterval, TxRxMode=txrxmode)

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
		response, error = swtch.updateLLDPGlobalById(ObjectId=objectidEnable=enable, SnoopAndDrop=snoopanddrop, TranmitInterval=tranmitinterval, TxRxMode=txrxmode)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
