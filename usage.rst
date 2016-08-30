.. _usage:

=====
Usage
=====

---------------------------
1. Prepare protein database
---------------------------

fGAP requires protein database in FASTA file. We recommend 3 ~ 4 organisms' proteome to save running time. For this, we provide a script to build your database using NCBI API.

Usage::

    # Assume you downloaded fGAP in $HOME/fGAP
    python $HOME/fGAP/fgap/download_sister_orgs.py\
     --download_dir <download_directory>\
     --taxon <taxon>\
     --num_sisters <number_of_sisters>\
     --email_address <your_email_address>

E-mail address is needed for NCBI Entrez.

Example command::

    python $HOME/fGAP/fgap/download_sister_orgs.py\
     --download_dir sister_orgs\
     --taxon "Schizophyllum"\
     --num_sisters 3\
     --email_address mbnmbn00@gmail.com

All taxon levels are allowed for *--taxon* argument, but genus level is appropriate. Now make protein database::

    cd sister_orgs
    gunzip *.faa.gz
    cat ./*faa > prot_db.faa

You can now input *prot_db.faa* to fGAP. 

-----------
2. Run fGAP
-----------

To run fGAP, you need three main arguments

 - Genome assembly (FASTA)
 - Transcriptomic reads (FASTQ)
 - Protein database (FASTA)

Currently, fgap gets only **Illumina paired-end** reads files. The file names of two paired-end reads should have suffix like 'XX_1.fastq' and 'XX_2.fastq'. The prefixes should be same without '_' character. For example, File names would be like *hyphae_1.fastq* and *hyphae_2.fastq*.

Usage::

    # Assume you downloaded fGAP in $HOME/fGAP
    python $HOME/fGAP/fgap/fgap.py\
     --output_dir <output_directory>\
     --trans_read_files <transcriptome_reads_fastqs>\
     --project_name <project_name_without_space>\
     --genome_assembly <genome_assembly_fasta>\
     --augustus_species <augustus_species>\
     --org_id <organism_id>\
     --sister_proteome <sister_proteome>\
     --num_cores <number_of_cpus_to_be_used>\

- Augustus species: you should provide one augustus_species used in Augustus. This is the list what this software provides.

+------------+----------------+-----------------------+-----------------------+
| Phylum     | Class          | Species               | augustus_species      |
+============+================+=======================+=======================+
| Ascomycota | Eurotiomycetes | Aspergillus fumigatus | aspergillus_fumigatus |
+------------+----------------+-----------------------+-----------------------+
| body row 2 | ...            | ...                   |                       |
+------------+----------------+-----------------------+-----------------------+

---------
3. Output
---------

--------------------
4. Trouble-shootings
--------------------

This is very beta version of software, so please don't hesistate reporting any bug or error you have encountered at mbnmbn00@korea.ac.kr or mbnmbn00@gmail.com.
