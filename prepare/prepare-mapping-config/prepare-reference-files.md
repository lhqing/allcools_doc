# Prepare Reference Files

The reference files required for making the MappingConfig file is listed below

## Reference FASTA

I download reference FASTA from the [**UCSC genome browser**](https://hgdownload.soe.ucsc.edu/downloads.html). For mapping, I will keep all the small contigs to make sure all reads mapped properly, but I usually remove them and only focus on the main chromosomes for further analysis.

Another thing is the lambda DNA spike-in as a non-conversion estimation \(we do that\), I usually append the [lambda genome](https://www.ncbi.nlm.nih.gov/nuccore/215104) with the name chrL to my genome FASTA. You can download the chrL from [NCBI](https://www.ncbi.nlm.nih.gov/nuccore/215104) and append that to your genome.

## Bismark Reference

Use bismark to prepare the genome index, see its documentation [here](https://rawgit.com/FelixKrueger/Bismark/master/Docs/Bismark_User_Guide.html#i-running-bismark-genome-preparation). Note that we use bowtie2 for snmC-seq and snmCT-seq \(that's bismark's default also\), and bowtie1 for snm3C-seq \([the same as snm3C-seq paper](https://www.nature.com/articles/s41592-019-0547-z)\).

## Gene Annotation GTF \(mct only\)

For human and mouse, we usually use [GENCODE's latest version](https://www.gencodegenes.org/). But I do not update GTF throughout the same project. \(And the difference between versions probably have little impact on your analysis results.\)

## STAR Reference \(mct only\)

Use STAR to prepare its genome index, see its documentation [here](https://github.com/alexdobin/STAR/blob/master/doc/STARmanual.pdf).



