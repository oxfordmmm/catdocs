Deployment
==========

In a cloud infrasture, we create a head node with ubuntu 18.04. Then we connect to the head node to 

    1. Install Oxford Cats Software, 
    2. Plug Pipelines and 
    3. Set up Data etc. 

Install Cats
------------

**Install distribution software**

* Update repository:

.. code-block:: bash

   sudo apt update

* Install etckeeper:

.. code-block:: bash

    sudo apt install etckeeper

* Install packages necessary for python deployment

.. code-block:: bash

    sudo apt install build-essential python3-virtualenv virtualenv libpython3-all-dev

**Install nextflow**

.. code-block:: bash

    sudo apt install openjdk-8-jre-headless
    cd
    wget https://github.com/nextflow-io/nextflow/releases/download/v18.10.1/nextflow-18.10.1-all -O nextflow
    sudo mv nextflow /usr/bin
    sudo chmod a+x /usr/bin/nextflow

**Install openVPN**

.. code-block:: bash

    sudo apt install openvpn

**Install SP3 software**

* Create sp3 directory

.. code-block:: bash

    cd
    mkdir ~/sp3

* Install catgrid

.. code-block:: bash

    cd ~/sp3
    git clone https://gitlab.com/MMMCloudPipeline/hypergrid catgrid
    cd catgrid
    virtualenv -p python3 env
    source env/bin/activate
    pip3 install -r requirements.txt

* Copy =slurm_emu= files to /usr/bin

.. code-block:: bash

    cd ~/sp3/catgrid/tools
    sudo cp slurm_emu/* /usr/bin
    sudo chmod a+x /usr/bin/{sbatch,squeue,scancel}

* install catcloud

.. code-block:: bash

    cd ~/sp3
    git clone https://gitlab.com/MMMCloudPipeline/catcloud catcloud
    cd catcloud
    virtualenv -p python3 env
    source env/bin/activate
    pip3 install -r requirements.txt
    cp config.yaml-example config.yaml

* Install catweb

.. code-block:: bash

    cd ~/sp3
    git clone https://gitlab.com/MMMCloudPipeline/catweb catweb
    cd catweb
    virtualenv -p python3 env
    source env/bin/activate
    pip3 install -r requirements
    cp config.yaml-example config.yaml

* Install fetch-api

.. code-block:: bash

    cd ~/sp3
    git clone https://gitlab.com/MMMCloudPipeline/fetchapi fetch-api
    cd fetch-api
    virtualenv -p python3 env
    source env/bin/activate
    pip3 install -r requirements.txt
    mkdir logs

* Install download-api

.. code-block:: bash

    cd ~/sp3
    git clone https://gitlab.com/MMMCloudPipeline/download-api
    cd download-api
    virtualenv -p python3 env
    source env/bin/activate
    pip3 install -r requirements.txt

* Install resistance

.. code-block:: bash

    cd ~/sp3
    git clone https://gitlab.com/MMMCloudPipeline/resistance
    cd resistance
    git submodule init
    git submodule update
    virtualenv -p python3 env
    source env/bin/activate
    export PYTHONPATH=~/.local/lib/python3.6/site-packages/
    cd gemucator
    python3 setup.py install --user
    cd ..
    cd piezo
    pip3 install datreant tqdm pandas pyvcf
    python3 setup.py install --user
    cd ..
    cd resistanceapi
    pip3 install -r requirements.txt

* Install catreport

.. code-block:: bash

    cd ~/sp3
    git clone https://gitlab.com/MMMCloudPipeline/catreport.git
    cd catreport
    virtualenv -p python3 env
    source env/bin/activate
    pip3 install -r requirements.txt

* Install and configure nginx

.. code-block:: bash

    sudo apt install nginx

* Copy sp3 nginx config

.. code-block:: bash

    cd /etc/nginx/sites-available
    sudo wget 'https://files.mmmoxford.uk/f/7b7bd07669b5417e8998/?dl=1' -O sp3
    cd /etc/nginx/sites-enabled
    sudo ln -s /etc/nginx/sites-available/sp3

* Copy domain keys to =/etc/letsencrypt/=

.. code-block:: bash

    sudo mkdir /etc/letsencrypt/

    Copy =domain.cert.pem= and =domain.key.pem= to =/etc/letsencrypt/=

    Copy =/etc/letsencrypt/options-ssl-nginx.conf= and =/etc/letsencrypt/ssl-dhparams.pem= to =/etc/letsencrypt/=

* Edit nginx config

.. code-block:: bash

    edit =/etc/nginx/sites-available/sp3=

* Restart nginx

.. code-block:: bash

    sudo systemctl restart nginx

Plug Pipelines
--------------

1. Clone pipeline code to /data/pipelines/bug-flow

2. Create/copy config file ~/sp3/catweb/config.yaml

3. Add one line to ~/sp3/catweb/config.yaml Under the "nextflows:" add

.. code-block:: yaml

   "- !include config.yaml.d/davideyre/bug-flow.yaml"

4. Copy singularity files to /data/images

5. Restart catweb api and ui

Set up Data Store
-----------------

**Create directories**

.. code-block:: bash

    sudo mkdir -p /data /work
    sudo chown ubuntu:ubuntu /data /work
    sudo mkdir -p /db
    sudo chown ubuntu:ubuntu /db

**Move data into correct folders**

The =/data= directory is mounted read-only on the compute nodes

Files that don't change should be owned by root and not writable by other users

.. code-block:: bash

    cd ~/sp3
    git clone https://gitlab.com/MMMCloudPipeline/persistence
    cd persistence
    pip3 install flask pyyaml requests


** Persistent store configuration

* Example configuration

.. code-block:: yaml

    name: Cats
    id: 44444444-4444-4444-4444-444444444444
    store: 131.251.130.111
    url: https://cats.oxfordfun.com
    contact: denis.volk@ndm.ox.ac.uk
    description: SP3 instance in CLIMB Cardiff

**Explanation of fields**

+---------------+----------------------------------+
| Field name    | Field description                |
+===============+==================================+
| name          | Name of cluster instance         |
+---------------+----------------------------------+
| id            | UUIDv4 of instance               |
+---------------+----------------------------------+
| store         | persistent store host address    |
+---------------+----------------------------------+
| url           | URL of catweb for this instance  |
+---------------+----------------------------------+
| contact       | Contact email for instance admin |
+---------------+----------------------------------+
| description   | Instance description             |
+---------------+----------------------------------+
