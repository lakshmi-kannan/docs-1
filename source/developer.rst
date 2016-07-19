.. FlexSwitchSDK documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Developers Home              
===============

How to contribute
^^^^^^^^^^^^^^^^^
FlexSwitch is built with the following design principles


Building FlexSwitch From Sources
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
FlexSwitch software consists of various protocol suites and infrastructure components. All the components in the system
were designed to be modular and independent of each other. 
For this reason we have organized the code as separate git repositories.
However to facilitate building one complete installable software we have an overarching repository called reltools. 
Follow the instructions described in the below section to build a package for deployment.

.. toctree::
   :maxdepth: 1

    Build instructions <build>

System Architecture
^^^^^^^^^^^^^^^^^^^
FlexSwitch is built with the following design principles
    - Model driven architecture, Each protcol/component has well defined model. 
    - Micro service architecture, Each protocols/component can function independently
    - Flexible and Modular architecture

.. toctree::
   :maxdepth: 1

    Architecture details <architecture>

Open Source Components
^^^^^^^^^^^^^^^^^^^^^^
FlexSwitch, being an opensource soultion, relies on several other opensource components.
These OpenSource components are of great help in simplifying our implementation. 
We acknowledge and are grateful to these developers for their contributions to open source.
You can find the source code of their open source projects along with license information below. 


.. toctree::
   :maxdepth: 1

    Open Source components <opensources>

Creating New Component
^^^^^^^^^^^^^^^^^^^^^^
Adding a new component to the FlexSwitch Software requires a few steps to get started.  In addition to getting
the basics started users should know what utilities have been written in aiding the creation of new modules.

.. toctree::
   :maxdepth: 1

   Daemon Creation Quick Start Example <daemon_quick_start>
   Daemon Creation Details <daemon>


Design Decisions 
^^^^^^^^^^^^^^^^^

.. toctree::
   :maxdepth: 1

    Design Decisions <decisions>

