Deployment
==========

In a cloud infrasture,  a head node is needed to created with ubuntu 18.04. Then we connect to the head node to 

    1. Install Oxford Cats Software
    2. Start Oxford Cats Services
    3. Plug Pipelines


Install Cats Software
---------------------

.. code-block:: bash

    cd sp3doc
    bash install.bash
    

Start Cats Services
-------------------
.. code-block:: bash

    cd sp3doc
    bash systemd-start.sh


Plug Pipelines
--------------

1. Clone pipeline code eg. to /data/pipelines/bug-flow

2. Create sp3 configuration file for the pipeline, eg. bug-flow.yaml

3. Add one line to ~/sp3/catweb/config.yaml Under the "nextflows:" add

.. code-block:: yaml

   "- !include config.yaml.d/davideyre/bug-flow.yaml"
  
4. Copy singularity files to /data/images

5. Copy references, other dependencies to /data/references

6. Copy test data to /data/inputs/uploads/

7. Restart catweb api and ui

.. code-block:: bash

   systemctl restart catwebapi --user
   systemctl restart catwebui --user
