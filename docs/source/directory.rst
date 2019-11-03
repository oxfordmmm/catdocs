Data Types
==========

Cats software
-------------

+----------------------------+-------------------------+-------+
| directory/file             | contents                | owner |
+============================+=========================+=======+
| ~/sp3/catcloud             | catcloud                | user  |
+----------------------------+-------------------------+-------+
| ~/sp3/catgrid              | catgrid                 | user  |
+----------------------------+-------------------------+-------+
| ~/sp3/catreport            | catreport               | user  |
+----------------------------+-------------------------+-------+
| ~/sp3/catstat              | catstat                 | user  |
+----------------------------+-------------------------+-------+
| ~/sp3/catweb               | catweb                  | user  |
+----------------------------+-------------------------+-------+
| ~/sp3/catweb/config.yaml.d | catweb pipeline configs | user  |
+----------------------------+-------------------------+-------+
| ~/sp3/cattag/              | cattag                  | user  |
+----------------------------+-------------------------+-------+
| ~/sp3/downloadapi          | downloadapi             | user  |
+----------------------------+-------------------------+-------+
| ~/sp3/fetchapi             | fetchapi                | user  |
+----------------------------+-------------------------+-------+
| ~/sp3/resistance           | resistance              | user  |
+----------------------------+-------------------------+-------+

Static Data
-----------

+-----------------------------------------+-------------------------+---------------+-----------------------------------------------------+
| directory/file                          | contents                | owner         |               Notes                                 |
+=========================================+=========================+===============+=====================================================+
| /data/images                            | container images        | root          |One pipeline could have one or more container images |
+-----------------------------------------+-------------------------+---------------+-----------------------------------------------------+
| /data/pipelines                         | nextflow pipelines      | root          |Pipeline software, source controlled in Git          |
+-----------------------------------------+-------------------------+---------------+-----------------------------------------------------+
| /data/references                        | reference data          | root          |Genome references, Taxonomic classification databases|
+-----------------------------------------+-------------------------+---------------+-----------------------------------------------------+
| /data/reports/resistance/data           | resistance data         | root          |Genbank file, resistance catalog etc.                |
+-----------------------------------------+-------------------------+---------------+-----------------------------------------------------+
| /data/fetch                             | fetch api data          | fetch api     |Data fetched to Cloud from ENA                       |
+-----------------------------------------+-------------------------+---------------+-----------------------------------------------------+
| /data/inputs                            | fetch api symlinks      | fetch api     |Data fetched to Cloud by SFTP                        |
+-----------------------------------------+-------------------------+---------------+-----------------------------------------------------+

Dynamic Data
------------

+-----------------------------------------+-------------------------+---------------+
| directory/file                          | contents                | owner         |
+=========================================+=========================+===============+
| /work/runs                              | pipeline runs           | nextflow      |
+-----------------------------------------+-------------------------+---------------+
| /work/output                            | pipeline outputs        | nextflow      |
+-----------------------------------------+-------------------------+---------------+
| /work/reports/catreport/reports         | report files            | catreport     |
+-----------------------------------------+-------------------------+---------------+
| /work/reports/resistanceapi/vcfs        | resistanceapi temp      | resistanceapi |
+-----------------------------------------+-------------------------+---------------+
| /work/logs/reports/resistanceapi        | resistanceapi logs      | resistanceapi |
+-----------------------------------------+-------------------------+---------------+
| /work/logs/fetchapi*                    | fetchapi logs           | fetchapi      |
+-----------------------------------------+-------------------------+---------------+
| /work/logs/catweb*                      | catweb logs             | catweb        |
+-----------------------------------------+-------------------------+---------------+

Audit Trail Data
----------------

+----------------------+--------------------------+-----------+
| directory/file       | contents                 | owner     |
+======================+==========================+===========+
| /db/catweb.sqlite    | nextflow runs  etc.      | catweb    |
+----------------------+--------------------------+-----------+
| /db/catreport.sqlite | report files and path    | catreport |
+----------------------+--------------------------+-----------+
| /db/fetch-api.sqlite | fetch queues and datasets| fetch-api |
+----------------------+--------------------------+-----------+
| /db/cattag.sqlite    | tags for runs and samples| cattag    |
+----------------------+--------------------------+-----------+


Nginx Configuration
-------------------

+-----------------------------------------+-------------------------+---------------+
| directory/file                          | contents                | owner         |
+=========================================+=========================+===============+
| /etc/nginx/sites-available/sp3          | sp3 nginx config        | root          |
+-----------------------------------------+-------------------------+---------------+
| /etc/letsencrypt/domain.cert.pem        | domain cert             | root          |
+-----------------------------------------+-------------------------+---------------+
| /etc/letsencrypt/domain.key.pem         | domain key              | root          |
+-----------------------------------------+-------------------------+---------------+
| /etc/letsencrypt/options-ssl-nginx.conf | nginx ssl options       | root          |
+-----------------------------------------+-------------------------+---------------+
| /etc/letsencrypt/ssl-dhparams.pem       | nginx ssl options       | root          |
+-----------------------------------------+-------------------------+---------------+


Clockwork Output Data
---------------------

.. image:: _static/cwoutput.png


Clockwork Reporting Data
-------------------------

+-------------------------+-------------------------+-----------------+
| Process                 | Files                   | Notes           |
+=========================+=========================+=================+
| Kraken2                 | ERR550931_kraken2.tab   | reported        |
+-------------------------+-------------------------+-----------------+
| Mykrobe                 | mykrobe_output.json     | reported        |
+-------------------------+-------------------------+-----------------+
| Reference               | reference_info.txt      | reported        |
+-------------------------+-------------------------+-----------------+
| Samtool QC              | samtools_qc.stats       | reported        |
+-------------------------+-------------------------+-----------------+
| Resistance              | final.vcf               | reported        |
+-------------------------+-------------------------+-----------------+


Data Storage
------------

**Ephemeral**

Ephemeral data are available when the cloud instance is running and the run has not been deleted from the cloud instance, such as dynamic data, output data.

**Short-term**

Pipeline input data (fastq or bam) are available on Cloud for a short period of time, say 2 weeks to 2 months based on the capacity of the platform.

Pipeline output data (e.g. Clockwork TB pipeline output) will be available for short-term, say 2 weeks to 2 months based on the capacity of the platform.

**Persistent**

Persistent data are needed to be available without cloud instance running, which should be stored in a dedicated storage, such as static data, audit trail data, reporting data.

**Long-term**

Persistent data can be available for long-term access based on user wish and cost of storage. 
