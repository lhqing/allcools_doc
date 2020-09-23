# 🚧 Prepare Reference Files

The reference files required for making MappingConfig file is listed below

## Reference FASTA

I download reference FASTA from [**UCSC genome browser**](https://hgdownload.soe.ucsc.edu/downloads.html). For mapping, I will keep all the small contigs to make sure all reads mapped properly, but I usually remove them and only focus on main chromosomes for further analysis.

Another thing is the lambda DNA spike-in as a non-conversion estimation \(we do that\), I usually append [lambda genome](https://www.ncbi.nlm.nih.gov/nuccore/215104) with the name chrL to my genome FASTA. You can download the chrL below and append that to your genome.

## Bismark Reference



