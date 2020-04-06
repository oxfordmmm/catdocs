User Guide
==========

Welcome to use Oxford SP3. Please take a moment to view this user guide and consider the options available to you before you start.

User, group and storage
-----------------------
To use Oxford SP3, a user needs to register an SP3 **account**. The account allows you to log into one of our SP3 cloud platforms for pathogen sequencing data analysis.

When register, we will assign you to a **group**. SP3 uses group to manage data access and privacy. All users of one group can share data and pipelines. This means a user in one group can see all the analysis run by another user in the same group.

A group can be a physical organisation or a virtual organisation. For example, Oxford University can have two groups, one for TB research, one for virus research.

If your group has a cloud **storage**, say a S3 bucket, your sequencing data can be uploaded to that bucket and SP3 can get data from there if you allow us to do so. Only users from your organisation can see your sequencing data.

SP3 can also get data from ENA via study number, project number or sample assession number.


Data submission
---------------
There are three ways to upload sequencing data to SP3. 

1. Upload sequencing data to `ENA <https://www.ebi.ac.uk/ena/submit>`_
2. Upload sequencing data to a SP3 Storage dedicated to an organisation, such as a S3 bucket.
3. Upload sequncing data to SP3 via SFTP link.

The differences of three mechanisms of submission are as follows:

+----------------+---------------------------------------------------+-------------------------+---------------------------------+
|                |            Tools                                  |    Meta-data required   |       Access Control            |
+----------------+---------------------------------------------------+-------------------------+---------------------------------+
| ENA submission | `ENA <https://www.ebi.ac.uk/ena/submit>`_         |           Yes           |  Available to all SP3 users     |
+----------------+---------------------------------------------------+-------------------------+---------------------------------+
| SP3 submission | `Catsup <https://github.com/oxfordmmm/catsup>`_   |           Yes           | Available within organisation   |
+----------------+---------------------------------------------------+-------------------------+---------------------------------+
| FTP submission | SFTP client                                       |           No            |  Available to all SP3 users     |
+----------------+---------------------------------------------------+-------------------------+---------------------------------+

Register an account
-------------------

To register with SP3, please send an email to crookcs.it@ndm.ox.ac.uk with a subject as "**SP3 User Registration**" and provide following information: 

* Your Email
* Your Full Name
* Your organisation
* Your group (if you know)
* Your research summary related to SP3
* How often do you expect to use SP3?
* How many samples do you expect to submit to SP3?
* Which way would you submit your data to SP3? (see below choice)
* Any other information you like us to know.