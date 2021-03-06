
.. include:: /_static/substitutions.txt

=============================
Class 25 : Getting Data and Asking for Help 
=============================

:Last updated: |today|

Final Class
-----------

#. Problem set 5

#. Office Hours for help with final projects and problem set(s)

#. Optional Class going on shell scripts to run RNA-Seq and Chip-Seq Next
   Tuesday 1-3pm here. 

#. Final Project presentations 

   <5 min 
   
   3 slides (problem, some awesome code, and conclusion/plots)
   
   Date: May 2 from 1-3pm
   
   Place: RC1 South 9th floor
   
   Push code to github repository

Goals for today
---------------
#. Where and how to download public data.  
#. How to visualize your data.
#. How to ask for help and point out bugs in software.

Downloading Sequencing Data
----------------
Most journals require that raw sequencing data be deposited to public
databases. 

#. Researchers in the US usually deposit data in the Short Read
   Achive (`SRA <https://www.ncbi.nlm.nih.gov/sra>`_) hosted by the NCBI. 

#. European groups, usually deposit data in `Array Express <https://www.ebi.ac.uk/arrayexpress/>`_ hosted by EMBL.

#. Project Specific downloads: 
   
   The Cancer Genome Atlas (`TCGA <https://portal.gdc.cancer.gov/>`_)
   
   `ENCODE <https://www.encodeproject.org/matrix/?type=Experiment>`_
   
   `1000 Genomes Project <http://www.internationalgenome.org/data/>`_
 

Getting data from the SRA
=========================

#. Find specific experiments in the `Gene Expression Omnibus
   <https://www.ncbi.nlm.nih.gov/gds>`_ from GEO Datasets. 

#. Downloading "processed" experiment data. ``BED``, ``Bedgraph``, ``count
   tables``, ``bigWig``, etc.

#. Extract the SRA accession numbers and download raw data from the `SRA GUI
   <https://trace.ncbi.nlm.nih.gov/Traces/sra/>`_ 

#.  Use ``fastq-dump`` on command line. 

fastq-dump
==========

The  `SRAToolKit
<https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=toolkit_doc&f=std>`_
has command-line utilities to allow for programmatic access to sequencing
data. The ``fastq-dump`` command is useful for directly downloading fastq
data, provided a SRA accession number. 

.. code-block:: bash
  
  ~/path_to_sratoolkit/bin/fastq-dump -h
  # -X download only a specific number of records

  fastq-dump -X 10 --gzip SRR390728

Download in a loop
==================

Use SRA website to get a list of SRA accesion number for a project. Then
download all of the data as fastq data. 

.. code-block:: bash
  
  files=$(cat sranumbers.txt)

  for x in $files
    do
    echo "downloading "$x
    fastq-dump -X 10 --gzip $x
    done

Download in parallel 
====================
`GNU parallel <https://www.gnu.org/software/parallel/>`_  is a powerful unix tool 
for parallelizing jobs if you don't have access to a compute cluster. 


.. code-block:: bash
  
  #same output as previous for loop
  # -j indicates number of jobs to run at once

  cat sranumbers.txt \
    | parallel -j 4 `fastq-dump -X 10 {}`

Downloading Annotations
-----------------------

#. UCSC `table browser <http://genome.ucsc.edu/>`_ is an interactive
   GUI useful for downloading a variety of genomics data

#. Ensembl `BioMart <http://www.ensembl.org/index.html>`_ is similar to
   the table browser, with some unique annotations. 

#. `Gencode <http://www.gencodegenes.org/>`_ annotations used by Encode


Visualizing your data
---------------------

Always, always, always look at your data.

#. Integrative Genomics Viewer (`IGV <http://software.broadinstitute.org/software/igv/download>`_)

#. UCSC genome browser (http://genome.ucsc.edu/)
   

Getting help 
------------

Sometimes you will get errors that you do not understand. 

#. First google it. Quote the error message and include the package name
   or language. If there are variables or files included in the message exclude them from
   the search. 

#. Go to the source code repository and search for your problem (i.e. github
   issues, google groups/mailing list)

#. Before you ask others for help, make sure the question hasn't been
   answered before. 
 
`StackOverflow <www.stackoverflow.com>`_

`Biostars <www.biostars.com>`_

`SeqAnswers <www.seqanswers.com>`_

`Bioconductor <www.bioconductor.com>`_

Hopefully not your experience
-----------------------------

.. image:: https://imgs.xkcd.com/comics/wisdom_of_the_ancients.png

There will be bugs
------------------

#. Bioinformatics relies on software built by people and people make
   mistakes.  There is a lot of bad code out there. 

#. There will be bugs and most tools won't do everything you wish they would. 

#. Solutions: 
   
   get developers to fix the bug

   fix the bug yourself and contribute to the project
   
   use another tool 
   
   write your own tool 


Reproducible Example (reprex)
-----------------------------

#. Writing a reproducible example is a key skill to getting any help from
   the internet.
#. Keep it simple and distill your problem down to a small set of code the reproduces your
   error. 

#. The error should be recaptitulated by copying and running the code as
   is. Do not depend on external data if possible

#. Often by trying to simplify and reproduce your error you will actually
   solve your problem. 

What makes a good reprex?
-------------------------

#. load necessary package at top 
#. use built-in datasets if possible, otherwise use ``dput()``, or
   ``tibble::frame_data()``
#. Use comments to explain steps
#. Include relevant error message
#. Potentially include the output of ``sessionInfo()``

The reprex package
------------------

The `reprex package <http://jennybc.github.io/reprex/>`_ makes it easy to
produce well-formatted R reprexes for posting to github or stackoverflow. 

.. code-block:: R
  
  install.packages("reprex")
  library(reprex)

copy the following code into your clipboard

.. code-block:: R
  
  a <- c("1", "1.2")
  mean(a)

Now in the console type:

.. code-block:: R
  
  reprex()

Gists
-----
If the code is long, or if you want to share your code in private use
`github gist <https://gist.github.com/>`_. 

Avoid putting code directly in email messages, as often the format will get mangled. 



Additional Resources
--------------------

Books

#. Advanced R and R for Data Science by Hadley Wickham et al. 

#. Bioinformatics Data Skills by Vince Buffalo

#. Python for Biologists


