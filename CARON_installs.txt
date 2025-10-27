#!/bin/bash

echo "----------Installation des packages nécessaires----------"
conda install -c bioconda unzip trimmomatic star samtools subread
conda activate

echo "----------Création du dossier index pour l'indexation du génome----------"
mkdir index

echo "----------Téléchargement du génome du chromosome 18----------"
wget http://hgdownload.soe.ucsc.edu/goldenPath/hg19/chromosomes/chr18.fa.gz -O chr18.fa.gz
echo "----------Décompression du fichier génome----------"
gunzip chr18.fa.gz

echo "----------Téléchargement de l'annotation Gencode----------"
wget ftp://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_24/GRCh37_mapping/gencode.v24lift37.basic.annotation.gtf.gz -O annotation.gtf.gz
echo "----------Décompression de l'annotation Gencode----------"
gunzip annotation.gtf.gz

echo "----------Indexation du génome avec STAR----------"
STAR --runMode genomeGenerate   --runThreadN 8   --genomeDir ./index   --genomeFastaFiles chr18.fa   --sjdbGTFfile annotation.gtf

echo "----------Indexation terminée, lancer le fichier Caron_pipeline pour continuer l'analyse----------"
