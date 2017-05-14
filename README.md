# Vanderwalt_BioRXIV_2017
This is the repository for the manuscript "Assembling Metagenomes, one community at a time" submitted to BioRXIV

### Background
The field of Microbial Ecology has rapidly evolved in the past 50 year. Shotgun metagenomic sequencing has allowed unprecedented access to uncultured environmental microorganisms. Within metagenomic post processing, assembly of metagenomic sequences is essential for gene prediction and annotation, and enables the assembly of draft genomes of dominant taxa. However, there is currently no strict standard for the assembly of metagenomic sequence data. 

### Methods
To assist with selection of an appropriate metagenome assembler we evaluated the capabilities of nine prominent assembly tools on nine publicly-available environmental metagenomes and three synthetic metagenomes. Eight of the assessed assemblers utilize de Bruijn graphs, whereas one (Omega) uses a graph overlapping method. We assessed each assembler using default parameters, and if possible allowed each assembler to self optimize the k-mer parameter. 
Assembly quality was evaluated using METAQuast for *N50*, assembly span, number of contigs and longest contig. In addition we assessed run time and memory requirements for each of the tools. 

### Results
Overall, we found that SPAdes provided the largest contigs and highest N50 values across 6 of the 9 environmental datasets, followed by MEGAHIT and metaSPAdes. MEGAHIT emerged as a computationally inexpensive alternative to SPAdes, assembling the most complex dataset using less than 500 GB of RAM and within 10 hours.

### Conclusions
Nevertheless, we found that assembler choice primarily hinges on the scientific question at hand, the resources available and the bioinformatic competence of the researcher. 


# ***Please not that this REPO is still under construction and will be updated as soon as possible***
