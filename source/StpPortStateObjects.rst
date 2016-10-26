StpPortState Object
=============================================================

*state/StpPort*
------------------------------------

- Multiple objects of this type can exist in a system.

+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
|     **PARAMETER NAME**      | **DATA TYPE** |        **DESCRIPTION**         | **DEFAULT** |        **VALID VALUES**        |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| IntfRef **[KEY]**           | string        | The port number of the port    | N/A         | N/A                            |
|                             |               | for which this entry contains  |             |                                |
|                             |               | Spanning Tree Protocol         |             |                                |
|                             |               | management information.        |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| Vlan **[KEY]**              | int32         | The value of instance of the   | N/A         | N/A                            |
|                             |               | vlan object                    |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| StpInPkts                   | uint64        | Number of STP PDUs received    | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TcInPkts                    | uint64        | Number of TC BPDUs received    | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BdmPrevState                | string        | BDM previous fsm state         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BpduGuardDetected           | int32         | Indicates whether a BPDU frame | N/A         | false(2), true(1)              |
|                             |               | was received on this STP port  |             |                                |
|                             |               | if the port  is and Edge Port  |             |                                |
|                             |               | and BPDU Guard is enabled      |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PrtmCurrState               | string        | PRTM current fsm state         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PstmPrevState               | string        | PSTM previous fsm state        | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BaWhile                     | int32         | Bridge Assurance timer 3 *     | N/A         | N/A                            |
|                             |               | Hello Timer                    |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BdmCurrState                | string        | BDM current fsm state          | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BridgeAssurance             | int32         | Used to make sure that a       | N/A         | false(2), true(1)              |
|                             |               | neighboring switch does        |             |                                |
|                             |               | not malfunction  and begin     |             |                                |
|                             |               | forwarding frames when it      |             |                                |
|                             |               | should not.  It does this by   |             |                                |
|                             |               | monitoring receipt of BPDUs    |             |                                |
|                             |               | on point-to-point links.       |             |                                |
|                             |               | When the  BPDUs stop being     |             |                                |
|                             |               | received the port is put into  |             |                                |
|                             |               | blocking state  (actually      |             |                                |
|                             |               | a port inconsistent state      |             |                                |
|                             |               | which stops forwarding).       |             |                                |
|                             |               |   When BPDUs restart the       |             |                                |
|                             |               | port resumes normal RSTP or    |             |                                |
|                             |               | MST modes.   This handles      |             |                                |
|                             |               | unidirectional links as well   |             |                                |
|                             |               | as the malfunction of a        |             |                                |
|                             |               | neighboring switch where STP   |             |                                |
|                             |               | stops sending BPDUs but the    |             |                                |
|                             |               | switch  continues to forward   |             |                                |
|                             |               | frames.                        |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PrtmPrevState               | string        | PRTM previous fsm state        | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| DesignatedBridge            | string        | The Bridge Identifier of       | N/A         | N/A                            |
|                             |               | the bridge that this port      |             |                                |
|                             |               | considers to be the Designated |             |                                |
|                             |               | Bridge for this port's         |             |                                |
|                             |               | segment.                       |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PpmPrevState                | string        | PPM previous fsm state         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| RcvdInfoWhile               | int32         | The Received Info timer. The   | N/A         | N/A                            |
|                             |               | time remaining before the      |             |                                |
|                             |               | spanning tree information      |             |                                |
|                             |               | received by this Port          |             |                                |
|                             |               | [portPriority (17.19.21)       |             |                                |
|                             |               | and portTimes (17.19.22)]      |             |                                |
|                             |               | is aged out if not refreshed   |             |                                |
|                             |               | by the receipt of a further    |             |                                |
|                             |               | Configuration Message.         |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TcWhile                     | int32         | The Topology Change timer. TCN | N/A         | N/A                            |
|                             |               | Messages are sent while this   |             |                                |
|                             |               | timer is running               |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminPathCost               | int32         | The administratively assigned  | N/A         | N/A                            |
|                             |               | value for the contribution     |             |                                |
|                             |               | of this port to the path cost  |             |                                |
|                             |               | of paths toward the spanning   |             |                                |
|                             |               | tree root.  Writing a value of |             |                                |
|                             |               | '0' assigns the automatically  |             |                                |
|                             |               | calculated default Path Cost   |             |                                |
|                             |               | value to the port.  If the     |             |                                |
|                             |               | default Path Cost is being     |             |                                |
|                             |               | used this object returns '0'   |             |                                |
|                             |               | when read.  This complements   |             |                                |
|                             |               | the object PathCost or         |             |                                |
|                             |               | PathCost32 which returns the   |             |                                |
|                             |               | operational value of the path  |             |                                |
|                             |               | cost.    The value of this     |             |                                |
|                             |               | object MUST be retained across |             |                                |
|                             |               | reinitializations of the       |             |                                |
|                             |               | management system.             |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| ForwardTransitions          | uint32        | The number of times this       | N/A         | N/A                            |
|                             |               | port has transitioned from     |             |                                |
|                             |               | the Learning state to the      |             |                                |
|                             |               | Forwarding state.              |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PimCurrState                | string        | PIM current fsm state          | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BridgeAssuranceInconsistant | int32         | When port stops receiving BPDU | N/A         | false(2), true(1)              |
|                             |               | on a Bridge Assurance enabled  |             |                                |
|                             |               | port then this will be set.    |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| Enable                      | int32         | The enabled/disabled status of |           1 | disabled(2), enabled(1)        |
|                             |               | the port.                      |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| FdWhile                     | int32         | The Forward Delay timer.       | N/A         | N/A                            |
|                             |               | Used to delay Port State       |             |                                |
|                             |               | transitions until other        |             |                                |
|                             |               | Bridges have received spanning |             |                                |
|                             |               | tree information               |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| MdelayWhile                 | int32         | The Migration Delay timer.     | N/A         | N/A                            |
|                             |               | Used by the Port Protocol      |             |                                |
|                             |               | Migration state machine to     |             |                                |
|                             |               | allow time for another RSTP    |             |                                |
|                             |               | Bridge on the same LAN to      |             |                                |
|                             |               | synchronize its migration      |             |                                |
|                             |               | state with this Port before    |             |                                |
|                             |               | the receipt of a BPDU can      |             |                                |
|                             |               | cause this Port to change      |             |                                |
|                             |               | the BPDU types it transmits.   |             |                                |
|                             |               | Initialized to MigrateTime     |             |                                |
|                             |               | (17.13.9).                     |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| Priority                    | int32         | The value of the priority      | N/A         | N/A                            |
|                             |               | field that is contained in the |             |                                |
|                             |               | first in network byte order    |             |                                |
|                             |               | octet of the 2 octet long      |             |                                |
|                             |               | Port ID.  The other octet of   |             |                                |
|                             |               | the Port ID is given by the    |             |                                |
|                             |               | value of StpPort. On bridges   |             |                                |
|                             |               | supporting IEEE 802.1t or IEEE |             |                                |
|                             |               | 802.1w permissible values are  |             |                                |
|                             |               | 0-240 in steps of 16.          |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| DesignatedPort              | string        | The Port Identifier of the     | N/A         | N/A                            |
|                             |               | port on the Designated Bridge  |             |                                |
|                             |               | for this port's segment.       |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| HelloWhen                   | int32         | The Hello timer. Used to       | N/A         | N/A                            |
|                             |               | ensure that at least one BPDU  |             |                                |
|                             |               | is transmitted by a Designated |             |                                |
|                             |               | Port in each HelloTime period. |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PathCost32                  | int32         | The contribution of this       | N/A         | N/A                            |
|                             |               | port to the path cost of       |             |                                |
|                             |               | paths towards the spanning     |             |                                |
|                             |               | tree root which include this   |             |                                |
|                             |               | port.  802.1D-1998 recommends  |             |                                |
|                             |               | that the default value of      |             |                                |
|                             |               | this parameter be in inverse   |             |                                |
|                             |               | proportion to the speed of     |             |                                |
|                             |               | the attached LAN.  This object |             |                                |
|                             |               | replaces PathCost to support   |             |                                |
|                             |               | IEEE 802.1t.                   |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TcAckOutPkts                | uint64        | Number of TC Ack BPDUs         | N/A         | N/A                            |
|                             |               | transmitted                    |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PrxmPrevState               | string        | PRXM previous fsm state        | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PtimPrevState               | string        | PTIM previous fsm state        | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| State                       | int32         | The port's current state as    | N/A         | listening(3), disabled(1),     |
|                             |               | defined by application of the  |             | broken(6), learning(4),        |
|                             |               | Spanning Tree Protocol.  This  |             | forwarding(5), blocking(2)     |
|                             |               | state controls what action     |             |                                |
|                             |               | a port takes on reception      |             |                                |
|                             |               | of a frame.  If the bridge     |             |                                |
|                             |               | has detected a port that is    |             |                                |
|                             |               | malfunctioning it will place   |             |                                |
|                             |               | that port into the broken(6)   |             |                                |
|                             |               | state.  For ports that are     |             |                                |
|                             |               | disabled (see Enable) this     |             |                                |
|                             |               | object will have a value of    |             |                                |
|                             |               | disabled(1).                   |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| AdminEdgePort               | int32         | The administrative value of    | N/A         | false(2), true(1)              |
|                             |               | the Edge Port parameter.  A    |             |                                |
|                             |               | value of true(1) indicates     |             |                                |
|                             |               | that this port should be       |             |                                |
|                             |               | assumed as an edge-port and    |             |                                |
|                             |               | a value of false(2) indicates  |             |                                |
|                             |               | that this port should be       |             |                                |
|                             |               | assumed as a non-edge-port.    |             |                                |
|                             |               |    Setting this object will    |             |                                |
|                             |               | also cause the corresponding   |             |                                |
|                             |               | instance of OperEdgePort to    |             |                                |
|                             |               | change to the same value.      |             |                                |
|                             |               |  Note that even when this      |             |                                |
|                             |               | object's value is true the     |             |                                |
|                             |               | value of the corresponding     |             |                                |
|                             |               | instance of OperEdgePort can   |             |                                |
|                             |               | be false if a BPDU has been    |             |                                |
|                             |               | received.  The value of this   |             |                                |
|                             |               | object MUST be retained across |             |                                |
|                             |               | reinitializations of the       |             |                                |
|                             |               | management system.             |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| MaxAge                      | int32         | The value that all bridges     | N/A         | N/A                            |
|                             |               | use for MaxAge as advertised   |             |                                |
|                             |               | by the root bridge.  Note      |             |                                |
|                             |               | that 802.1D-1998 specifies     |             |                                |
|                             |               | that the range for this        |             |                                |
|                             |               | parameter is related to the    |             |                                |
|                             |               | value of BridgeHelloTime.  The |             |                                |
|                             |               | granularity of this timer is   |             |                                |
|                             |               | specified by 802.1D-1998 to be |             |                                |
|                             |               | 1 second.  An agent may return |             |                                |
|                             |               | a badValue error if a set is   |             |                                |
|                             |               | attempted to a value that is   |             |                                |
|                             |               | not a whole number of seconds. |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PathCost                    | int32         | The contribution of this       | N/A         | N/A                            |
|                             |               | port to the path cost of       |             |                                |
|                             |               | paths towards the spanning     |             |                                |
|                             |               | tree root which include this   |             |                                |
|                             |               | port.  802.1D-1998 recommends  |             |                                |
|                             |               | that the default value of      |             |                                |
|                             |               | this parameter be in inverse   |             |                                |
|                             |               | proportion to    the speed     |             |                                |
|                             |               | of the attached LAN.  New      |             |                                |
|                             |               | implementations should support |             |                                |
|                             |               | PathCost32. If the port path   |             |                                |
|                             |               | costs exceeds the maximum      |             |                                |
|                             |               | value of this object then      |             |                                |
|                             |               | this object should report the  |             |                                |
|                             |               | maximum value namely 65535.    |             |                                |
|                             |               |  Applications should try to    |             |                                |
|                             |               | read the PathCost32 object     |             |                                |
|                             |               | if this object reports the     |             |                                |
|                             |               | maximum value.                 |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PrxmCurrState               | string        | PRXM current fsm state         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| HelloTime                   | int32         | The value that all bridges use | N/A         | N/A                            |
|                             |               | for HelloTime as advertised    |             |                                |
|                             |               | by the root bridge.  The       |             |                                |
|                             |               | granularity of this timer is   |             |                                |
|                             |               | specified by 802.1D-1998 to    |             |                                |
|                             |               | be 1 second.  An agent may     |             |                                |
|                             |               | return a badValue error if a   |             |                                |
|                             |               | set is attempted    to a value |             |                                |
|                             |               | that is not a whole number of  |             |                                |
|                             |               | seconds.                       |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TcmCurrState                | string        | TCM current fsm state          | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PtxmPrevState               | string        | PTXM previous fsm state        | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TcOutPkts                   | uint64        | Number of TC BPDUs transmitted | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TcmPrevState                | string        | TCM previous fsm state         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BpduGuardInterval           | int32         | The interval time to which     |          30 | N/A                            |
|                             |               | a port will try to recover     |             |                                |
|                             |               | from BPDU Guard err-disable    |             |                                |
|                             |               | state.  If no BPDU frames are  |             |                                |
|                             |               | detected after this timeout    |             |                                |
|                             |               | plus 3 Times Hello Time then   |             |                                |
|                             |               | the port will transition back  |             |                                |
|                             |               | to Up state.  If condition     |             |                                |
|                             |               | is cleared manually then this  |             |                                |
|                             |               | operation is ignored.  If set  |             |                                |
|                             |               | to zero then timer is inactive |             |                                |
|                             |               | and recovery is based on       |             |                                |
|                             |               | manual intervention.           |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| DesignatedRoot              | string        | The unique Bridge Identifier   | N/A         | N/A                            |
|                             |               | of the Bridge recorded as      |             |                                |
|                             |               | the Root in the Configuration  |             |                                |
|                             |               | BPDUs transmitted by the       |             |                                |
|                             |               | Designated Bridge for the      |             |                                |
|                             |               | segment to which the port is   |             |                                |
|                             |               | attached.                      |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| EdgeDelayWhile              | int32         | The Edge Delay timer. The      | N/A         | N/A                            |
|                             |               | time remaining in the absence  |             |                                |
|                             |               | of a received BPDU before      |             |                                |
|                             |               | this port is identified as an  |             |                                |
|                             |               | operEdgePort.                  |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PstmCurrState               | string        | PSTM current fsm state         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| OperPointToPoint            | int32         | The operational point-to-point | N/A         | false(2), true(1)              |
|                             |               | status of the LAN segment      |             |                                |
|                             |               | attached to this port.  It     |             |                                |
|                             |               | indicates whether a port       |             |                                |
|                             |               | is considered to have a        |             |                                |
|                             |               | point-to-point connection.     |             |                                |
|                             |               | If adminPointToPointMAC        |             |                                |
|                             |               | is set to auto(2) then the     |             |                                |
|                             |               | value of operPointToPointMAC   |             |                                |
|                             |               | is determined in accordance    |             |                                |
|                             |               | with the specific procedures   |             |                                |
|                             |               | defined for the MAC entity     |             |                                |
|                             |               | concerned as defined in IEEE   |             |                                |
|                             |               | 802.1w clause 6.5.  The value  |             |                                |
|                             |               | is determined dynamically;     |             |                                |
|                             |               | that is it is re-evaluated     |             |                                |
|                             |               | whenever the value of          |             |                                |
|                             |               | adminPointToPointMAC changes   |             |                                |
|                             |               | and whenever the specific      |             |                                |
|                             |               | procedures defined for the MAC |             |                                |
|                             |               | entity evaluate a change in    |             |                                |
|                             |               | its point-to-point status.     |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PvstInPkts                  | uint64        | Number of PVST BPDUs received  | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BpduGuard                   | int32         | Used in conjuction with        | N/A         | false(2), true(1)              |
|                             |               | AdminEdge to shutdown a port   |             |                                |
|                             |               | when a BPDU is received.       |             |                                |
|                             |               | Protects against loops in the  |             |                                |
|                             |               | network                        |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BpduOutPkts                 | uint64        | Number of BPDUs transmitted    | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PvstOutPkts                 | uint64        | Number of PVST BPDUs           | N/A         | N/A                            |
|                             |               | transmitted                    |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| StpOutPkts                  | uint64        | Number of STP BPDUs            | N/A         | N/A                            |
|                             |               | transmitted                    |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| OperEdgePort                | int32         | The operational value of the   | N/A         | false(2), true(1)              |
|                             |               | Edge Port parameter.  The      |             |                                |
|                             |               | object is initialized to the   |             |                                |
|                             |               | value of the corresponding     |             |                                |
|                             |               | instance of AdminEdgePort.     |             |                                |
|                             |               |  When the corresponding        |             |                                |
|                             |               | instance of AdminEdgePort      |             |                                |
|                             |               | is set this object will be     |             |                                |
|                             |               | changed as well.  This object  |             |                                |
|                             |               | will also be changed to false  |             |                                |
|                             |               | on reception of a BPDU.        |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PimPrevState                | string        | PIM previous fsm state         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| RrWhile                     | int32         | The Recent Root timer.         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PtimCurrState               | string        | PTIM current fsm state         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PtxmCurrState               | string        | PTXM current fsm state         | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| RstpOutPkts                 | uint64        | Number of RSTP BPDUs           | N/A         | N/A                            |
|                             |               | transmitted                    |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| TcAckInPkts                 | uint64        | Number of TC Ack BPDUs         | N/A         | N/A                            |
|                             |               | received                       |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| BpduInPkts                  | uint64        | Number of BPDUs received       | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| DesignatedCost              | int32         | The path cost of the           | N/A         | N/A                            |
|                             |               | Designated Port of the segment |             |                                |
|                             |               | connected to this port.  This  |             |                                |
|                             |               | value is compared to the Root  |             |                                |
|                             |               | Path Cost field in received    |             |                                |
|                             |               | bridge PDUs.                   |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| ForwardDelay                | int32         | The value that all bridges use | N/A         | N/A                            |
|                             |               | for ForwardDelay as advertised |             |                                |
|                             |               | by the root bridge.  Note that |             |                                |
|                             |               | 802.1D-1998 specifies that     |             |                                |
|                             |               | the range for this parameter   |             |                                |
|                             |               | is related to the value of     |             |                                |
|                             |               | dot1dStpBridgeMaxAge.  The     |             |                                |
|                             |               | granularity of this timer is   |             |                                |
|                             |               | specified by 802.1D-1998 to be |             |                                |
|                             |               | 1 second.  An agent may return |             |                                |
|                             |               | a badValue error if a set is   |             |                                |
|                             |               | attempted to a value that is   |             |                                |
|                             |               | not a whole number of seconds. |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| PpmCurrState                | string        | PPM current fsm state          | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| RbWhile                     | int32         | The Recent Backup timer.       | N/A         | N/A                            |
|                             |               | Maintained at its initial      |             |                                |
|                             |               | value twice HelloTime while    |             |                                |
|                             |               | the Port is a Backup Port.     |             |                                |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+
| RstpInPkts                  | uint64        | Number of RSTP BPDUs received  | N/A         | N/A                            |
+-----------------------------+---------------+--------------------------------+-------------+--------------------------------+



*FlexSwitch CURL API Supported*
------------------------------------

	- GET By Key
		 curl -X GET -H 'Content-Type: application/json' --header 'Accept: application/json' -d '{<Model Object as json-Data>}' http://device-management-IP:8080/public/v1/state/StpPort
	- GET ALL
		 curl -X GET http://device-management-IP:8080/public/v1/state/StpPorts?CurrentMarker=<x>&Count=<y>
	- GET By ID
		 curl -X GET http://device-management-IP:8080/public/v1/config/StpPortState/<uuid>


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
		response, error = swtch.getStpPortState(IntfRef=intfref, Vlan=vlan)

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
		response, error = swtch.getStpPortStateById(ObjectId=objectid)

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
		response, error = swtch.getAllStpPortStates()

		if error != None: #Error not being None implies there is some problem
			print error
		else :
			print 'Success'


