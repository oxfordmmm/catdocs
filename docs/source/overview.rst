Overview
========

Pathogen genomic data analysis can be extremely bespoke and diverse. Many institutions and labs around the world have their own infrastructure and software suites to collect, process and analyze data. However, those existing solutions are difficult to use outside of the organization and the datasets for clinically validating software are also not standardized. This has hindered the research and clinical service utilizing the whole genome sequencing technology for pathogen identification and diagnosis. 

`Oxford MMM <http://modmedmicro.nsms.ox.ac.uk/>`_ software team has designed and developed Scalable Pathogen Pipeline Platform (SP3), a web-based cloud platform that enables container-centric bioinformatic workflows running on a diverse set of platforms, from single PCs to cloud infrastructure. 

SP3 fetches data from a public repository like ENA (European Nucleotide Archive) and configures bioinformatic workflows written with container-technology, like Docker or Singularity. 

SP3 maximizes usability and minimizes software and infrastructure maintenance. It exhibits an always-on managed software as a service (SaaS) where the analysis can be achieved by a few clicks without having to maintain the underlying software or hardware. 

When deployed to commercial cloud platform, it benefits from elastic cloud computing, allowing users to pay only for data processing done, rather than a fixed maintenance cost of traditional clusters. SP3 has been tested  on Google Cloud Platform (GCP), Microsoft Azure, Amazon Elastic Compute Cloud (Amazon EC2)  and OpenStack Platforms. As an open platform, SP3 promotes the reproducible, scalable and maintainable bioinformatic pipeline development. The platform is configurable and extensible through modularization , containerization and cloud-centric deployment. 
It utilizes the best regarded bioinformatic pipelines available in the pathogen research community and we are establishing a growing user base of pathogen research, clinical diagnosis and public health communities.

.. image:: _static/architecture.png

User Journey
------------

.. image:: _static/flow.png

Log in
------

User selects which SP3 cloud instance to use and logs in.

About login and register, see :ref:`user-guide`.


Fetch Data
----------
.. image:: _static/fetch.png


**From ENA**

If the genomic data that the user wishes to analyze is hosted on the ENA, SP3 can fetch it directly. The user goes to the Dataset page, clicks New Fetch, inputs the project accession and the samples to fetch and clicks New Fetch. The data is fetched from the ENA in the background and the progress can be monitored on the dataset page.

**From Other Source**

Sequence files can be transferred to the cloud server, then SP3 can fetch it from a folder. The users goes to the Dataset page, clickes New Fetch, choose LOCAL as source, and provide the folder of the data. The data is fetched from the local folder, which takes a few seconds to be ready for analysis.

Start a pipeline
----------------

Once the dataset is fetched, the user can start a new analysis by going to the Datasets page, selecting a pipeline, and clicking Run on the dataset they wish to run the analysis on. This takes them to the New Run page where they select the settings specific to this analysis pipeline. Once they submit the run, they are taken to the pipeline status page where they can monitor the progress of the run.

Monitor the Progress
--------------------

.. image:: _static/monitor.png

On the pipeline status screen, the user can click the details link to go to the run details link. This allows the user to view the nextflow log, to stop the run, view the progress per-sample and view the commands run and their output for each nextflow task. When the run is finished, the user can view the Nextflow report, the timeline, repeat the run or fetch the output as a new dataset. The details of the cluster compute can also the viewed on the Compute page, providing information on the nodes that are active, disk space status, what tasks are running on which nodes and an activity graph covering the past 24 hours.

View the report
---------------

If the pipeline has an associated report, it can be viewed at the run details page by clicking on the sample name.

.. image:: _static/ERR025833.png

