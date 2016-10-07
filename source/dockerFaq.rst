FAQs
===============


1) **how to test whether syslog and redis-server are running** ?

As a part of docker_startup.sh script , syslog and redis will be runnning in your docker container. if you want to verify 

ps -aux | grep redis   
ps -aux | grep rsyslog 

2) **How to assign the ip address to each of the containers ?**

When the containers are spawned IP address is already assigned to them .For example

eth0      Link encap:Ethernet  HWaddr 02:42:ac:11:00:04  
          inet addr:172.17.0.4  Bcast:0.0.0.0  Mask:255.255.0.0
          inet6 addr: fe80::42:acff:fe11:4/64 Scope:Link 
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:38 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:5339 (5.3 KB)  TX bytes:648 (648.0 B)


To assign the IP address to the interface that are created by the script , you need to run curl command for IPv4Intf .

3) How to log-in to the switch ?


There is no explicit login for the switch. Once you are inside the docker container its a running switch itself. You can check state or config using REST commands.



**Frequently seen error messages and their causes**


1) When running docker_startup.sh

See 'docker run --help'.
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
Cannot connect to the Docker daemon. Is the docker daemon running on this host?
ln: failed to create symbolic link ‘/var/run/netns/net’: Permission denied
ln: failed to create symbolic link ‘/var/run/netns/net’: Permission denied
-e done!

Solution - Run the script in sudo mode.

2) 

root@0f5d1d2455fc:/# curl -H "Content-Type: application/json" -d '{"IpAddr": "40.1.1.2/24", "IntfRef": "eth35"}'http://localhost:8080/public/v1/config/IPv4Intf                                  
curl: (7) Failed to connect to localhost port 8080: Connection refused

This most of the times mean flexswitch didnt start correctly. You can check if there is any daemon running using

ps -aux | grep flex

Start flexswitch using 

/etc/init.d/flexswitch start



Note : 
Current docker_startup script located below is provided for ubuntu platform 
https://github.com/OpenSnaproute/test

 
