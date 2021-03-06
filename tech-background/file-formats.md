---
description: Base level methylation counts
---

# File Formats

## ALLCools

Both ALLC and MCDS files are generated by ALLCools. Read more details about ALLCools [here](https://hq-1.gitbook.io/allcools/).

## ALLC File

The ALLC \(ALL Cytosine\) format is a tab-separated table contain **base level methylation and coverage counts**. ALLC format is originally defined by [methylpy](https://github.com/yupenghe/methylpy), a python package developed in our lab for bulk WGBS-seq data analysis. Each row in an ALLC file corresponds to one cytosine in the genome. An ALLC file contains 7 mandatory columns and no header. YAP uses ALLCools to generate ALLC files compressed and indexed by `bgzip` and `tabix` from the [`htslib`](https://github.com/samtools/htslib).

The ALLC file generated by YAP only contains information from a single cell, while the ALLC file can also be merged from multiple single cells \(by cluster, etc.\) as a bulk-level methylation table.

### Columns in ALLC file

| index | column name | example | note |
| :--- | :--- | :--- | :--- |
| 1 | chromosome | chr12 | The same as genome FASTA |
| 2 | position | 18283342 | 1-based |
| 3 | strand | + | either + or - |
| 4 | sequence context | CGT | can be more than 3 bases, used to determine mC type |
| 5 | mc | 1 | count of reads supporting methylation |
| 6 | cov | 2 | read coverage, cov &gt;= mc |
| 7 | methylated | 1 | indicator of significant methylation \(1 if no test is performed\) |

### Tabix of ALLC file

Using `bgzip` and `tabix`, we can compress the ALLC file while allowing region query. This is done by YAP \(using ALLCools\) automatically, but here is an example of the exact command to do so:

```text
# bgzip is similar to gzip, 
# but it allow tabix to generate index from the compressed file.
$ bgzip CELL_ID.allc.tsv

# tabix generate an "CELL_ID.allc.tsv.gz.tbi" file of this ALLC file.
$ tabix -b 2 -e 2 -s 1 CELL_ID.allc.tsv.gz

# you can then query specific region from this ALLC file.
$ tabix CELL_ID.allc.tsv.gz chr1:100000000-101000000 | head
chr1	100016605	+	CCT	0	1	1
chr1	100016606	+	CTT	0	1	1
chr1	100016614	+	CCG	0	1	1
chr1	100016615	+	CGC	1	1	1
chr1	100016617	+	CCC	0	1	1
chr1	100016618	+	CCA	0	1	1
chr1	100016619	+	CAC	0	1	1
chr1	100016621	+	CCT	0	1	1
chr1	100016622	+	CTC	0	1	1
chr1	100016624	+	CGG	1	1	1

# see tabix and bgzip documentation for more information
$ tabix -h
```

## MCDS File

{% hint style="info" %}
I am updating ALLCools and its documentation, once done, will provide a link here. Right now this is a minimum introduction of MCDS.
{% endhint %}

ALLC file records all the methylation raw counts, but for clustering analysis, we need to do some "binning" to get the feature-level \(genomic-region-level\) raw counts. [After mapping, the `allcools mcds` function is used to aggregate all the single-cell ALLC files into a cell-by-feature dataset, called MCDS file](../generate-mcds.md).

Unlike the ALLC file that has fixed format, the MCDS file is a flexible dataset storing all different kinds of feature counts \(gene, genomic bins at different length\) at different methylation types \(CpH, CpG\) in a single[ netCDF4 file](../other/faq.md#what-is-netcdf-4). 

MCDS file is generated and manipulated by the python package `xarray.Dataset`, which allows easy combination, selection, and transformation of the multi-dimensional raw count array to cell-by-feature 2-D array for clustering. [See xarray's documentation for more information.](http://xarray.pydata.org/en/stable/)

![MCDS file contains all kinds of feature-level methylation counts in a single netCDF4 file.](../.gitbook/assets/image%20%285%29.png)

### Example of using MCDS

[Here](https://github.com/lhqing/clustering_example) I provide a toy dataset in MCDS format and some example code of reading it using xarray. For more details about MCDS and further clustering steps, please go to [the ALLCools documentation](https://hq-1.gitbook.io/allcools/).

