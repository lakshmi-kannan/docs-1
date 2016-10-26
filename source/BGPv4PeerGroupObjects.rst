BGPv4PeerGroup Object
=============================================================

*config/BGPv4PeerGroup*
------------------------------------

- Multiple objects of this type can exist in a system.

+-------------------------+---------------+--------------------------------+-------------+------------------+
|   **PARAMETER NAME**    | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| Name **[KEY]**          | string        | Name of the BGP peer group     | N/A         | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| HoldTime                | uint32        | Hold time for the BGP neighbor |           0 | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| PeerAS                  | string        | Peer AS of the BGP neighbor    |             | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| UpdateSource            | string        | Source IP to connect to the    |             | N/A              |
|                         |               | BGP neighbor                   |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| AddPathsRx              | bool          | Receive additional paths from  | false       | N/A              |
|                         |               | BGP neighbor                   |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| Description             | string        | Description of the BGP         |             | N/A              |
|                         |               | neighbor                       |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| LocalAS                 | string        | Local AS of the BGP neighbor   |             | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixes             | uint32        | Maximum number of prefixes     |           0 | N/A              |
|                         |               | that can be received from the  |             |                  |
|                         |               | BGP neighbor                   |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixesRestartTimer | uint8         | Time to wait before we start   |           0 | N/A              |
|                         |               | BGP peer session when we       |             |                  |
|                         |               | receive max prefixes           |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| AddPathsMaxTx           | uint8         | Max number of additional paths |           0 | N/A              |
|                         |               | that can be transmitted to BGP |             |                  |
|                         |               | neighbor                       |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| AuthPassword            | string        | Password to connect to the BGP |             | N/A              |
|                         |               | neighbor                       |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixesDisconnect   | bool          | Disconnect the BGP peer        | false       | N/A              |
|                         |               | session when we receive the    |             |                  |
|                         |               | max prefixes from the neighbor |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| NextHopSelf             | bool          | Use neighbor source IP as the  | false       | N/A              |
|                         |               | next hop for IBGP neighbors    |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| RouteReflectorClient    | bool          | Set/Clear BGP neighbor as a    | false       | N/A              |
|                         |               | route reflector client         |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| AdjRIBInFilter          | string        | Policy that is applied for     |             | N/A              |
|                         |               | Adj-RIB-In prefix filtering    |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| KeepaliveTime           | uint32        | Keep alive time for the BGP    |           0 | N/A              |
|                         |               | neighbor                       |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixesThresholdPct | uint8         | The percentage of maximum      |          80 | N/A              |
|                         |               | prefixes before we start       |             |                  |
|                         |               | logging                        |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| MultiHopEnable          | bool          | Enable/Disable multi hop for   | false       | N/A              |
|                         |               | BGP neighbor                   |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| MultiHopTTL             | uint8         | TTL for multi hop BGP neighbor |           0 | N/A              |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| RouteReflectorClusterId | uint32        | Cluster Id of the internal     |           0 | N/A              |
|                         |               | BGP neighbor route reflector   |             |                  |
|                         |               | client                         |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| AdjRIBOutFilter         | string        | Policy that is applied for     |             | N/A              |
|                         |               | Adj-RIB-Out prefix filtering   |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+
| ConnectRetryTime        | uint32        | Connect retry time to          |           0 | N/A              |
|                         |               | connect to BGP neighbor after  |             |                  |
|                         |               | disconnect                     |             |                  |
+-------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/BGPv4PeerGroup
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BGPv4PeerGroup/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/BGPv4PeerGroups?CurrentMarker=<x>&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/BGPv4PeerGroup
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/BGPv4PeerGroup
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/BGPv4PeerGroup<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/BGPv4PeerGroup
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/BGPv4PeerGroup<uuid>


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
		response, error = swtch.getBGPv4PeerGroup(Name=name)

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
		response, error = swtch.getBGPv4PeerGroupById(ObjectId=objectid)

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
		response, error = swtch.getAllBGPv4PeerGroups()

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
		response, error = swtch.createBGPv4PeerGroup(Name=name, HoldTime=holdtime, PeerAS=peeras, UpdateSource=updatesource, AddPathsRx=addpathsrx, Description=description, LocalAS=localas, MaxPrefixes=maxprefixes, MaxPrefixesRestartTimer=maxprefixesrestarttimer, AddPathsMaxTx=addpathsmaxtx, AuthPassword=authpassword, MaxPrefixesDisconnect=maxprefixesdisconnect, NextHopSelf=nexthopself, RouteReflectorClient=routereflectorclient, AdjRIBInFilter=adjribinfilter, KeepaliveTime=keepalivetime, MaxPrefixesThresholdPct=maxprefixesthresholdpct, MultiHopEnable=multihopenable, MultiHopTTL=multihopttl, RouteReflectorClusterId=routereflectorclusterid, AdjRIBOutFilter=adjriboutfilter, ConnectRetryTime=connectretrytime)

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
		response, error = swtch.deleteBGPv4PeerGroup(Name=name)

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
		response, error = swtch.deleteBGPv4PeerGroupById(ObjectId=objectid

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
		response, error = swtch.updateBGPv4PeerGroup(Name=name, HoldTime=holdtime, PeerAS=peeras, UpdateSource=updatesource, AddPathsRx=addpathsrx, Description=description, LocalAS=localas, MaxPrefixes=maxprefixes, MaxPrefixesRestartTimer=maxprefixesrestarttimer, AddPathsMaxTx=addpathsmaxtx, AuthPassword=authpassword, MaxPrefixesDisconnect=maxprefixesdisconnect, NextHopSelf=nexthopself, RouteReflectorClient=routereflectorclient, AdjRIBInFilter=adjribinfilter, KeepaliveTime=keepalivetime, MaxPrefixesThresholdPct=maxprefixesthresholdpct, MultiHopEnable=multihopenable, MultiHopTTL=multihopttl, RouteReflectorClusterId=routereflectorclusterid, AdjRIBOutFilter=adjriboutfilter, ConnectRetryTime=connectretrytime)

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
		response, error = swtch.updateBGPv4PeerGroupById(ObjectId=objectidHoldTime=holdtime, PeerAS=peeras, UpdateSource=updatesource, AddPathsRx=addpathsrx, Description=description, LocalAS=localas, MaxPrefixes=maxprefixes, MaxPrefixesRestartTimer=maxprefixesrestarttimer, AddPathsMaxTx=addpathsmaxtx, AuthPassword=authpassword, MaxPrefixesDisconnect=maxprefixesdisconnect, NextHopSelf=nexthopself, RouteReflectorClient=routereflectorclient, AdjRIBInFilter=adjribinfilter, KeepaliveTime=keepalivetime, MaxPrefixesThresholdPct=maxprefixesthresholdpct, MultiHopEnable=multihopenable, MultiHopTTL=multihopttl, RouteReflectorClusterId=routereflectorclusterid, AdjRIBOutFilter=adjriboutfilter, ConnectRetryTime=connectretrytime)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
