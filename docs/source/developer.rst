Pipeline Developer Guide
========================

Prerequisites
-------------

To deploy a bioinformatic pipeline in SP3, 

0. Pipeline code has to be version controlled in a Git repo (github, gitlab or gitea etc.).

1. Pipeline is written in Nextflow, calling scripting language like shell, python or R etc.

2. Pipeline has a container with all 3rd party dependencies using either docker or singularity.

A sample of such pipeline is `here <https://github.com/oxfordfun/FunVCF>`_.


Nextflow Checklist
------------------

- Have an **input** directory as a parameter (e.g. --input_dir)
- Have an **output** directory as a parameter (e.g. --output_dir)
- Have a file **pattern** for the input files (e.g. --readpat)
- Have different profiles for different enviornment in nextflow.config
- Have output data explicitly in **output** channel, do not use \*.\*
- Have **publishDir** in process to explicitly claim final output files
- Have **tag** to identify individual sample identifier
- Have memory usage set for process that has high memory usage, e.g. **memory '10 G'** for centrifuge


Nextflow Do NOT
---------------

- Do Not write to input directory
- Do Not write to reference/database directory
- Do Not write to /tmp, use **scratch true** instead
- Do Not write anywhere except nextflow work directory
- Do Not change work directory
- Do Not access files outside of channel except reference files
- Do Not create files outside of channel
- Do Not have a list of scripts in one process if they do not have to run together.

Docker Checklist
----------------

- Have a folder called **Docker** for Docker build context, including Docker file and files that needed to be copied into Docker.
- Build **FROM** an official and small size image
- Have **LABEL** with version, description, maintainer, dockerhub link etc.
- Split **RUN** command in lines for better readability
- Use **WORKDIR** instead of profiferating instructions like RUN cd && do-something- 

Best Docker Practice can be found at `Docker Docs <https://docs.docker.com/develop/develop-images/dockerfile_best-practices/>`_.