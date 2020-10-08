# Before Start

## Important Note

{% hint style="warning" %}
YAP is a full pipeline designed for raw sequencing data \(BCL files and raw FASTQ files before demultiplex\) generated [in the Ecker Lab](https://ecker.salk.edu/).

**If you download our published data and want to remap using the cell-level FASTQ files,** [**I provided a tutorial here**](mapping-form-cell-level-fastq-files.md)**.**
{% endhint %}

## What is YAP?

YAP \(**Y**et **A**nother-**P**ipeline \) is a mapping pipeline designed for several single nucleus methyl-cytosine sequencing \(snmC-seq\) based technologies.

[See source code on Github.](https://github.com/lhqing/cemba_data)

### Author

[Hanqing Liu](https://github.com/lhqing)

## Technologies Supported

* [snmC-seq2 & 3](tech-background/tech-ref.md#snmc-seq2-3): DNA methylome
* [snmCT-seq](tech-background/tech-ref.md#snmct-seq): DNA methylome + Transcriptome
* [snm3C-seq](tech-background/tech-ref.md#snm-3-c-seq): DNA methylome + Chromatin Contact
* [NOMe treated](tech-background/tech-ref.md#snmct-seq): X + Chromatin Accessibility

## How to use it?

1. Be familiar with the background of [cell barcoding](tech-background/barcoding.md) and the technology you use. If not, read the corresponding TECH BACKGROUND section.
2. Follow the [installation tutorial](installation.md) to install `yap` and associated packages.
3. Follow the MAPPING PIPELINE section step by step.
4. If you have questions, first go to the [FAQ](other/faq.md) page. **If the problem is not solved, you can** [**post an issue on GitHub**](https://github.com/lhqing/cemba_data/issues/new)**.**
5. This documentation is searchable.

## After Mapping?

Check out [ALLCools](https://github.com/lhqing/ALLCools), the package for downstream cell-level and cluster-level analysis.

