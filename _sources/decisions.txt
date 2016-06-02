.. FlexSwitch documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Design decisions
================


Declarative v/s Imperative
^^^^^^^^^^^^^^^^^^^^^^^^^^

Declarative Model 
"""""""""""""""""

Declarative model is paradigm where the user declares what needs to be done on an entity without concern for the control flow. 

It is up to the entity to digest and perform internal computation to reach the desired end state.   
In the networking industry this is akin to giving a monolithic configuration file to a network device and letting
the device reach the desired configuration on its own.  Cisco's ACI, OPFlex  are examples that follow this path.  
The result of this approach is a single view of the world for how a configuration is applied.  

Imperative Model 
"""""""""""""""""

Imperative model assumes more classical programming approach. In this model the user specifies the control flow and 
explicit steps. This is typically done by providing raw APIs to the end user and allowing them program the device to 
their needs.   This is not to say that order dependencies do not exist, but it is up to the user to determine the way to apply state to a device.   In the networking industry this akin to OpenFlow.  The result of this approach allows for multiple flows for how to apply configuration, without have a single view.

Winner?

Both Declarative and Imperative models have their place in the networking industry.
However pushing declarative programming all the way to the protocol daemons/smallest of components of the software is 
counterproductive.  This results in a single view of the world for setting up equipment, that will vary from vendor to
vendor. With the imperative model the burden of applying configuration is placed on the network operator and may not 
be desirable. Functionality, simplicity and ease of use are the requirements of many network operators.

FlexSwitch approach  
"""""""""""""""""""
We provide the both an imperative model which gives the operator the flexibility to utilize our system in any 
environment and the best way they see fit.  While we supply Restful APIs to imperatively program FlexSwitch for 
enhanced flexibility,  we also have applications that perform declarative interactions between the user desired configuration
and our APIs. We believe that choice and control of model should be in the hands of the customer, rather than 
a one-size fits all approach. This allows for FlexSwitch to be utilized in any environment irrespective of model or approach.  

DB vs. RPC
^^^^^^^^^^

DB method
"""""""""

DB notification based method of communicating among various modules is a popular approach to build network OS. This
approach makes it possible to mix multiple software components from different vendors and make a solution. 
It would also eliminate any possible spaghetti dependencies. However this approach would introduce a one central 
component that might become a single point of failure. 

RPC method 
""""""""""
RPC method is efficient in terms of performance. Micro service architectures are possible with RPC. 
However it is possible to introduce cyclic/complex dependencies among the components. 

FlexSwitch approach  
"""""""""""""""""""
FlexSwitch architecture is a mixture of both approaches. We chose to use RPCs from clients to servers. 
For instance config daemon acts as a client for all the daemons and it talks to the daemons underneath it. 
However it the underlying daemons would never initiate or use any API from config daemon/upper layers. So all RPCs are 
only top-down. We use notifications for the underlying components to communicate to their consumers. For instance 
ASICd would notify all the port up/down events. 

In addition to these rules we also ensure no lateral communication happens using RPC. For instance BGP would never 
communicate with OSPF. Similarly none of the L3 protocol components would talk to L2 protocol daemons.
