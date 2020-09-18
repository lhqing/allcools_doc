# Before Start

## Important Note

{% hint style="warning" %}
YAP is currently an **in-house** pipeline designed for raw sequencing data \(BCL files and raw FASTQ files before demultiplex\) generated [in the Ecker Lab](https://ecker.salk.edu/). In the future, YAP may become more generalizable, but right now \(due to time limit\) I can only support needs within the lab.

**If you download our published data and want to remap using the cell-level FASTQ files,** [**I provided a tutorial here**](mapping-2/mapping-form-cell-level-fastq-files.md)**.**
{% endhint %}

## What is YAP?

YAP \(**Y**et **A**nother-**P**ipeline \) is a mapping pipeline designed for several single nucleus methyl-cytosine sequencing \(snmC-seq\) based technologies.

[See source code on Github.](https://github.com/lhqing/cemba_data)

## Technologies Supported

* [snmC-seq2 & 3](tech-background/snmc-seq.md): DNA methylome
* snmCT-seq: DNA methylome + Transcriptom
* snm3C-seq: DNA methylome + Chromatin Contact
* [NOMe treated](tech-background/nome-treatment.md): X + Chromatin Accessibility

## After Mapping?

Check out [ALLCools](https://github.com/lhqing/ALLCools), the package for downstream cell-level and cluster-level analysis.



