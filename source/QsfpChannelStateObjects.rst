QsfpChannelState Object
=============================================================

*state/QsfpChannel*
------------------------------------

- Multiple objects of this type can exist in a system.

+----------------------+---------------+------------------------------+-------------+------------------+
|  **PARAMETER NAME**  | **DATA TYPE** |       **DESCRIPTION**        | **DEFAULT** | **VALID VALUES** |
+----------------------+---------------+------------------------------+-------------+------------------+
| ChannelNum **[KEY]** | int32         | Qsfp Channel Number          | N/A         | N/A              |
+----------------------+---------------+------------------------------+-------------+------------------+
| QsfpId **[KEY]**     | int32         | QSFP Id                      | N/A         | N/A              |
+----------------------+---------------+------------------------------+-------------+------------------+
| Present              | bool          | Present or Not Value         | N/A         | N/A              |
+----------------------+---------------+------------------------------+-------------+------------------+
| RXPower              | float64       | Rx power on channel 1        | N/A         | N/A              |
+----------------------+---------------+------------------------------+-------------+------------------+
| TXBias               | float64       | Tx Current Bias on channel 1 | N/A         | N/A              |
+----------------------+---------------+------------------------------+-------------+------------------+
| TXPower              | float64       | Rx power on channel 1        | N/A         | N/A              |
+----------------------+---------------+------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/QsfpChannel
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/QsfpChannels?CurrentMarker=<x>\\&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/QsfpChannelState/<uuid>


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
		response, error = swtch.getQsfpChannelState(ChannelNum=channelnum, QsfpId=qsfpid)

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
		response, error = swtch.getQsfpChannelStateById(ObjectId=objectid)

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
		response, error = swtch.getAllQsfpChannelStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


