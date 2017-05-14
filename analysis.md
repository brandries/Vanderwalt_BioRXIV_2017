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

### CLC
CLC is a commential **pay-to-use** software, available [here](https://www.qiagenbioinformatics.com/products/clcgenomics-workbench/)
As it utlizes a graphic-user-interface (GUI), no command options can be provided here. 
Assemblies were generated using default parameters and a word size (**k-mer**) of 55.

### IDBA-UD
The following block of code was set up to perform complete assembly of a metagenome using IDBA-UD.

IDBA-UD requires merging of paired end reads using `fq2fa`, and assembly was performed with iterative **k-mer** sizes up to 71. 
The time taken to complete an assembly in real time was also assessed using base bash variables.
```echo "assembly pipeline starting"
echo "starting IDBA-UD"
date
#set variable for assessing wall-time taken for assembly
vstart=$(date +%s) &&

cd /home/andries/assembly_paper/metagenomes/soil/soil_warming/
mkdir ./IDBA-UD                                                  
cd ./IDBA-UD

#merge fastq paired reads for idba-ud assembly
~/Applications/assembly/idba/bin/fq2fa --merge --filter ./*_1.fastq ./*_2.fastq soil_warming_merge.fasta

#assemble using idba-ud, with a maximum k-mer size of 71 
/home/andries/Applications/assembly/idba/bin/idba_ud -o ./ --long_read /home/andries/assembly_paper/metagenomes/soil/soil_warming/soil_warming_merge.fasta --maxk 71 --num_threads 8

echo "IDBA-UD just finished"
echo "it took $(($(date +'%s')-$vstart)) seconds to complete this job" | mail -s "IDBA-UD just finished" andriesvanderwalt@gmail.com
date
```

### MEGAHIT

### metaSPAdes

### MetaVelvet

### Ray Meta

### SPAdes

### Velvet

### Omega

