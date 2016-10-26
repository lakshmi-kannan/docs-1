LaPortChannelState Object
=============================================================

*state/LaPortChannel*
------------------------------------

- Multiple objects of this type can exist in a system.

+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
|  **PARAMETER NAME**   | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| IntfRef **[KEY]**     | string        | Id of the lag group            | N/A         | N/A                            |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| LagType               | int32         | Sets the type of LAG           | N/A         | LACP(0), STATIC(1)             |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| MinLinks              | uint16        | Specifies the mininum number   | N/A         | N/A                            |
|                       |               | of member interfaces that must |             |                                |
|                       |               | be active for the aggregate    |             |                                |
|                       |               | interface to be available      |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfIndex               | int32         | the ifindex of the bonded      | N/A         | N/A                            |
|                       |               | interface                      |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| LacpMode              | int32         | ACTIVE is to initiate the      |           0 | ACTIVE(0), PASSIVE(1)          |
|                       |               | transmission of LACP packets.  |             |                                |
|                       |               | PASSIVE is to wait for peer to |             |                                |
|                       |               | initiate the transmission of   |             |                                |
|                       |               | LACP packets.                  |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| LagHash               | int32         | The tx hashing algorithm used  |           0 | LAYER2(0), LAYER3_4(2),        |
|                       |               | by the lag group               |             | LAYER2_3(1)                    |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| OperState             | string        | Operational status of the lag  | N/A         | N/A                            |
|                       |               | group.  If all ports are DOWN  |             |                                |
|                       |               | this will display DOWN.  If    |             |                                |
|                       |               | the group was admin disabled   |             |                                |
|                       |               | then will display DOWN.  No    |             |                                |
|                       |               | ports configured in group will |             |                                |
|                       |               | display DOWN                   |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| SystemIdMac           | string        | The MAC address portion of     | N/A         | N/A                            |
|                       |               | the nodes System ID. This      |             |                                |
|                       |               | is combined with the system    |             |                                |
|                       |               | priority to construct the      |             |                                |
|                       |               | 8-octet system-id              |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| SystemPriority        | uint16        | Sytem priority used by the     | N/A         | N/A                            |
|                       |               | node on this LAG interface.    |             |                                |
|                       |               | Lower value is higher priority |             |                                |
|                       |               | for determining which node is  |             |                                |
|                       |               | the controlling system.        |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminState            | string        | Convenient way to              | N/A         | N/A                            |
|                       |               | disable/enable a lag group.    |             |                                |
|                       |               | The behaviour should be such   |             |                                |
|                       |               | that all traffic should stop.  |             |                                |
|                       |               | LACP frames should continue to |             |                                |
|                       |               | be processed                   |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| Interval              | int32         | Set the period between         |           1 | SLOW(1), FAST(0)               |
|                       |               | LACP messages -- uses the      |             |                                |
|                       |               | lacp-period-type enumeration.  |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| IntfRefList           | string        | List of current member         | N/A         | N/A                            |
|                       |               | interfaces for the aggregate   |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+
| IntfRefListUpInBundle | string        | List of current member         | N/A         | N/A                            |
|                       |               | interfaces for the aggregate   |             |                                |
+-----------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/LaPortChannel
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/LaPortChannels?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/LaPortChannelState/<uuid>


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
		response, error = swtch.getLaPortChannelState(IntfRef=intfref)

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
		response, error = swtch.getLaPortChannelStateById(ObjectId=objectid)

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
		response, error = swtch.getAllLaPortChannelStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


