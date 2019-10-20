Deployment
==========

In a cloud infrasture, we create a head node with ubuntu 18.04. Then we connect to the head node to 

    1. Install Oxford Cats Software
    2. Start Oxford Cats Services
    3. Plug Pipelines


Install Cats Software
------------

.. code-block:: bash

    cd sp3doc
    bash install.bash
    

Start Cats Services
------------
.. code-block:: bash

    cd sp3doc
    bash systemd-start.sh


Plug Pipelines
--------------

1. Clone pipeline code to /data/pipelines/bug-flow

2. Create/copy config file ~/sp3/catweb/config.yaml

3. Add one line to ~/sp3/catweb/config.yaml Under the "nextflows:" add

.. code-block:: yaml

   "- !include config.yaml.d/davideyre/bug-flow.yaml"

4. Copy singularity files to /data/images

5. Restart catweb api and ui
