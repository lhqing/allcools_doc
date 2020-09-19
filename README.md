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
* snmCT-seq: DNA methylome + Transcriptome
* snm3C-seq: DNA methylome + Chromatin Contact
* [NOMe treated](tech-background/nome-treatment.md): X + Chromatin Accessibility

## How to use?

1. Make sure you understand the background of [cell barcoding](tech-background/barcoding.md) and the technology you use. If not, read the corresponding TECH BACKGROUND section.
2. Follow the [installation tutorial](installation.md) to install yap and associated packages.
3. Follow the MAPPING PIPELINE section, example of each 
4. If you have question, first go to [FAQ](other/faq.md) page. **If problem is not solved,** [**post an issue on github**](https://github.com/lhqing/cemba_data)**.**

## After Mapping?

Check out [ALLCools](https://github.com/lhqing/ALLCools), the package for downstream cell-level and cluster-level analysis.

