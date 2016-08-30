.. _usage:

=====
Usage
=====

---------------------------
1. Prepare protein database
---------------------------

fGAP requires protein database in FASTA file. We recommend 3 ~ 4 organisms' proteome to save running time. For this, we provide script to build database using NCBI API.

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

All taxon levels are allowed for *--taxon* argument, but Genus is appropriate. Now make protein database.::

    cd sister_orgs
    gunzip *.faa.gz
    cat ./*faa > prot_db.faa

You can put **prot_db.faa** to fGAP. 

-----------
2. Run fGAP
-----------

---------
3. Output
---------