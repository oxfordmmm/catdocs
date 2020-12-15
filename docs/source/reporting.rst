Reporting
=========

Kraken2
-------

Kraken2 is used to classify reads according to their most likely taxonomic clade.

More: `speciation documentation <https://github.com/oxfordmmm/speciation>`_

Kraken2 DB: `MiniKraken2_v2_8GB <https://ccb.jhu.edu/software/kraken2/downloads.shtml>`_ 

Mykrobe Speciation
------------------
Mykrobe is used to further classification if the sample appear to be mycobacterial, or a mixture containing M. tuberculosis reads.

Mykrobe tests for the presence of probe sequences in the reads to determine the species present. 

The “Coverage” is the percent of the probe that has non-zero read depth. “Median depth” is the median read depth across the probe.

See `mykrobe documentation <https://github.com/oxfordmmm/speciation>`_

See `SNP panel for lineage classification <http://tgu.ibv.csic.es/?page_id=1794>`_

Reference
---------
Reference is selected based on mykrobe result. 

There are currently 10 available, with associated RefSeq chromosome IDs as follows:

* Mycobacterium abscessus --> NC_010397.1
* Mycobacterium africanum --> NC_000962.3
* Mycobacterium avium --> NC_002944.2
* Mycobacterium bovis --> NC_002945.4
* Mycobacterium chelonae --> NZ_CP007220.1
* Mycobacterium chimaera --> NZ_CP012885.2
* Mycobacterium fortuitum --> NZ_CP011269.1
* Mycobacterium intracellulare --> NC_016946.1
* Mycobacterium kansasii --> NC_022663.1
* Mycobacterium tuberculosis --> NC_000962.3

Samtools QC
-----------
See `Samtools documentation <http://www.htslib.org/doc/samtools-stats.html>`_

Resistance
----------

Resistance configuration
^^^^^^^^^^^^^^^^^^^^^^^^

Drugs
^^^^^

Mutations
^^^^^^^^^


