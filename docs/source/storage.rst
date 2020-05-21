.. _data-storage:

Data storage
============

As shown below, SP3 data are stored in three types of storage (blue blocks) and they serve different purposes:

.. image:: _static/architecture.png

+------------------------+---------------------------------+---------------------------+------------------------------+
|    SP3 Storage         |           Where is it ?         |     What files stored?    |         Data Life            |
+========================+=================================+===========================+==============================+
| Temp Storage           |         SP3 Cloud sites         | input and output files    |         Ephemeral (Weeks)    |
+------------------------+---------------------------------+---------------------------+------------------------------+
| Local Storage          |          Local Premise          | input and output files    |         User Preference      |
+------------------------+---------------------------------+---------------------------+------------------------------+
| Persistent Storage     |         SP3 S3 Storage          |     Requested output      |        Long-terms (Years)    |
+------------------------+---------------------------------+---------------------------+------------------------------+


Temp storage (SP3 Cloud Storage)
--------------------------------

To run a pathogen pipeline, raw or pre-processed sequencing data (paired fastq files or bam files ) needs to be fetched to the Cloud platform storage, such as Amazon Elastic Block Volume (EBS).

These volumes can be attached to compute nodes and we use these volumes just like a hard drive.

Cloud storage not only keeps sequencing data (paired fastq files or bam files), but also supports the run temporary files (nextflow work folder etc), audit trail data and output files (bam files, vcf
files, fasta files etc.). 

On one Cloud site, if we have a capacity up to 10T cloud storage, we can run up to 5000 samples using the SP3 Cloud storage as one sample will take up to 2G of space (see below). SP3 Cloud
storage is equivalent to Amazon EBS Volumes.

To allow more sample running, data needs to be either deleted or moved from Cloud storage to Local storage or to Persistent storage, in our case, Amazon Simple Storage Service (S3).

Local storage
-------------

After a run completes, users can download all output data to a local storage using a single command, such as:

.. code-block:: bash

    wget -m -nH --cut-dirs=1 -np -R 'index.*'
    https://download-sp3ebi.mmmoxford.uk/files/c3f8f038-27cd-4951-b9ae-60301e0b7fa3/


Different pipeline will have different output files, for example, clockwork will have output like following:

.. code-block:: bash

    /work/output/407f775a-04d9-4276-8220-4628ffbe0edb
    8 directories, 26 files
    Total size: 791M

    └── ERR025833
        ├── cortex
        │   └── cortex.out
        │       └── vcfs
        │           └── cortex_wk_flow_I_RefCC_FINALcombined_BC_calls_at_all_k.raw.vcf
        ├── minos
        │   ├── final.vcf
        │   ├── gvcf.fasta
        │   ├── gvcf.samtools.vcf
        │   └── gvcf.vcf.gz
        ├── samtools
        │   ├── rmdup.bam
        │   └── samtools.vcf
        ├── samtools_qc
        │   ├── het_snps.het_calls.vcf
        │   ├── het_snps.per_contig.tsv
        │   ├── het_snps.summary.tsv
        │   ├── samtools_qc.plot-acgt-cycles.png
        │   ├── samtools_qc.plot-coverage.png
        │   ├── samtools_qc.plot-gc-content.png
        │   ├── samtools_qc.plot-gc-depth.png
        │   ├── samtools_qc.plot-indel-cycles.png
        │   ├── samtools_qc.plot-indel-dist.png
        │   ├── samtools_qc.plot-insert-size.png
        │   ├── samtools_qc.plot-mism-per-cycle.png
        │   ├── samtools_qc.plot-quals-hm.png
        │   ├── samtools_qc.plot-quals.png
        │   ├── samtools_qc.plot-quals2.png
        │   ├── samtools_qc.plot-quals3.png
        │   └── samtools_qc.stats
        └── speciation
            ├── ERR025833_kraken2.tab
            ├── mykrobe_output.json
            └── reference_info.txt

At the same time, SP3 will sync data to persistent storage. When data is available in SP3 S3 storage, the data in SP3 Cloud storage will be deleted to allow more data to run.

Persistent storage (S3 Storage)
-------------------------------

When a run completes, requested output data will be synced to SP3 S3 storage to be kept for long-term. 

The data stored in SP3 S3 Storage is upon agreement and varies across different pipelines. For example, we save following for clockwork pipeline output in persistent storage:

.. code-block:: bash

    └── ERR025833
        ├── cortex
        │   └── cortex.out
        │       └── vcfs
        ├── minos
        │   ├── final.vcf
        │   └── gvcf.fasta
        ├── samtools
        ├── samtools_qc
        │   └── samtools_qc.stats
        └── speciation
            ├── ERR025833_kraken2.tab
            ├── mykrobe_output.json
            └── reference_info.txt