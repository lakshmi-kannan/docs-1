BGPv4Neighbor Object
=============================================================

*config/BGPv4Neighbor*
------------------------------------

- Multiple objects of this type can exist in a system.

+---------------------------+---------------+--------------------------------+-------------+------------------+
|    **PARAMETER NAME**     | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** | **VALID VALUES** |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| IntfRef **[KEY]**         | string        | Interface of the BGP neighbor  | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| NeighborAddress **[KEY]** | string        | Address of the BGP neighbor    | N/A         | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MultiHopEnable            | bool          | Enable/Disable multi hop for   | false       | N/A              |
|                           |               | BGP neighbor                   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AddPathsMaxTx             | uint8         | Max number of additional paths |           0 | N/A              |
|                           |               | that can be transmitted to BGP |             |                  |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AdjRIBInFilter            | string        | Policy that is applied for     |             | N/A              |
|                           |               | Adj-RIB-In prefix filtering    |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixes               | uint32        | Maximum number of prefixes     |           0 | N/A              |
|                           |               | that can be received from the  |             |                  |
|                           |               | BGP neighbor                   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RouteReflectorClient      | bool          | Set/Clear BGP neighbor as a    | false       | N/A              |
|                           |               | route reflector client         |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AdjRIBOutFilter           | string        | Policy that is applied for     |             | N/A              |
|                           |               | Adj-RIB-Out prefix filtering   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| BfdSessionParam           | string        | Bfd session param name to be   | default     | N/A              |
|                           |               | applied                        |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AddPathsRx                | bool          | Receive additional paths from  | false       | N/A              |
|                           |               | BGP neighbor                   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| Disabled                  | bool          | Enable/Disable the BGP         | false       | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| Description               | string        | Description of the BGP         |             | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixesRestartTimer   | uint8         | Time in seconds to wait before |           0 | N/A              |
|                           |               | we start BGP peer session when |             |                  |
|                           |               | we receive max prefixes        |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MultiHopTTL               | uint8         | TTL for multi hop BGP neighbor |           0 | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| PeerGroup                 | string        | Peer group of the BGP neighbor |             | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixesDisconnect     | bool          | Disconnect the BGP peer        | false       | N/A              |
|                           |               | session when we receive the    |             |                  |
|                           |               | max prefixes from the neighbor |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| RouteReflectorClusterId   | uint32        | Cluster Id of the internal     |           0 | N/A              |
|                           |               | BGP neighbor route reflector   |             |                  |
|                           |               | client                         |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| BfdEnable                 | bool          | Enable/Disable BFD for the BGP | false       | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| NextHopSelf               | bool          | Use neighbor source IP as the  | false       | N/A              |
|                           |               | next hop for IBGP neighbors    |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| LocalAS                   | string        | Local AS of the BGP neighbor   |             | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| MaxPrefixesThresholdPct   | uint8         | The percentage of maximum      |          80 | N/A              |
|                           |               | prefixes before we start       |             |                  |
|                           |               | logging                        |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| PeerAS                    | string        | Peer AS of the BGP neighbor    |             | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| UpdateSource              | string        | Source IP to connect to the    |             | N/A              |
|                           |               | BGP neighbor                   |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| AuthPassword              | string        | Password to connect to the BGP |             | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| ConnectRetryTime          | uint32        | Connect retry time to          |           0 | N/A              |
|                           |               | connect to BGP neighbor after  |             |                  |
|                           |               | disconnect                     |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| HoldTime                  | uint32        | Hold time for the BGP neighbor |           0 | N/A              |
+---------------------------+---------------+--------------------------------+-------------+------------------+
| KeepaliveTime             | uint32        | Keep alive time for the BGP    |           0 | N/A              |
|                           |               | neighbor                       |             |                  |
+---------------------------+---------------+--------------------------------+-------------+------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/BGPv4Neighbor
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/BGPv4Neighbor/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/BGPv4Neighbors?CurrentMarker=<x>&Count=<y>
	- CREATE(POST)
		 curl -X POST -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/BGPv4Neighbor
	- DELETE By Key
		 curl -X DELETE -i -H 'Accept:application/json' -d '{<Model Object as json data>}' http://device-management-IP:8080/public/v1/config/BGPv4Neighbor
	- DELETE By ID
		 curl -X DELETE http://device-management-IP:8080/public/v1/config/BGPv4Neighbor<uuid>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/BGPv4Neighbor
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/BGPv4Neighbor<uuid>


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
		response, error = swtch.getBGPv4Neighbor(IntfRef=intfref, NeighborAddress=neighboraddress)

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
		response, error = swtch.getBGPv4NeighborById(ObjectId=objectid)

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
		response, error = swtch.getAllBGPv4Neighbors()

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
		response, error = swtch.createBGPv4Neighbor(IntfRef=intfref, NeighborAddress=neighboraddress, MultiHopEnable=multihopenable, AddPathsMaxTx=addpathsmaxtx, AdjRIBInFilter=adjribinfilter, MaxPrefixes=maxprefixes, RouteReflectorClient=routereflectorclient, AdjRIBOutFilter=adjriboutfilter, BfdSessionParam=bfdsessionparam, AddPathsRx=addpathsrx, Disabled=disabled, Description=description, MaxPrefixesRestartTimer=maxprefixesrestarttimer, MultiHopTTL=multihopttl, PeerGroup=peergroup, MaxPrefixesDisconnect=maxprefixesdisconnect, RouteReflectorClusterId=routereflectorclusterid, BfdEnable=bfdenable, NextHopSelf=nexthopself, LocalAS=localas, MaxPrefixesThresholdPct=maxprefixesthresholdpct, PeerAS=peeras, UpdateSource=updatesource, AuthPassword=authpassword, ConnectRetryTime=connectretrytime, HoldTime=holdtime, KeepaliveTime=keepalivetime)

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
		response, error = swtch.deleteBGPv4Neighbor(IntfRef=intfref, NeighborAddress=neighboraddress)

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
		response, error = swtch.deleteBGPv4NeighborById(ObjectId=objectid

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
		response, error = swtch.updateBGPv4Neighbor(IntfRef=intfref, NeighborAddress=neighboraddress, MultiHopEnable=multihopenable, AddPathsMaxTx=addpathsmaxtx, AdjRIBInFilter=adjribinfilter, MaxPrefixes=maxprefixes, RouteReflectorClient=routereflectorclient, AdjRIBOutFilter=adjriboutfilter, BfdSessionParam=bfdsessionparam, AddPathsRx=addpathsrx, Disabled=disabled, Description=description, MaxPrefixesRestartTimer=maxprefixesrestarttimer, MultiHopTTL=multihopttl, PeerGroup=peergroup, MaxPrefixesDisconnect=maxprefixesdisconnect, RouteReflectorClusterId=routereflectorclusterid, BfdEnable=bfdenable, NextHopSelf=nexthopself, LocalAS=localas, MaxPrefixesThresholdPct=maxprefixesthresholdpct, PeerAS=peeras, UpdateSource=updatesource, AuthPassword=authpassword, ConnectRetryTime=connectretrytime, HoldTime=holdtime, KeepaliveTime=keepalivetime)

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
		response, error = swtch.updateBGPv4NeighborById(ObjectId=objectidMultiHopEnable=multihopenable, AddPathsMaxTx=addpathsmaxtx, AdjRIBInFilter=adjribinfilter, MaxPrefixes=maxprefixes, RouteReflectorClient=routereflectorclient, AdjRIBOutFilter=adjriboutfilter, BfdSessionParam=bfdsessionparam, AddPathsRx=addpathsrx, Disabled=disabled, Description=description, MaxPrefixesRestartTimer=maxprefixesrestarttimer, MultiHopTTL=multihopttl, PeerGroup=peergroup, MaxPrefixesDisconnect=maxprefixesdisconnect, RouteReflectorClusterId=routereflectorclusterid, BfdEnable=bfdenable, NextHopSelf=nexthopself, LocalAS=localas, MaxPrefixesThresholdPct=maxprefixesthresholdpct, PeerAS=peeras, UpdateSource=updatesource, AuthPassword=authpassword, ConnectRetryTime=connectretrytime, HoldTime=holdtime, KeepaliveTime=keepalivetime)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
