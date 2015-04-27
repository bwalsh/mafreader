MAFReader Quickstart
=================

MAFReader is a simple command line tool that reads a `MAF <https://wiki.nci.nih.gov/display/TCGA/Mutation+Annotation+Format+%28MAF%29+Specification>`_ file, calls `CIViC <https://civic.genome.wustl.edu>`_ for each line therein.

MAFReader outputs a table in `markdown <https://help.github.com/articles/github-flavored-markdown/#tables>`_ format for easy inclusion into downstream reports

MAFReader requires Python 3.*. To check your python version, run:

```
    $ python -V
    Python 3.4.2
```

Usage:

```

    $ python MAFReader.py -h
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
```

Process
========
On entry MAFReader reads all variants from CIViC for a particular gene, using entrez_id as the gene identifier.
* If there is no data returned from CIViC, MAFReader displays _gene not found in civic_  and moves on.
* If there is data returned from CIViC, MAFReader searches the CIViC _EvidenceItems_ returned and matches on 
{Chromosome}:{Start_position}-{End_position} ({Reference_Allele}->{Tumor_Seq_Allele1})
  * If there is a match MAFReader displays _[civic variant]_ with a link to the specific variant in CIViC
  * Otherwise MAFReader displays  _[civic gene]_ with a link to the gene in CIViC





Output
=============

| hugo_symbol  | entrez_gene_id  | variant  | drugs  | link  |
|---  |---  |---  |---  |---  |
| -  | 207  | E17K  |   | [civic variant](http://civic.genome.wustl.edu/#/events/genes/207/summary/variants/8/summary)  |
| -  | 7157  | R175H  |   | [civic gene](http://civic.genome.wustl.edu/#/events/genes/7157/summary)  |



Customization
=============
For local CIViC deployments use the -c option "-c locahost:3000"

Issues
======

* MAFReader calls CIViC for each variant in the MAF file.  An optimization would be to modify CIViC to accept a batch of entrez_ids to match on.

* MAFReader does not cache any reponses from CIViC.  An optimization would be for MAFReader to cache responses and leverage the ETag header CIViC provides.

* MAFReader does not populate CIViC with any information if it encounters a "no find".  

