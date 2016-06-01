.. FlexSwitchSDK documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Open Source Components
======================


System Components
^^^^^^^^^^^^^^^^^

GoLang
""""""

Golang has become the modern programming language for systems and infrastructure programming.  Benefits of using GoLang:

	- **Statically typed and Compiled** - All the type safety issues are caught during compile time, unlike at run time like Python, Java Script
	- **Built In Garbage Collection**  - Programmer does not have to manage memory for allocation and frees. This eliminates many system crashes that are way too familiar for systems programmers.
	- **Built In  concurrency** - Golang's concurrency patterns are very powerful and easy to use. 
	- **Built in multi core support** - Golang's concurrency patterns are very powerful and easy to use.
 
FlexSwitch utilizes golang as the base language for all our development. This brings agility into our development and also quality into our software

Python
""""""

RPC tools
"""""""""

Most modern software needs to interact with other software modules in some fashion.  Using RPC is one of very well known mechanisms to achieve this
Thanks to the opensource community. There are a few comprehensive solutions available 

Thrift RPC
++++++++++

Apache Thrift has been very stable and scalable solution for Inter Process Communication (IPC)/Remote Procedure Calls (RPC)

	- **Cross language, Multi language support** - Thrift supports multiple languages( golang, python, C** etc). Clients and servers can be developed in  different languages.  
	- **Simple Interface Definition Language** - IDL defined by Thrift is very simple to use. 
	- **Compiler to generate Client and Server** - Thrift compiler generates client and server in various languages.
	- **Best performance among other choices** - Thrift offers better performance than other RPC tools including gRPC, Protobuf3

FlexSwitch utilizes Thrift for internal communication among our daemons. Thrift RPC is used only from top to down (i.e.) clients to servers.
FlexSwitch ensures not to use RPC from a server to client allowing daemons to remain agnostic of their clients thus eliminating spaghetti dependencies. 


Pub/Sub Mechanisms 
""""""""""""""""""

FlexSwitch software uses non-persistent pub/sub mechanism for notifying its internal components. We need a lightweight and efficient Pub/sub mechanism 

Nano Message
++++++++++++
    
Nano-Message offers clean posix compliant APIs. Performance numbers against Nano Message are much better than its counterparts like ZeroMQ, D-Bus etc
We use Nano Message library in ASICd to notify other protocol daemons about possible events like interface creation, deletion link up/down

Linux
"""""

FlexSwitch software runs on linux in userspace, keeping with the portability and flexibility mantra engrained into our code. 
Due to stability, security and wide spread adoption, Linux has become the defacto standard for all the networking equipment. 


Configuration and State Database
""""""""""""""""""""""""""""""""
FlexSwitch software stores its configuration and state in database to facilitate restoring configuration after restart and to make it easy for the customer applications to read the state of the system. We needed a database that is very efficient. 

Redis
+++++
   
Redis was written in ANSI C and very scaleable database. It also several other features.

	- **In-Memory database** - Redis works primarily as In-Memory database with the option of synchronising the data to disk when needed. This is ideal for storing large state data like MAC Tables, Route tables, Statistics etc
	- **Pub/Sub mechanism** - In addition to working as a database Redis offers pub/sub mechanism. So it can be used as a message broker as well.
	- **High-availability** - Redis provides high-availability by supporting clusters. This would also help in Chassis based systems very well.

FlexSwitch utilizes Redis for storing system state, configuration, and externally visible events like link down, link up etc. 

