Getting started with flexswitch on Docker
==========================================
The below instructions describe how to use FlexSwitch on Vagrant.  This is just a ubuntu 14.04 image with FlexSwitch running on top 

Instructions on how to get Vagrant box up with FlexSwitch:

Download this files "snaproute.box" and "VagrantFile" from 

https://github.com/OpenSnaproute/binaries/tree/master/vagrant

1)Make folder to store images:
        mkdir srBox; cd srBox
        
2)Copy files into srBox:
        cp snaproute.box VagrantFile srBox/
        
3) vagrant box add SnapRoute112 snaproute.box
4) vagrant up
5) vagrant ssh
     password is vagrant


This image is based on Ubuntu 14.04 and two ports are created within this image by default
"Eth0" and "Eth1”.


