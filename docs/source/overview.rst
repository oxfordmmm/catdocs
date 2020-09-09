Overview
========

Pathogen genomic data analysis can be extremely bespoke and diverse. Many institutions and labs around the world have their own infrastructure and software suites to collect, process and analyze data. However, those existing solutions are difficult to use outside of the organization and the datasets for clinically validating software are also not standardized. This has hindered the research and clinical service utilizing the whole genome sequencing technology for pathogen identification and diagnosis. 

`Oxford MMM <http://modmedmicro.nsms.ox.ac.uk/>`_ software team has designed and developed Scalable Pathogen Pipeline Platform (SP3), a web-based cloud platform that enables container-centric bioinformatic workflows running on a diverse set of platforms, from single PCs to cloud infrastructure. 

.. image:: _static/architecture.png

SP3 fetches data from a public repository like ENA (European Nucleotide Archive) and configures bioinformatic workflows written with container-technology, like Docker or Singularity. 

SP3 maximizes usability and minimizes software and infrastructure maintenance. It exhibits an always-on managed software as a service (SaaS) where the analysis can be achieved by a few clicks without having to maintain the underlying software or hardware. 

When deployed to commercial cloud platform, it benefits from elastic cloud computing, allowing users to pay only for data processing done, rather than a fixed maintenance cost of traditional clusters. SP3 has been tested  on Google Cloud Platform (GCP), Microsoft Azure, Amazon Elastic Compute Cloud (Amazon EC2)  and OpenStack Platforms. As an open platform, SP3 promotes the reproducible, scalable and maintainable bioinformatic pipeline development. The platform is configurable and extensible through modularization , containerization and cloud-centric deployment. 
It utilizes the best regarded bioinformatic pipelines available in the pathogen research community and we are establishing a growing user base of pathogen research, clinical diagnosis and public health communities.

