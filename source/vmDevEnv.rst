Welcome to FlexSwitch Setting Up Development Environment
========================================================

Using Virtual Box
-----------------

Please follow the following instruction:

- Install Virtual Box from `here <https://www.virtualbox.org/wiki/Downloads>`_
- Download the Virtual Box Appliance from `here <https://drive.google.com/open?id=0B-H6d4gwmuunTDJrZnc5Q3pJNEU>`_
- Import the `SnapRoute.ova <https://drive.google.com/open?id=0B-H6d4gwmuunTDJrZnc5Q3pJNEU>`_ image

        - Username: snaproute
        - Password: snaproute

- Execute following command
        - sudo apt-get update
        - sudo apt-get install build-essential fabric git

- Clone Reltools from `OpenSnapRouter <http://www.github.com/Opensnaproute>`_

        - Change directory to home directory
                - cd /home/snaproute
                - mkdir git
                - cd git
                - git clone https://github.com/OpenSnaproute/reltools.git

        - Get OpenSnapRoute Source Code
                - cd ~/git/reltools
                - fab setupDevEnv

        - Build Debian Package
                - cd ~/git/reltools
                - python makePkg.py


Reference:

`How to setup Host only adapter? <http://askubuntu.com/questions/293816/in-virtualbox-how-do-i-set-up-host-only-virtual-machines-that-can-access-the-Setting>`_
