============
Installation
============

-----------------
0. Pre-requisites
-----------------

fGAP requires several softwares installed before running the command. We provide simple installation guide for each software. The guide was intensely tested in Ubuntu 14.04 LTS (Unfortunately, we do not provide the supports for other platforms including Windows, OS X, or other Linux distributions in this version).

- :ref:`BeforeWeStart`
- :ref:`Hisat2`
- :ref:`Trinity`
- :ref:`Maker2`
- :ref:`RepeatModeler`
- Braker1
- Augustus
- BUSCO
- InterProScan
- BLAST
- Python modules


.. _BeforeWeStart:

^^^^^^^^^^^^^^^
Before we start
^^^^^^^^^^^^^^^

We will install all dependencies at ``$HOME/fgap/tools``, so create the directory first. ::

    cd $HOME
    mkdir -p fGAP/tools

.. _Hisat2:

^^^^^^^^^^^^^^^^^^^
Hisat2 installation
^^^^^^^^^^^^^^^^^^^

**Hisat2** is an alignment program for mapping next-generation sequencing reads  to a reference genome.

http://ccb.jhu.edu/software/hisat2/index.shtml

Install Hisat2 version 2.0.2-beta using github ::

    cd $HOME/fGAP/tools
    git clone https://github.com/infphilo/hisat2.git
    cd hisat2
    make

    # Edit ~/.bashrc
    vim ~/.bashrc
    # Add following line
    export PATH=$PATH:$HOME/fGAP/tools/hisat2
    # Save, exit, and apply the change
    source ~/.bashrc

    # Check installation
    which hisat2

.. _Trinity:

^^^^^^^^^^^^^^^^^^^^
Trinity installation
^^^^^^^^^^^^^^^^^^^^

**Trinity** performs efficient and robust *de novo* reconstruction of transcriptomes from RNA-seq data.

Install Trinity v2.2.0 using github ::

    cd $HOME/fGAP/tools
    git clone https://github.com/trinityrnaseq/trinityrnaseq.git
    cd trinityrnaseq
    make

    # Edit ~/.bashrc
    vim ~/.bashrc
    # Add following line
    export PATH=$PATH:$HOME/fGAP/trinityrnaseq
    # Save, exit, and apply the change
    source ~/.bashrc

    # Check installation
    which Trinity

.. _Maker:

^^^^^^^^^^^^^^^^^^^
Maker2 installation
^^^^^^^^^^^^^^^^^^^

Maker2 is an eay-to-use annotation pipeline designed for emerging model organism genomes.

http://www.gmod.org/wiki/MAKER

Install Maker v2.31.8. Please note that you need the proper license to use Maker2 (http://yandell.topaz.genetics.utah.edu/cgi-bin/maker_license.cgi). ::

    # Move to install directory
    cd $HOME/fGAP/tools/

    # Download and unzip maker2
    wget http://yandell.topaz.genetics.utah.edu/maker_downloads/5456/CA4F/CED4/052811E9418D53F8B67DDE88D5E2/maker-2.31.8.tgz # Use your own download
    tar -zxvf maker-2.31.8.tgz

    # Install Maker2 pre-requisites
    cd maker/src
    sudo apt-get install libpq-dev
    sudo apt-get install exonerate # version 2.2.0
    perl Build.PL
    sudo ./Build installdeps
    ./Build installexes
    ./Build install

    # Edit ~/.bashrc
    vim ~/.bashrc
    # Add following lines
    export PATH=$PATH:$HOME/fGAP/tools/maker/bin
    export PATH=$PATH:$HOME/fGAP/tools/maker/exe/snap
    # Save, exit, and apply the changes
    source ~/.bashrc
    # Check installation
    which maker

    # Configure RepeatMasker
    # First download repbase manually at http://www.girinst.org/server/RepBase/index.php
    # And move it to $HOME/fGAP/maker/exe/RepeatMasker/
    tar -zxvf repeatmaskerlibraries-20150807.tar.gz # Or whatever you downloaded
    cd $HOME/fGAP/tools/exe/RepeatMasker/
    ./configure

    # **TRF PROGRAM**
    # This is the full path to the TRF program.
    # This is now used by RepeatMasker to mask simple repeats.
    # Enter path [  ]:
    $HOME/fGAP/maker/exe/RepeatMasker/trf

    # Add a Search Engine:
    # 1. CrossMatch: [ Un-configured ]
    # 2. RMBlast - NCBI Blast with RepeatMasker extensions: [ Un-configured ]
    # 3. WUBlast/ABBlast (required by DupMasker): [ Un-configured ]
    # 4. HMMER3.1 & DFAM: [ Un-configured ]

    # 5. Done
    # Enter Selection:
    2

    # **RMBlast (rmblastn) INSTALLATION PATH**
    # This is the path to the location where
    # the rmblastn and makeblastdb programs can be found.
    # Enter path [  ]:
    $HOME/fGAP/maker/exe/RepeatMasker/rmblast/bin

.. _RepeatModeler:

^^^^^^^^^^^^^^^^^^^^^^^^^^
RepeatModeler installation
^^^^^^^^^^^^^^^^^^^^^^^^^^

**RepeatModeler** is a de-novo repeat family identification and modeling package.

http://www.repeatmasker.org/RepeatModeler.html

Install RepeatModeler and its dependencies ::

    # Check perl version (ensure version > 5.8.8)
    perl -v

    # RECON - De Novo Repeat Finder 
    cd $HOME/fGAP/tools/
    wget http://www.repeatmasker.org/RECON-1.08.tar.gz
    tar -zxvf RECON-1.08.tar.gz
    cd RECON-1.08/src/
    make
    make install

    # RepeatScout - De Novo Repeat Finder
    cd $HOME/fGAP/tools/
    wget http://repeatscout.bioprojects.org/RepeatScout-1.0.5.tar.gz
    tar -zxvf RepeatScout-1.0.5.tar.gz
    cd RepeatScout-1
    make

    # Now install RepeatModeler
    cd $HOME/fGAP/tools/
    wget http://www.repeatmasker.org/RepeatModeler-open-1-0-8.tar.gz
    tar -zxvf RepeatModeler-open-1-0-8.tar.gz
    cd RepeatModeler/
    perl ./configure

    # **REPEATMASKER INSTALLATION PATH**
    # This is the path to the location where
    # the RepeatMasker program suite can be found.
    # Enter path [  ]:
    $HOME/fGAP/maker/exe/RepeatMasker/

    # **RECON INSTALLATION PATH**
    # This is the path to the location where
    # the RECON program suite can be found.
    # Enter path [  ]:
    $HOME/fGAP/tools/RECON-1.08/bin

    # **RepeatScout INSTALLATION PATH**
    # This is the path to the location where
    # the RepeatScout program suite can be found.
    # Enter path [  ]:
    $HOME/fGAP/tools/RepeatScout-1/

    # **TRF INSTALLATION PATH**
    # This is the path to the location where
    # the TRF program can be found.
    # Enter path [  ]:
    $HOME/fGAP/maker/exe/RepeatMasker

    # Add a Search Engine:
    # 1. RMBlast - NCBI Blast with RepeatMasker extensions: [ Un-configured ]
    # 2. WUBlast/ABBlast: [ Un-configured ]

    # 3. Done
    # Enter Selection:
    1

    # **RMBlast (rmblastn) INSTALLATION PATH**
    # This is the path to the location where
    # the rmblastn and makeblastdb programs can be found.
    # Enter path [  ]:
    $HOME/fGAP/maker/exe/RepeatMasker/rmblast/bin

    # Edit ~/.bashrc
    vim ~/.bashrc
    # Add following line
    export PATH=$PATH:$HOME/fGAP/tools/RepeatModeler
    # Save, exit, and apply the change
    source ~/.bashrc

    # Check installation
    which RepeatModeler

.. _Braker1:

^^^^^^^^^^^^^^^^^^^^
Braker1 installation
^^^^^^^^^^^^^^^^^^^^

**Braker1** is an unsupervised RNA-Seq-based genome annotation with GeneMark-ET and AUGUSTUS.

http://exon.gatech.edu/genemark/braker1.html

Install Braker1 and its dependencies. ::

    # GeneMark-ET - You must download manually via web
    # http://exon.gatech.edu/GeneMark/license_download.cgi
    # Downloaded file name should be like *gm_et_linux_64.tar.gz*
    tar -zxvf gm_et_linux_64.tar.gz
    cp gm_et_linux_64 /csbl/tool/ngs/ -r
    vim ~/.bashrc






---------------
1. Install fGAP
---------------