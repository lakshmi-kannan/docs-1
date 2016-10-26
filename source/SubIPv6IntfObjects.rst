SubIPv6Intf Object
=============================================================

*config/SubIPv6Intf*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IntfRef **[KEY]**  | string        | Intf name of system generated  | N/A         | N/A              |
|                    |               | id (ifindex) of the ipv4Intf   |             |                  |
|                    |               | where sub interface is to be   |             |                  |
|                    |               | configured                     |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| IpAddr **[KEY]**   | string        | Ip Address for the interface   | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Enable             | bool          | Enable or disable this         | false       | N/A              |
|                    |               | interface                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| MacAddr            | string        | Mac address to be used for     | N/A         | N/A              |
|                    |               | the sub interface. If none     |             |                  |
|                    |               | specified IPv4Intf mac address |             |                  |
|                    |               | will be used                   |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Type               | string        | Type of interface              | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/SubIPv6Intf
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/SubIPv6Intf/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/SubIPv6Intfs?CurrentMarker=<x>&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/SubIPv6Intf
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/SubIPv6Intf
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/SubIPv6Intf<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/SubIPv6Intf
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/SubIPv6Intf<uuid>


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
		response, error = swtch.getSubIPv6Intf(IntfRef=intfref, IpAddr=ipaddr)

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
		response, error = swtch.getSubIPv6IntfById(ObjectId=objectid)

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
		response, error = swtch.getAllSubIPv6Intfs()

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
		response, error = swtch.createSubIPv6Intf(IntfRef=intfref, IpAddr=ipaddr, Enable=enable, MacAddr=macaddr, Type=type)

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
		response, error = swtch.deleteSubIPv6Intf(IntfRef=intfref, IpAddr=ipaddr)

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
		response, error = swtch.deleteSubIPv6IntfById(ObjectId=objectid

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
		response, error = swtch.updateSubIPv6Intf(IntfRef=intfref, IpAddr=ipaddr, Enable=enable, MacAddr=macaddr, Type=type)

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
		response, error = swtch.updateSubIPv6IntfById(ObjectId=objectidEnable=enable, MacAddr=macaddr, Type=type)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
