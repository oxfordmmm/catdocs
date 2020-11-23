Pipelines
=========

Overview
--------

+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| Pipeline                |     Species                            |       Features and Repo                           |      Author      |
+=========================+========================================+===================================================+==================+
| Clockwork combined      |    TB + NTM                            |    - Speciation (Kraken2 + Mykrobe)               |   Denis & Fan    |
|                         |                                        |    - Clockwork (for TB)                           |                  |
|                         |                                        |    - Drug Resistance on Clockwork VCF             |                  |
|                         |                                        |    - TB Neighbourhood and Phylogeny Trees         |                  |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| Clockwork VC            |    TB                                  |    https://github.com/iqbal-lab-org/clockwork     |   Martin Hunt    |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| Oxford CompassCompact   |    TB + NTM                            |    https://github.com/oxfordmmm/CompassCompact    |    Yifei & Fan   |
|                         |                                        |                                                   |                  |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| APHA BTB                |    Bovine TB                           |   https://github.com/oxfordmmm/BovTB-nf-docker    |  Richard & Fan   |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+
| Oxford Bug Flow         |    Bacteria                            |   https://github.com/davideyre/bug-flow           |    David Eyre    |
+-------------------------+----------------------------------------+---------------------------------------------------+------------------+


TB Pipelines
------------

+--------------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|pipleine      |input     |kraken2   |removecontam|mykrobe   |auto pick |trim      |bwa map   |samtool   | samtoolqc |  cortex  |  minos   |  fasta     |resistance|
|              |          |          |            |          |reference |          |          |mpileup   |           |          |          |            |          |
|              |          |          |            |          |          |          |          |          |           |          |          |            |          |
+==============+==========+==========+============+==========+==========+==========+==========+==========+===========+==========+==========+============+==========+
|catbug        |fastq/bam |Y         |Y           |Y         |Y         |Y         |Y         |Y         |Y          |Y         |Y         |Y           |Y         |
|tb            |          |          |            |          |          |          |          |          |           |          |          |            |          |
+--------------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|catbug        |fastq/bam |Y         |Y           |Y         |Y         |Y         |Y         |Y         |Y          |          |          |Y           |          |
|non-tb        |          |          |            |          |          |          |          |          |           |          |          |            |          |
+--------------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|clockwork     |fastq/bam |Y         |Y           |Y         |Y         |Y         |Y         |Y         |Y          |Y         |Y         |Y           |Y         |
|tb            |          |          |            |          |          |          |          |          |           |          |          |            |          |
+--------------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|CompassCompact|fastq/bam |          |            |          |          |          |Y         |Y         |Y          |          |          |Y           |          |
|              |          |          |            |          |          |          |          |          |           |          |          |            |          |
+--------------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+
|Clockwork VC  |fastq     |          |            |          |          |Y         |Y         |Y         |Y          |Y         |Y         |            |          |
|              |          |          |            |          |          |          |          |          |           |          |          |            |          |
+--------------+----------+----------+------------+----------+----------+----------+----------+----------+-----------+----------+----------+------------+----------+

TB Neighbourhood (alpha release)
--------------------------------

For clockwork TB pipeline, we have a service built for examining genetic neighbourhood based on SNP distance. 

To see genetic related samples, a sample would have been through following processes:

1. The sample has been succesfully run in **clockwork** pipeline.
2. The sample has been identified by mykrobe as **mycobacterium tuberculosis**.
3. The sample has been succesfully mapped to reference **NC_000962.3**.
4. The sample has been archived to Sp3 persistence storage. (This is currently done manually.)
5. The sample has been pushed to TB neighbourhood service, catwalk. (This is currently done manually.)

With alpha release, you would not see neighbourhood right after the run as the step 4 and step 5 would be run manually at the moment. The step 4 and step 5 would be done at the end of the day or end of the week, so please check it later.

If you have a sample that has been through all the above processes, here is how to see the genetic neighbours.


**Step 1**. Click the sample name to view SP3 report, from a complete run, eg. click **ERR552831** as shown below.

.. image:: _static/neighbour11.png

**Step 2**. Click link "Query genetic neighbourhood" at the top of the SP3 report below the sample name.

.. image:: _static/neighbour22.png

**Step 3**. Genetic neighbourhood page would show you the result. In the example below, there were **17** neighbours found shown in a neighbourhood table.

Among all 17 genetic related samples, there are 8 samples run from **EBI Cats** site and the rest from **Cats** site (staging/test site).

The run name of the neighour samples (with a prefix of organisation) gives a hint on the source of the neighbours, the organisation, such as PHS, PHW, OAHPP etc.

And the sample names of the neighbours are also shown at the 3rd column of the table.

The last column of the neightbour table is the SNP distance, to the query sample. You might notice, in this case, SNP distances are all shown as Zero. This is because the same sample has been run in all different organisations.

.. image:: _static/neighbour33.png

You can also query genetic neighbours ad-hoc in an interactive way, go to "clockwork" pipeline and click "View TB Neighbourhood"

.. image:: _static/viewTB.png
   :align: center   
   :height: 80pt

Follow the hint, use a run id and a sample name and set a SNP distance for the query.

.. image:: _static/neighbour.png 
        
TB Phylogeny (alpha release)
----------------------------

For TB Neighbourhood, we build phylogeny trees for the nearest neighbourhood of TB samples.

To create a tree for your sample and its neighbours: 

**Step 1**. Query neighbours
At SP3 sample report page, click 'Query genetic neighbourhood'.

.. image:: _static/tree1.png
        :align: center   
        :height: 120pt

**Step 2**. Select and generate

Select the samples among the neighbours, and build the tree.

You can adjust SNP distance, and select all or some of the neighbours to build trees.

.. image:: _static/tree2.png

**Step 3**. Confirm and name the tree

Confirm your selection, and provide a name for your tree for later reference. Then click the button to generate the tree.

.. image:: _static/tree3.png

**Step 4**. Monitor the queue

The tree buildling could be compute intensive and it could take a while. 

After tree building job is submitted, you would be able to see your tree job is queued to compute.

.. image:: _static/tree4.png

You can refresh the page every so often, until it completes. It could be seconds, or minutes or hours depending on the amount of the nodes.

.. image:: _static/tree5.png

**Step 5**. View the tree

When completed, the tree can be viewed in a page. (This uses phylocanvas, so javascript needs to be allowed in the browser.)

.. image:: _static/tree6.png

In this page, one or more nodes can be highlighted, given a search text in the node label.

.. image:: _static/tree7.png

You can use more features of Phylocanvas, by right click on the tree, such as:

    - Export leave labels, newick file and tree image
    - Show or hide labels
    - Align/Realign labels

.. image:: _static/tree7canvas.png

You can also zoom or pan the image or click on node to highlight or clear the highlight.

If you like to see trees built by other users, please click "Tree" at top menu. There are quite a lot already! 

.. image:: _static/tree8.png
