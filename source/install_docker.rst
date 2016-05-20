Getting ready with flexswitch 
==========================================

Load docker image
^^^^^^^^^^^^^^^^^^^^^
Flexv34.tar is the docker image with flexswitch package infused with it. 
We have used ubuntu 14.04 base image to create this package. 
::
    
    Prerequisites - Preinstalled Docker on the host machine.

- Download your .tar image from here

- Load the image   
 
:: 
  
   load < Flex34.tar
   
   docker images

   <TODO add command output >

Start the container 
^^^^^^^^^^^^^^^^^^^^^
- Instantiate a container using command  

docker run -d --log-driver=syslog  --cap-add=ALL  --name flex_container libero18/ubuntu-14.04:Flexv5


::

 **Note**  The flags used while spawning container . Which are necessary for proper functioning of the flexswitch
    --log-driver  This will enable syslog support for logging
    --cap-add=ALL In order to create/get on  linux interfaces enable all permissions.

Verify Flexswitch installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- Before starting the flexswitch start the syslog service and redis-server

:: 


     rsyslogd &
     redis-server &

- /etc/init.d/flexswitch is the script to start /stop the flexswitch daemons. 

:: 

 
/etc/init.d/flexswitch <start/stop/restart>

Basic commands 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Once all daemons are up , here are the basic commands you can use to get started . Note that the successive tutorials will cover detailed illustrations about configuration and debugging.

- To access all REST APIs use swagger 

http://localhost:8080/api-docs/

- Check system health 

::
 
    http://<host_ip>:8080/public/v1/state/SystemStatus

    {
    "ObjectId": "",
    "Object": {
    "ConfigObj": null,
    "Name": "7abb27f0ad2a",
    "SwVersion": "",
    "Ready": true,
    "Reason": "None",
    "UpTime": "19h54m58.355328307s",
    "NumCreateCalls": "Total 19 Success 15",
    "NumDeleteCalls": "Total 0 Success 0", 
    "NumUpdateCalls": "Total 4 Success 4",
    "NumGetCalls": "Total 1 Success 0",
    "NumActionCalls": "Total 0 Success 0",
    "FlexDaemons": [
    {

