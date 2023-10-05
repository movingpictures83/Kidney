# Kraken2 analysis of Ji In data

## Step 1 - Install Kraken and Braken

In this analysis we will use:

* <a href="https://ccb.jhu.edu/software/kraken2/">Kraken2</a> tool for taxonomic classification
* <a href="https://ccb.jhu.edu/software/bracken/"> Braken </a> tool for estimation of relative abundance

The following scripts were executed in Castalia machine.

First, we need to download Kraken2

    git clone https://github.com/DerrickWood/kraken2
    git clone https://github.com/jenniferlu717/Bracken
    
Than, we go to the downloaded folder and compile Kraken2 and Braken

    ./install_kraken2.sh ../../kraken2
    ./install_braken.sh
    
Next, we need to build Kraken2 reference databases. We will try two databases: 
* bacteria: RefSeq complete bacterial genomes/proteins
* RDP (Kraken 2 database name: rdp), using the bacterial and archaeal 16S data.

To build databases run the following:

    ./krakenBuildDB.sh
   
The time to build the database

    Database construction complete. [Total: 1h7m42.980s]

## Step 2 - Data preprocessing

File config.sh contains all static variables such as paths and parameters.

For convenience, we moved all the fastq foler into one place, such that samples folder contains:

    ckd_1  ckd_2  ckd_3  ckd_4  ckd_5  donor
    
    
Since Data is compressed, we need to expand it. Run the following to expand the samples:

    ./expand_all.sh
    
    
## Step 3 - Analyzing with Kraken2

To get the taxonomic classification with kraken2 and get abundance estimation with Braken, run the following:

    ./runKrakenBacterial.sh
    
To run bacterial database, comment lines 5-6, and uncomment 8-9, and vica-versa for RDP database.