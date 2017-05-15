# Analysis

### Download datasets
First you will have to download the files needed for the assemblies. 

#### MG-RAST
Files downloaded from MG-RAST were downloaded using the following code:

```curl -X GET --url "http://api.metagenomics.anl.gov/1/download/mgm4497389.3?file=050.1" > forest_metagenome_1.fastq```

Where `4497389.3` represents the accesion number and `forest_metagenome_1.fastq` the filename in your system

#### NCBI Sequence Read Archive 
Files downloaded from the NCBI SRA were downloaded using the following code:

```wget ftp://ftp-trace.ncbi.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR527/SRR5275893/SRR5275893.sra```

Where `SRR5275893` represents the accession number.

Next after downloading all the `.sra` files, they are converted into `.fastq` files. You require the 
[SRA Toolkit](https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=software) 
on your server for this.

```for FILE in ./*.sra; do fastq-dump --split-files $FILE; done```

### Perform quality control on datasets
Quality control was performed using [Prinseq-lite](https://sourceforge.net/projects/prinseq/).
All reads with a mean phred score < 20 and which contains any ambigious bases (Ns) were removed.

`prinseq-lite -verbose -fastq ./*.fastq -fastq2 ./*.fastq -min_qual_mean 20 -ns_max_n 0`

## Assessment of each assembler

The scripts used to assemble each of the datasets with all nine assemblers can be found in the assemblers.md file
