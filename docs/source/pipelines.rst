Pipelines
=========

Overview
--------

+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| Pipeline                |     Species                            |       Features                                    |      Author      |
+=========================+========================================+===================================================+==================+
| Catbug                  |    TB + NTM                            |    - Speciation (Kraken2 + Mykrobe)               |  Denis Volk      |
|                         |                                        |    - Clockwork (for TB)                           |                  |
|                         |                                        |    - Compass (for NTM)                            |                  |
|                         |                                        |    - Drug Resistance on Clockwork VCF             |                  |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| Clockwork VC            |    TB                                  |    Trim, Map, Samtools, Cortex, Minos             |   Martin Hunt    |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| Clockwork TB Only       |    TB                                  |    - Speciation (Kraken2 + Mykrobe)               |                  |
|                         |                                        |    - Trim, Map, Samtools, Cortex, Minos           |    Denis Volk    |
|                         |                                        |    - Drug Resistance                              |                  |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| CompassCompact          |    TB + NTM                            |    BWA, Mpileup, AnnotVCF, Basecall               |    Yifei Xu      |
|                         |                                        |                                                   |                  |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| CompassCompact Plus     |    TB + NTM                            |    - Speciation (Kraken2 + Mykrobe)               |     Fan Yang     |
|                         |                                        |    - BWA, Mpileup, AnnotVCF, Basecall             |                  |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| PHE Flu                 |     Description                        |       Repo                                        |       Ulf        |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| APHA BTB                |     Description                        |       Repo                                        |  Richard Ellis   |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| Bug Flow                |     Description                        |       Repo                                        |    David Eyre    |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| Nano Virus Metagenomics |     Description                        |       Repo                                        |     Yifei Xu     |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+

Input and Output
----------------

+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|pipleine  |input     |kraken2   |removecontam|mykrobe   |auto pick |trim      |bwa map   |samtool   | samtoolqc |  cortex  |  minos   |  fasta     |resistance|
|          |          |          |            |          |reference |          |          |mpileup   |           |          |          |            |          |
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
+==========+==========+==========+============+==========+==========+==========+==========+==========+===========+==========+==========+============+==========+
|catbug    |fastq/bam |Y         |Y           |Y         |Y         |Y         |Y         |Y         |Y          |Y         |Y         |Y           |Y         |
|tb        |          |          |            |          |          |          |          |          |           |          |          |            |          |
+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|catbug    |fastq/bam |Y         |Y           |Y         |Y         |Y         |Y         |Y         |Y          |          |          |Y           |          |
|non-bb    |          |          |            |          |          |          |          |          |           |          |          |            |          |
+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|clockwork |fastq/bam |Y         |Y           |Y         |Y         |Y         |Y         |Y         |Y          |Y         |Y         |Y           |Y         |
|tb        |          |          |            |          |          |          |          |          |           |          |          |            |          |
+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
|          |          |          |            |          |          |          |          |          |           |          |          |            |          |
+----------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+