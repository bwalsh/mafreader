mafreader Quickstart
=================

mafreader is a simple command line tool that reads a `MAF <https://wiki.nci.nih.gov/display/TCGA/Mutation+Annotation+Format+%28MAF%29+Specification>`_ file, calls `CIViC <https://civic.genome.wustl.edu>`_ for each line therein.

mafreader outputs a table in `markdown <https://help.github.com/articles/github-flavored-markdown/#tables>`_ format for easy inclusion into downstream reports

mafreader requires Python 3.*. To check your python version, run:

.. code:: console

    $ python -V
    Python 3.4.2


Usage:

.. code:: console

    $ python mafreader.py -h
    usage: civic [-h] [-i INPUT_FILE] [-o OUTPUT_FILE] [-c HOST]
                 [-col ENTREZ_ID_COLUMN]

    optional arguments:
      -h, --help            show this help message and exit
      -i INPUT_FILE, --input_file INPUT_FILE
                            input file (assumed to be tab separated MAF format);
                            defaults to stdin
      -o OUTPUT_FILE, --output_file OUTPUT_FILE
                            output file; defaults to stdout
      -c HOST, --host HOST  url of reference civic host (default:
                            civic.genome.wustl.edu)
      -col ENTREZ_ID_COLUMN, --entrez_id_column ENTREZ_ID_COLUMN
                            column in the input file that contains the entrez id.
                            Defaults to 1 (0 based)


Customization
=============
For local CIViC deployments use the -c option "-c locahost:3000"

Output
=======
+------------+------------+-----------+-----------+-----------+
| hugo_symbol  | entrez_gene_id  | variant  | drugs  | link  |
+------------+------------+-----------+-----------+-----------+
| -  | 207  | E17K  |   | [civic variant](http://civic.genome.wustl.edu/#/events/genes/207/summary/variants/8/summary)  |
+------------+------------+-----------+-----------+-----------+
| -  | 7157  | R175H  |   | [civic gene](http://civic.genome.wustl.edu/#/events/genes/7157/summary)  |
+------------+------------+-----------+-----------+-----------+



Issues
======

- mafreader calls CIViC for each variant in the MAF file.  An optimization would be to modify CIViC to accept a batch of entrez_ids to match on.

- mafreader does not cache any reponses from CIViC.  An optimization would be for mafreader to cache responses and leverage the ETag header CIViC provides.

- mafreader does not populate CIViC with any information if it encounters a "no find".  

