FlexSwitch Config Models
========================
FlexSwitch configuration APIs are defined as model objects. Code generation tools take the model as input and produce code that ConfigMgr invokes to send configuration to back-end servers and store in DB.
A model object can be configuration, state or action type. Few objects can be both configuration and state types.

Create, Update, and Delete operations can be performed on configuration objects. These APIs send configurations to back-end server for proessing and stores in DB for persistency.
Get operation can be performed on state objects. These APIs request state object(s) from back-end server and responds back.
Exec operation can be performed on action objects. These APIs are send a command to back-end server to perform a certain action, such as clean stats on port, etc.

Model objects can be defined as go struct or in yang file. This document describes how to define a model object in go struct.
There are various tags used to identify nature of the object or field in the object.

ACCESS: "w"          ---- Object type - "w" means config, "r" means state and "x" means action
MULTIPLICITY: "*"    ---- How many instances of this object can exist. "*" means multiple and "1" means singleton
ACCELERATED: "true"  ---- If the object can be configured in asynchronous mode.
USESTATEDB: "true"   ---- if true then this state object is stored in DB.
AUTOCREATE: "true"   ---- If true then this object will be automatically created with default values when FlexSwitch come up.
SNAPROUTE: "KEY"     ---- Identifies if this field is a key in this object. There can be more than one keys.
DESCRIPTION: "<str>" ---- Description of the field.
DEFAULT: <"value>"   ---- Default value of this field.
LEN: "<length>"      ---- If the field is of type string then length of the string allowed.
SELCTION: "<a>/<b>"  ---- List of possible values allowed for this field.
MIN: "<value>"       ---- If the field is of type integer then minimum value allowed.
MAX: "<value>"       ---- If the field is of type integer then maximum value allowed.
RANGE: "<a>-<b>"     ---- If the field is of type integer then range of values allowed in the range.


Examples
--------

::

 /*
  * BFD Session config
  */
 type BfdSession struct {
         baseObj
         IpAddr    string `SNAPROUTE: "KEY", ACCESS:"w",  MULTIPLICITY:"*", DESCRIPTION: "BFD neigh    bor IP address"`
         ParamName string `DESCRIPTION: "Name of the session parameters object to be applied on thi    s session", DEFAULT: "default"`
         Interface string `DESCRIPTION: "Name of the interface this session has to be established o    n", DEFAULT: "None"`
         PerLink   bool   `DESCRIPTION: "Run BFD sessions on individual link of a LAG if the neighb    or is reachable through LAG", DEFAULT: "false"`
         Owner     string `DESCRIPTION: "Module requesting BFD session configuration", DEFAULT: "us    er"`
 }
 
 /*
  * BFD Session state
  */
 type BfdSessionState struct {
         baseObj
         IpAddr                    string `SNAPROUTE: "KEY", ACCESS:"r",  MULTIPLICITY:"*",DESCRIPT    ION: "Neighbor IP address"`
         SessionId                 int32  `DESCRIPTION: "Session index"`
         ParamName                 string `DESCRIPTION: "Session parameters config"`
         IfIndex                   int32  `DESCRIPTION: "Interface index"`
         InterfaceSpecific         bool   `DESCRIPTION: "This session is tied to an interface"`
         IfName                    string `DESCRIPTION: "Interface to which this session is establi    shed on"`
         PerLinkSession            bool   `DESCRIPTION: "This is a perlink session on LAG"`
         LocalMacAddr              string `DESCRIPTION: "My MAC address"`
         RemoteMacAddr             string `DESCRIPTION: "Neighbor MAC address"`
         RegisteredProtocols       string `DESCRIPTION: "Registered owners"`
         SessionState              string `DESCRIPTION: "My state"`
         RemoteSessionState        string `DESCRIPTION: "Neighbor state"`
         LocalDiscriminator        uint32 `DESCRIPTION: "My discriminator"`
         RemoteDiscriminator       uint32 `DESCRIPTION: "Neighbor discriminator"`
         LocalDiagType             string `DESCRIPTION: "My diagnostic"`
         DesiredMinTxInterval      string `DESCRIPTION: "My desired minimum tx interval"`
         RequiredMinRxInterval     string `DESCRIPTION: "My required minimum rx interval"`
         RemoteMinRxInterval       string `DESCRIPTION: "Neighbor minimum rx interval"`
         DetectionMultiplier       uint32 `DESCRIPTION: "My detection multiplier"`
         RemoteDetectionMultiplier uint32 `DESCRIPTION: "Neighbor detection multiplier"`
         DemandMode                bool   `DESCRIPTION: "My demand mode"`
         RemoteDemandMode          bool   `DESCRIPTION: "Neighbor demand mode"`
         AuthSeqKnown              bool   `DESCRIPTION: "Authentication sequence known"`
         AuthType                  string `DESCRIPTION: "My Authentication type"`
         ReceivedAuthSeq           uint32 `DESCRIPTION: "Received authentication sequence number"`
         SentAuthSeq               uint32 `DESCRIPTION: "Sent authentication sequence number"`
         NumTxPackets              uint32 `DESCRIPTION: "Number of control packets sent"`
         NumRxPackets              uint32 `DESCRIPTION: "Number of control packets received"`
 }

 /*
  * ARP clear action
  */
 type ArpDeleteByIPv4Addr struct {
         baseObj
         IpAddr string `SNAPROUTE: "KEY", ACCESS:"x", MULTIPLICITY:"1", DESCRIPTION: "End Host IP A    ddress for which corresponding Arp entry needed to be deleted"`
 }

