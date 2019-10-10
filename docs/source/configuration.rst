Configuration
-------------

CatWeb Configuration Example
----------------------------

.. code-block:: yaml

    contexts:
    - name: local
        prog_dirs:   '/data/pipelines'
        root_dirs:   '/work'
        output_dirs: '/work/output'
        images_dir:  '/data/images'

    canonical_prog_dir: '/data/pipelines'
    log_dir: '/home/ubuntu/sp3/catweb/logs'
    db_target: '/db/catweb.sqlite'
    download_url: 'https://download-cats.oxfordfun.com/files/'

    nextflows:
    - !include config.yaml.d/clockwork/variant_call.yaml

    nfweb_api: { host: '127.0.0.1', port: '7100' }
    fetch_api: { host: '127.0.0.1', port: '7200' }

    authentication: ldap

    ldap:
    - name: 'ndm.local'
        host: '192.168.7.16'
        admins: ['denisv@ndm.local', 'fan@ndm.local']

    users:
    - name: compass

    cluster_view:
    disk_filter: "home|sda|sdb|sdc"
    embeds:
        - title: 'Statistics'
        - img: 'https://stat-cats.oxfordfun.com/draw'

**Explanation of the fields**

+-----------------------------+--------------------------------------------------------------------------------+
| Name                        | Explanation                                                                    |
+-----------------------------+--------------------------------------------------------------------------------+
| - contexts                  | - list of contexts                                                             |
| - contexts.name             | - set as local                                                                 |
| - contexts.prog_dirs        | - directory containing nextflow pipelines (will be  - {prog_dirs}/{flow_name}) |
| - contexts.root_dirs        | - directory containing nextflow run files (will be  - {root_dirs}/runs/{uuid}/)|
| - contexts.output_dirs      | - directory containing nextflow outputs (will be  - {output_dirs}/{uuid})      |
+-----------------------------+--------------------------------------------------------------------------------+
| - canonical_prog_dir        | - ~prog_dir~ that is used by catweb to get nextflow pipeline versions from git |
| - log_dir                   | - directory to put catweb configuration files into                             |
| - db_target                 | - sqlite database filepath                                                     |
| - download_url              | - prefix for nginx file downloads (url will be  - {download_url}/{uuid} - )    |
+-----------------------------+--------------------------------------------------------------------------------+
| - nextflows                 | - list of flows                                                                |
| - nextflows.!include        | - flows to include                                                             |
+-----------------------------+--------------------------------------------------------------------------------+
| - nfweb_api.host            | - hostname of nfweb api                                                        |
| - nfweb_api.port            | - port of nfweb api                                                            |
+-----------------------------+--------------------------------------------------------------------------------+
| - fetch_api.host            | - hostname of fetch api                                                        |
| - fetch_api.port            | - port of fetch api                                                            |
+-----------------------------+--------------------------------------------------------------------------------+
| - ldap                      | - list of ldap                                                                 |
| - ldap.name                 | - name of ldap configuration                                                   |
| - ldap.host                 | - hostname of ldap server                                                      |
| - ldap.admins               | - list of ldap admins                                                          |
+-----------------------------+--------------------------------------------------------------------------------+
| - users.name                | - name of users                                                                |
+-----------------------------+--------------------------------------------------------------------------------+
| - cluster_view              | - Catweb cluster view configuration                                            |
| - cluster_view.disk_filter  | - Regular expression identifying which disks to display                        |
| - cluster_view.embeds       | - List of embeds                                                               |
| - cluster_view.embeds.title | - Title of embed                                                               |
| - cluster_view.embeds.img   | - Link of embed                                                                |
+-----------------------------+--------------------------------------------------------------------------------+


Pipeline Configuration Example
------------------------------

.. code-block:: yaml

    name: "Clockwork_VC"
    display_name: "Clockwork variant call"
    script: "vc.nf"
    show: yes
    root_dir: "clockworkcloud/"
    prog_dir: "clockworkcloud/"
    output_dir: "output/"
    version: "0.1"
    description: "Clockwork variant vall"
    contexts:
    - name: local
        arguments: "-process.executor slurm"
    param:
    description:
        - name: 'ref_dir'
        arg: "--ref_dir"
        type: switch
        desc: "Reference directory"
        globs:
            - /data/references/clockwork/qc_vc/*
        - name: 'indir'
        arg: '--input_dir'
        type: input-reqr
        desc: "Input directory"
        - name: 'readpat'
        arg: '--read_pattern'
        type: input-reqr
        desc: "Input file pattern"
    output:
        parameter: "--output_dir"
    count_tasks_per_sample: 5

**Explanation of the fields**

+----------------------------+--------------------------------------------------------------------+
| Field name                 | Field description                                                  |
+----------------------------+--------------------------------------------------------------------+
|  name                      | Name of pipeline                                                   |
+----------------------------+--------------------------------------------------------------------+
|  display_name              | Name to display in catweb                                          |
+----------------------------+--------------------------------------------------------------------+
|  script                    | Nextflow script filename                                           |
+----------------------------+--------------------------------------------------------------------+
|  show                      | Toggle showing this script in catweb ( yes / no )                  |
+----------------------------+--------------------------------------------------------------------+
|  root_dir                  | Not used                                                           |
+----------------------------+--------------------------------------------------------------------+
|  prog_dir                  | Directory of nextflow pipeline relative to the context prog_dirs   |
+----------------------------+--------------------------------------------------------------------+
|  description               | Description of pipeline                                            |
+----------------------------+--------------------------------------------------------------------+
|  - contexts                | - List of contexts                                                 |
|  - contexts.name           | - Name of context                                                  |
|  - contexts.arguments      | - Arguments specific to this context                               |
+----------------------------+--------------------------------------------------------------------+
|  - param                   | - List of params                                                   |
|  - param.description       | - Description of params                                            |
|  - param.description.name  | - Name of parameter                                                |
|  - param.description.arg   | - Nextflow command-line key for parameter                          |
|  - param.description.type  | - switch  or  input-reqr                                           |
|  - param.description.desc  | - Description of parameter                                         |
|  - param.output            | - output                                                           |
|  - param.output.parameter  | - Nextflow command-line key that determines the output directory   |
|  - count_tasks_per_sample  | - How many nextflow tasks (processes) there are per input sample   |
+----------------------------+--------------------------------------------------------------------+