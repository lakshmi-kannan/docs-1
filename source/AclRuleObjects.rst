AclRule Object
=============================================================

*config/AclRule*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+--------------------+---------------+--------------------------------+-------------+------------------+
| RuleName **[KEY]** | string        | Acl rule name                  | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Action             | string        | Type of action (ALLOW/DENY)    | Allow       | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| L4MaxPort          | int32         | Max port when l4 port is       |           0 | N/A              |
|                    |               | specified as range             |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| L4SrcPort          | int32         | TCP/UDP source port            |           0 | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SourceMac          | string        | Source MAC address.            | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SrcPort            | string        | Source Port(used for mlag)     | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| DestIp             | string        | Destination IP address         | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| DstPort            | string        | Dest Port(used for mlag)       |           0 | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| L4DstPort          | int32         | TCP/UDP destionation port      | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| L4PortMatch        | string        | match condition can be         | NA          | N/A              |
|                    |               | EQ(equal)                      |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SourceIp           | string        | Source IP address              | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| SourceMask         | string        | Network mask for source IP     | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| DestMac            | string        | Destination MAC address        | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| DestMask           | string        | Network mark for dest IP       | N/A         | N/A              |
+--------------------+---------------+--------------------------------+-------------+------------------+
| L4MinPort          | int32         | Min port when l4 port is       |           0 | N/A              |
|                    |               | specified as range             |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+
| Proto              | string        | Protocol type                  | N/A         | N/A              |
|                    |               | TCP/UDP/ICMPv4/ICMPv6          |             |                  |
+--------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/AclRule
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/AclRule/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/AclRules?CurrentMarker=<x>\\&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/AclRule
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/AclRule
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/AclRule<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/AclRule
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/AclRule<uuid>


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
		response, error = swtch.getAclRule(RuleName=rulename)

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
		response, error = swtch.getAclRuleById(ObjectId=objectid)

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
		response, error = swtch.getAllAclRules()

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
		response, error = swtch.createAclRule(RuleName=rulename, Action=action, L4MaxPort=l4maxport, L4SrcPort=l4srcport, SourceMac=sourcemac, SrcPort=srcport, DestIp=destip, DstPort=dstport, L4DstPort=l4dstport, L4PortMatch=l4portmatch, SourceIp=sourceip, SourceMask=sourcemask, DestMac=destmac, DestMask=destmask, L4MinPort=l4minport, Proto=proto)

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
		response, error = swtch.deleteAclRule(RuleName=rulename)

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
		response, error = swtch.deleteAclRuleById(ObjectId=objectid

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
		response, error = swtch.updateAclRule(RuleName=rulename, Action=action, L4MaxPort=l4maxport, L4SrcPort=l4srcport, SourceMac=sourcemac, SrcPort=srcport, DestIp=destip, DstPort=dstport, L4DstPort=l4dstport, L4PortMatch=l4portmatch, SourceIp=sourceip, SourceMask=sourcemask, DestMac=destmac, DestMask=destmask, L4MinPort=l4minport, Proto=proto)

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
		response, error = swtch.updateAclRuleById(ObjectId=objectidAction=action, L4MaxPort=l4maxport, L4SrcPort=l4srcport, SourceMac=sourcemac, SrcPort=srcport, DestIp=destip, DstPort=dstport, L4DstPort=l4dstport, L4PortMatch=l4portmatch, SourceIp=sourceip, SourceMask=sourcemask, DestMac=destmac, DestMask=destmask, L4MinPort=l4minport, Proto=proto)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
