Ping Test 
===============

.. Note :: For this tutorial we assume that  you have docker image installed on you machine.



With this tutorial we are going to spawn 2 docker containers. 
And begin with pinging from interface on 1 docker to the other.

Lets get started

-  Start the docker with flexswitch image on it with below command

::
    
    sudo  docker run -d --log-driver=syslog --cap-add=ALL --name docker_ping1 libero18/ubuntu-14.04:Flexv8

-  Create interface eth1 with IP 20.0.1.6

::

  sudo pipework docker0 -i eth1 docker_ping1 20.0.1.6/24


-  Enter into the docker shell for docker_ping1

::
    
    sudo docker exec -it docker_ping1 bash


- All below commands are executed on the docker shell. 
    - Flexswitch needs syslog instance running before we start the flexswitch. Also we need to start redis-server before we begin with actual configurations

::
    
   rsyslogd &
   redis-server &

- flexswitch is the script used to start/stop/restart flexswitch instance. 


::
    
    /etc/init.d/flexswitch start

    - Lets start configuring interface with IP . 

::
   
     curl -H "Content-Type: application/json" -d '{"VlanId":5,"UntagIfIndexList":"2"}'    http://localhost:8080/public/v1/config/Vlan
    curl -H "Content-Type: application/json" -d '{"IpAddr": "51.1.1.5/24", "IfIndex":33554437}' http://localhost:8080/public/v1/config/IPv4Intf

-  Create another docker instance with name “docker_ping2” and start flexswitch package

Following commands are same as commands 1 to 8 to create another docker instance with interface on it.

 
::


    docker run -d --log-driver=syslog --cap-add=ALL --name docker_ping2 libero18/ubuntu--14.04:Flexv8

   sudo pipework docker0 -i eth1 docker_ping2 20.0.1.6/24
   sudo docker exec -it docker_ping2 bash

   rsyslogd &
   /etc/init.d/flexswitch start

 

- On docker_ping2 create SVI and assign IP address ( This command will create vlan23 off port 2 with ip address 80.0.1.16)

::


    curl -H "Content-Type: application/json" -d '{"VlanId":5,"UntagIfIndexList":"2"}' http://localhost:8080/public/v1/config/Vlan
    curl -H "Content-Type: application/json" -d '{"IpAddr": "51.1.1.6/24", "IfIndex":33554437}' http://localhost:8080/public/v1/config/IPv4Intf

 

 

- We are ready to ping from docker_ping1

::
     
    ping 51.1.1.6

.. Note :: Ping test script location  

