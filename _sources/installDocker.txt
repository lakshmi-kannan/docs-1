Getting ready with flexswitch 
==========================================

Load docker image
^^^^^^^^^^^^^^^^^^^^^
Flexv43.tar is the docker image with flexswitch package infused with it. 
We have used ubuntu 14.04 base image to create this package. 
::
    
    Prerequisites - Preinstalled Docker on the host machine.

- Download your .tar image 

- Load the image   
 
:: 
  
   load < Flex43.tar
   
   docker images

   @snaproute-lab-r710-1:~$ docker images
   REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
   libero18/ubuntu-14.04         Flexv43             311d7db88fdf        5 hours ago         605.5 MB


Start the container 
^^^^^^^^^^^^^^^^^^^^^
- Instantiate a container using command  

docker run -dt --privileged --log-driver=syslog --cap-add=ALL  --name Spine1 --ip 192.168.0.2 --net=clos-oob-network  -P libero18/ubuntu-14.04:Flexv43


::

 **Note**  The flags used while spawning container . Which are necessary for proper functioning of the flexswitch
    --log-driver  This will enable syslog support for logging
    --cap-add=ALL In order to create/get on  linux interfaces enable all permissions.
    --net - To create docker network for management IPs.

Verify Flexswitch installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- When docker container is spawned by default we start rsyslogd and redis-server. 


- /etc/init.d/flexswitch is the script to start /stop the flexswitch daemons. 

:: 

 
/etc/init.d/flexswitch <start/stop/restart>

Basic commands 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- Start flexswitch 

::

    service flexswitch start



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

- In case you need to flush all database and restart all daemons

::

   redis-cli
    run command "flushdb"


- Note that the successive tutorials will cover detailed illustrations about configuration and debugging.

