.. FlexSwitch documentation master file, created by
   sphinx-quickstart on Mon Apr  4 12:27:04 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


Network Engineer Guide
======================

The scope of this page is to detail the steps required to configure SnapRoute FlexSwitch networking stack on a white box switch running ONIE (Open Network Install Environment) Or Standalone package.  
As we all as examples of initial configurations made on the device’s utilizing console port or with the management port used for the ONIE kick process and an understanding of how to interact with the system. 

.. toctree::
   :maxdepth: 1

    ONIE Installation instructions <ONIE_Install>
    FlexSwitch Package Installation <flexswitch_install>
    Configuring FlexSwitch via CLI <cli_config>
	Configuring FlexSwitch via Ansible <ansible_config>
	Configuring FlexSwitch via REST <rest_config>
	Configuring FlexSwitch via Python SDK <python_config>


For more detail configuration examples can be viewed here:

    `Configuration Examples <example.html>`_


Supporting Documentation
************************

- `ONIE <https://github.com/opencomputeproject/onie/wiki>`_
- `Swagger <http://swagger.io>`_
- `JSONView for Chrome <https://chrome.google.com/webstore/detail/chklaanhfefbnpoihckbnefhakgolnmc>`_
- `Ansible <https://www.ansible.com>`_
- `Jinja2 <http://jinja.pocoo.org/docs/dev/>`_
