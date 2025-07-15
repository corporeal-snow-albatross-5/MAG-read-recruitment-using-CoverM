# MAG-read-recruitment-using-CoverM
CoverM is purpose-built for mapping reads to MAGs and calculating per-MAG coverage and relative abundance. 

### This tutorial assumes you’ve already made MAGs. 
### Updated 7-14-25

## Step 1: Install CoverM v0.7.0 using conda 
```
#Install CoverM using conda 
#This will install coverM v and dependencies like  minimap2, samtools
conda create -n coverm_env -c bioconda -c conda-forge coverm
conda activate coverm_env

```

## Step 2: Run CoverM
``` 
#Make sure your raw, trimmed reads and bins are in the same directory, then cd into that directory
#Make sure your MAGs have the extension .fna or coverM won’t recognize them

# I have two sets of MAGs to run, one set from Sequence 3, and one set from Sequence 4

#Seq 3
#default mapper: minimap2-sr

coverm genome \
  --interleaved Sequence3.inter.fastq \
  --genome-fasta-directory Seq3_MAGs/ \
  --output-file seq3_MAGs_sample_coverage.tsv \
  --threads 4 \
  --min-read-percent-identity 95 \
  --min-read-aligned-percent 75 \
  --min-covered-fraction 0 \
  --methods relative_abundance covered_bases length count reads_per_base rpkm tpm mean trimmed_mean

#Seq 4
#default mapper: minimap2-sr

coverm genome \
  --interleaved Sequence4.inter.fastq \
  --genome-fasta-directory Seq4_MAGs/ \
  --output-file seq4_MAGs_sample_coverage.tsv \
  --threads 4 \
  --min-read-percent-identity 95 \
  --min-read-aligned-percent 75 \
  --min-covered-fraction 0 \
  --methods relative_abundance covered_bases length count reads_per_base rpkm tpm mean trimmed_mean

```


## Step 3: Explore the output
```
You’ll get a file like sample_coverage.tsv with one row per MAG, and columns like:
```
genome	relative_abundance	coverage
MAG1	0.1234	        15.6
MAG2	0.0000	        0.0
...
```
