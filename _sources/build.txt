.. FlexSwitch documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.A

Building FlexSwitch from source
===============================

Pre-requisites:
^^^^^^^^^^^^^^^
    - Development environment has been setup using https://github.com/OpenSnaproute/vagrantFlexSwitchDev

    - ~/.bash.rc contains

        export SR_CODE_BASE=$HOME/git
    
        export GOPATH=$SR_CODE_BASE/snaproute/:$SR_CODE_BASE/external/:$SR_CODE_BASE/generated/
    

Instructions to build package:
------------------------------
All the platforms supported by FlexSwitch are listed in

$SR_CODE_BASE/reltools/pkgInfo.json 

Edit the above file to remove the platforms that are not needed FlexSwitch is built for all the platforms listed in the above file Run the below commands to generate packages

 ::

        cd   $SR_CODE_BASE/reltools

        python makePkg.py

 ::


The build may take around 15 min for the first package
