Port Object
=============================================================

*config/Port*
------------------------------------

- Multiple objects of this type can exist in a system.

+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| **PARAMETER NAME** | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| IntfRef **[KEY]**  | string        | Front panel port name or       | N/A         | N/A                            |
|                    |               | system assigned interface id   |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| Autoneg            | string        | Autonegotiation setting for    | OFF         | ON, OFF                        |
|                    |               | this port                      |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| BreakOutMode       | string        | Break out mode for the port.   | N/A         | 1x40(1), 4x10(2)               |
|                    |               | Only applicable on ports that  |             |                                |
|                    |               | support breakout. Valid modes  |             |                                |
|                    |               | - 1x40                         |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| IfIndex            | int32         | System assigned interface      | N/A         | N/A                            |
|                    |               | id for this port. Read only    |             |                                |
|                    |               | attribute                      |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| LoopbackMode       | string        | Desired loopback setting for   | NONE        | NONE, MAC, PHY, RMT            |
|                    |               | this port                      |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| MediaType          | string        | Type of media inserted into    | N/A         | N/A                            |
|                    |               | this port                      |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminState         | string        | Administrative state of this   | DOWN        | UP, DOWN                       |
|                    |               | port                           |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| MacAddr            | string        | Mac address associated with    | N/A         | N/A                            |
|                    |               | this port                      |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| PhyIntfType        | string        | Type of internal phy interface | N/A         | GMII, SGMII, QSMII, SFI, XFI,  |
|                    |               |                                |             | XAUI, XLAUI, RXAUI, CR, CR2,   |
|                    |               |                                |             | CR4, KR, KR2, KR4, SR, SR2,    |
|                    |               |                                |             | SR4, SR10, LR, LR4             |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| PRBSTxEnable       | bool          | Enable/Disable generation of   | false       | N/A                            |
|                    |               | PRBS on this port              |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| Duplex             | string        | Duplex setting for this port   | Full Duplex | Half Duplex, Full Duplex       |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| Mtu                | int32         | Maximum transmission unit size | N/A         | N/A                            |
|                    |               | for this port                  |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| PRBSPolynomial     | string        | PRBS polynomial to use for     | 2^7         | 2^7, 2^23, 2^31                |
|                    |               | generation/checking            |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| PRBSRxEnable       | bool          | Enable/Disable PRBS checker on | false       | N/A                            |
|                    |               | this port                      |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| Description        | string        | User provided string           | FP Port     | N/A                            |
|                    |               | description                    |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| EnableFEC          | bool          | Enable/Disable 802.3bj FEC on  | false       | N/A                            |
|                    |               | this interface                 |             |                                |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+
| Speed              | int32         | Port speed in Mbps             | N/A         | N/A                            |
+--------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/config/Port
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/Port/<uuid>
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/config/Ports?CurrentMarker=<x>\\&Count=<y>
	- UPDATE(PATCH) By Key
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/Port
	- UPDATE(PATCH) By ID
		 curl -X PATCH -H 'Content-Type: application/json' -d '{<Model Object as json data>}'  http://device-management-IP:8080/public/v1/config/Port<uuid>


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
		response, error = swtch.getPort(IntfRef=intfref)

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
		response, error = swtch.getPortById(ObjectId=objectid)

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
		response, error = swtch.getAllPorts()

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
		response, error = swtch.updatePort(IntfRef=intfref, Autoneg=autoneg, BreakOutMode=breakoutmode, IfIndex=ifindex, LoopbackMode=loopbackmode, MediaType=mediatype, AdminState=adminstate, MacAddr=macaddr, PhyIntfType=phyintftype, PRBSTxEnable=prbstxenable, Duplex=duplex, Mtu=mtu, PRBSPolynomial=prbspolynomial, PRBSRxEnable=prbsrxenable, Description=description, EnableFEC=enablefec, Speed=speed)

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
		response, error = swtch.updatePortById(ObjectId=objectidAutoneg=autoneg, BreakOutMode=breakoutmode, IfIndex=ifindex, LoopbackMode=loopbackmode, MediaType=mediatype, AdminState=adminstate, MacAddr=macaddr, PhyIntfType=phyintftype, PRBSTxEnable=prbstxenable, Duplex=duplex, Mtu=mtu, PRBSPolynomial=prbspolynomial, PRBSRxEnable=prbsrxenable, Description=description, EnableFEC=enablefec, Speed=speed)

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'
