.. include:: /_static/substitutions.txt 

.. _problem-set-8:

***************
 Problem Set 8
***************

:Due date: |pset8-due| 

Overview
--------
For this quiz you will write programs in Python to analyze data. 

Problem 1 (functions)
---------------------

Write a Python function to parse records from a BED file. Then use the
function to parse the BED file. Add an option to ignore specific
chromosomes. The function should look something like:

.. code:: python

    def parse_bed(filename, ignore=[]):
        ''' Documentation '''        
        ...
        # ignore specified chroms here
        ...

        yield fields

    # ignore chr1 in this code
    for region in parse_bed(filename, ...):
        ...

1. Document your function using the Google [Style]_ (**10 points**).

2. Parse the ``lamina.bed`` file, find the following for each of the
   odd-numbered and even-numbered chromosomes:

   a. Largest region on each (**5 points**)
   b. Mean region size on each using ``numpy`` (**5 points**).

Problem 2 (data structures)
---------------------------

Load data from ``lamina.bed`` using your new ``parse_bed()`` function
iunto the following data structures (**15 points**):

1. ``defaultdict(list)`` with counts of region sizes on each chromosome. 

2. ``defaultdict(set)`` with counts of region sizes on each chromosome. 

What is the key difference between the two structures?

Use these two structures to identify unique region sizes and regions sizes
that are observed more than once (**10 points**).

.. [Style] http://sphinxcontrib-napoleon.readthedocs.org/en/latest/index.html

Problem Set Submission
----------------------
Submit your problem set as a tar file to Canvas
(:ref:`problem-set-submission`).

.. raw:: pdf

    PageBreak
