============
Installation
============

-----------------
0. Pre-requisites
-----------------

fGAP requires several softwares installed before running the command. We provide simple installation guide for each software. The guide was intensely tested in Ubuntu 14.04 LTS (Unfortunately, we do not provide the supports for other platforms including Windows, OS X, or other Linux distributions in this version).

- :ref:`DownloadFGAP`
- :ref:`Blast`
- :ref:`Trinity`
- :ref:`Maker2`
- :ref:`RepeatModeler`
- :ref:`Braker1`
- :ref:`BUSCO`
- :ref:`InterProScan`
- :ref:`pythonModules`

.. _DownloadFGAP:

^^^^^^^^^^^^^
Download fGAP
^^^^^^^^^^^^^

Download fGAP using GitHub ``clone``. Suppose we are installing fGAP in your ``$HOME`` directory, but you are free to change the location. ::

    cd $HOME
    git clone https://github.com/mbnmbn00/fGAP.git

.. _Blast:

^^^^^^^^^^^^^^^^^^^^
BLAST+ installatioon
^^^^^^^^^^^^^^^^^^^^

BLAST+ is used in Maker and BUSCO running. ::

    sudo apt-get install ncbi-blast+

.. _Trinity:

^^^^^^^^^^^^^^^^^^^^
Trinity installation
^^^^^^^^^^^^^^^^^^^^

**Trinity** performs efficient and robust *de novo* reconstruction of transcriptomes from RNA-seq data.

Download and Install Trinity v2.2.0 using github. ::

    cd $HOME/fGAP/tools
    git clone https://github.com/trinityrnaseq/trinityrnaseq.git
    cd trinityrnaseq
    make

.. _Maker2:

^^^^^^^^^^^^^^^^^^^
Maker2 installation
^^^^^^^^^^^^^^^^^^^

Maker2 is an eay-to-use annotation pipeline designed for emerging model organism genomes.

http://www.gmod.org/wiki/MAKER

Install Maker v2.31.8. Please note that you need a proper license to use Maker2 (http://yandell.topaz.genetics.utah.edu/cgi-bin/maker_license.cgi). ::

    # Move to install directory
    cd $HOME/fGAP/tools/

    # Download and unzip maker2 named maker-2.31.8.tgz
    tar -zxvf maker-2.31.8.tgz

    # Install Maker2 pre-requisites
    cd maker/src
    sudo apt-get install libpq-dev
    sudo apt-get install exonerate # version 2.2.0
    perl Build.PL
    sudo ./Build installdeps
    ./Build installexes
    ./Build install

    # Configure RepeatMasker
    # First download repbase manually at http://www.girinst.org/server/RepBase/index.php
    # Then move it to $HOME/fGAP/maker/exe/RepeatMasker/
    tar -zxvf repeatmaskerlibraries-20150807.tar.gz # Or whatever you downloaded
    cd $HOME/fGAP/tools/maker_2.31.8/exe/RepeatMasker/
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
    $HOME/fGAP/maker_2.31.8/exe/RepeatMasker/rmblast/bin

.. _RepeatModeler:

^^^^^^^^^^^^^^^^^^^^^^^^^^
RepeatModeler installation
^^^^^^^^^^^^^^^^^^^^^^^^^^

**RepeatModeler** is a de-novo repeat family identification and modeling package.

http://www.repeatmasker.org/RepeatModeler.html

Install RepeatModeler and its dependencies. ::

    # Check perl version (ensure version > 5.8.8)
    perl -v

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


.. _Braker1:

^^^^^^^^^^^^^^^^^^^^
Braker1 installation
^^^^^^^^^^^^^^^^^^^^

**Braker1** is an unsupervised RNA-Seq-based genome annotation with GeneMark-ET and AUGUSTUS.

http://exon.gatech.edu/genemark/braker1.html

Install Braker1 and its dependencies. ::

    # Copy gm_key
    cp $HOME/fGAP/tools/gm_et_linux_64/gm_key ~/.gm_key

    # Perl modules
    sudo cpan YAML
    sudo cpan App::cpanminus
    sudo cpanm File::Spec::Functions
    sudo cpanm Hash::Merge
    sudo cpanm List::Util
    sudo cpanm Logger::Simple
    sudo cpanm Module::Load::Conditional
    sudo cpanm Parallel::ForkManager
    sudo cpanm POSIX
    sudo cpanm Scalar::Util::Numeric
    sudo cpanm YAML

    # For bamtools
    sudo apt-get install zlib1g-dev

.. _InterProScan:

^^^^^^^^^^^^^^^^^^^^^^^^^
InterProScan installation
^^^^^^^^^^^^^^^^^^^^^^^^^

**InterProScan** scans a sequence for matches against the InterPro protein signature databases.

https://github.com/ebi-pf-team/interproscan/wiki

Install InterProScan. ::

    cd $HOME/fGAP/tools/
    wget ftp://ftp.ebi.ac.uk/pub/software/unix/iprscan/5/5.18-57.0/interproscan-5.18-57.0-64-bit.tar.gz
    tar -zxvf interproscan-5.18-57.0-64-bit.tar.gz

.. _pythonModules:

^^^^^^^^^^^^^^^^^^^^^^
Install Python modules
^^^^^^^^^^^^^^^^^^^^^^

fGAP requires several python modules and they can be installed by *pip*. ::

    # Install pip
    sudo apt-get install python-pip

    # Install needed modules
    sudo pip install biopython
    sudo pip install numpy
    sudo pip install intervaltree

.. _checkDependencies:

You can check if fGAP is correctly installed.

    python $HOME/fGAP/check_dependencies.py -o tmp



