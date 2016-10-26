NDPGlobal Object
=============================================================

*config/NDPGlobal*
------------------------------------

- Only one object of this type can exist in a system.

+-----------------------------+---------------+--------------------------------+-------------+------------------+
|     **PARAMETER NAME**      | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| Vrf **[KEY]**               | string        | System Vrf                     | default     | N/A              |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| ReachableTime               | int32         | The time a neighbor is         |          10 | N/A              |
|                             |               | considered reachable after     |             |                  |
|                             |               | receiving a reachability       |             |                  |
|                             |               | confirmation in minutes        |             |                  |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| RetransmitInterval          | int32         | The time between               |           1 | N/A              |
|                             |               | retransmissions of Neighbor    |             |                  |
|                             |               | Solicitation messages to a     |             |                  |
|                             |               | neighbor when resolving the    |             |                  |
|                             |               | address or when probing the    |             |                  |
|                             |               | reachability of a neighbor in  |             |                  |
|                             |               | ms                             |             |                  |
+-----------------------------+---------------+--------------------------------+-------------+------------------+
| RouterAdvertisementInterval | int32         | Delay between each router      |           5 | N/A              |
|                             |               | advertisements in seconds      |             |                  |
+-----------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/NDPGlobal
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/NDPGlobal/<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/NDPGlobal
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/NDPGlobal<uuid>


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
		response, error = swtch.getNDPGlobal(Vrf=vrf)

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
		response, error = swtch.getNDPGlobalById(ObjectId=objectid)

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
		response, error = swtch.getAllNDPGlobals()

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
		response, error = swtch.updateNDPGlobal(Vrf=vrf, ReachableTime=reachabletime, RetransmitInterval=retransmitinterval, RouterAdvertisementInterval=routeradvertisementinterval)

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
		response, error = swtch.updateNDPGlobalById(ObjectId=objectidReachableTime=reachabletime, RetransmitInterval=retransmitinterval, RouterAdvertisementInterval=routeradvertisementinterval)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
