============
Installation
============

-----------------
0. Pre-requisites
-----------------

fGAP requires several softwares installed before running the command. We provide simple installation guide for each software. The guide was intensely tested in Ubuntu 14.04 LTS (Unfortunately, we do not provide the supports for other platforms including Windows, OS X, or other Linux distributions in this version).

- :ref:`BeforeWeStart`
- :ref:`Hisat2`
- Trinity
- RepeatModeller
- Maker2
- Braker1
- Augustus
- BUSCO
- InterProScan
- BLAST


.. _BeforeWeStart:

^^^^^^^^^^^^^^^
Before we start
^^^^^^^^^^^^^^^

We will install all dependencies at $HOME/fgap/tools, so create the directory first. ::

    cd $HOME
    mkdir fGAP
    cd fGAP
    mkdir tools

.. _Hisat2:

^^^^^^^^^^^^^^^^^^^
Hisat2 installation
^^^^^^^^^^^^^^^^^^^

*Hisat2* is an alignment program for mapping next-generation sequencing reads  to a population of human genomes (as well as against a single reference genome)

http://ccb.jhu.edu/software/hisat2/index.shtml

Install Hisat2 using github ::

    cd $HOME/fGAP/tools
    git clone https://github.com/infphilo/hisat2.git
    cd hisat2
    make

    # Edit ~/.bashrc
    vim ~/.bashrc
    # Add following line
    export PATH=$PATH:$HOME/fGAP/hisat2
    # Save and exit, and apply the change
    source ~/.bashrc

    # Check installation
    which hisat2

---------------
1. Install fGAP
---------------