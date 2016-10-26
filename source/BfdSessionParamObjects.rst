BfdSessionParam Object
=============================================================

*config/BfdSessionParam*
------------------------------------

- Multiple objects of this type can exist in a system.

+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
|    **PARAMETER NAME**     | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| Name **[KEY]**            | string        | Session parameters             | N/A         | N/A                            |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| AuthData                  | string        | Authentication password        | snaproute   | N/A                            |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| AuthKeyId                 | uint32        | Authentication key id          |           1 | N/A                            |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| AuthType                  | string        | Authentication type            | simple      | metmd5, keyedmd5, metsha1,     |
|                           |               |                                |             | keyedsha1, simple              |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| DemandEnabled             | bool          | Enable or disable demand mode  | false       | N/A                            |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| DesiredMinTxInterval      | uint32        | Desired minimum tx interval in |        1000 | N/A                            |
|                           |               | ms                             |             |                                |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| RequiredMinEchoRxInterval | uint32        | Required minimum echo rx       |           0 | N/A                            |
|                           |               | interval in ms                 |             |                                |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| AuthenticationEnabled     | bool          | Enable or disable              | false       | N/A                            |
|                           |               | authentication                 |             |                                |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| LocalMultiplier           | uint32        | Detection multiplier           |           3 | N/A                            |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+
| RequiredMinRxInterval     | uint32        | Required minimum rx interval   |        1000 | N/A                            |
|                           |               | in ms                          |             |                                |
+---------------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/BfdSessionParam
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BfdSessionParam/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/BfdSessionParams?CurrentMarker=<x>&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/BfdSessionParam
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/BfdSessionParam
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/BfdSessionParam<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/BfdSessionParam
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/BfdSessionParam<uuid>


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
		response, error = swtch.getBfdSessionParam(Name=name)

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
		response, error = swtch.getBfdSessionParamById(ObjectId=objectid)

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
		response, error = swtch.getAllBfdSessionParams()

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
		response, error = swtch.createBfdSessionParam(Name=name, AuthData=authdata, AuthKeyId=authkeyid, AuthType=authtype, DemandEnabled=demandenabled, DesiredMinTxInterval=desiredmintxinterval, RequiredMinEchoRxInterval=requiredminechorxinterval, AuthenticationEnabled=authenticationenabled, LocalMultiplier=localmultiplier, RequiredMinRxInterval=requiredminrxinterval)

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
		response, error = swtch.deleteBfdSessionParam(Name=name)

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
		response, error = swtch.deleteBfdSessionParamById(ObjectId=objectid

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
		response, error = swtch.updateBfdSessionParam(Name=name, AuthData=authdata, AuthKeyId=authkeyid, AuthType=authtype, DemandEnabled=demandenabled, DesiredMinTxInterval=desiredmintxinterval, RequiredMinEchoRxInterval=requiredminechorxinterval, AuthenticationEnabled=authenticationenabled, LocalMultiplier=localmultiplier, RequiredMinRxInterval=requiredminrxinterval)

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
		response, error = swtch.updateBfdSessionParamById(ObjectId=objectidAuthData=authdata, AuthKeyId=authkeyid, AuthType=authtype, DemandEnabled=demandenabled, DesiredMinTxInterval=desiredmintxinterval, RequiredMinEchoRxInterval=requiredminechorxinterval, AuthenticationEnabled=authenticationenabled, LocalMultiplier=localmultiplier, RequiredMinRxInterval=requiredminrxinterval)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
