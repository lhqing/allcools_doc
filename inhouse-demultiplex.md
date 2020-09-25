# Demultiplex

## Related Commands

```text
# demultiplex the random index, generate cell-level FASTQ files
yap demultiplex
```

## Purpose

The `bcl2fastq` command only demultiplexed the **PCR index**. ****Therefore, each set of the raw FASTQ files still contain reads from several cells \(8 cells in V1; 64 cells in V2\). This step further demultiplex **random index** on the 5' of R1, generating cell-level R1 and R2 FASTQ files.

**Random index is trimmed after demultiplex.** The random index name occur at the FASTQ file name, which combine with previous information to form the cell id.

**This step also prepares Snakefiles that contain all the commands for mapping \(using** [**snakemake**](https://snakemake.readthedocs.io/en/stable/)**\).**

## Input

Illumina `bcl2fastq` created FASTQ file sets.

* For MiSeq, each set has two files \(R1 & R2 from one lane\)
* For NovaSeq, each set has 2 \* N\_lane files, N\_lane depends on the flowcell used and the way of loading.

## Demultiplex

```text
yap demultiplex -h
usage: yap demultiplex [-h] --fastq_pattern FASTQ_PATTERN --output_dir
                       OUTPUT_DIR --config_path CONFIG_PATH --cpu CPU

optional arguments:
  -h, --help            show this help message and exit

Required inputs:
  --fastq_pattern FASTQ_PATTERN, -fq FASTQ_PATTERN
                        FASTQ files with wildcard to match all bcl2fastq
                        results, pattern with wildcard must be quoted.
                        (default: None)
  --output_dir OUTPUT_DIR, -o OUTPUT_DIR
                        Pipeline output directory, will be created
                        recursively. (default: None)
  --config_path CONFIG_PATH, -config CONFIG_PATH
                        Path to the mapping config, see 'yap default-mapping-
                        config' about how to generate this file. (default:
                        None)
  --cpu CPU, -j CPU     Number of cores to use. Note that the demultiplex step
                        will only use at most 16 cores. (default: None)
```

{% hint style="info" %}
* It took several minutes to demultiplex MiSeq files, several hours to demultiplex NovaSeq FASTQ files \(~100GB / h with 16 cores\). 
* This command creates lots of files simultaneously, in order to prevent too much burden on the file system, I set max CPU = 16
* Remember to use "" to quote the fastq pattern like this, otherwise the wildcard will be expanded in shell and cause error: `--fastq_pattern "path/pattern/to/your/bcl2fastq/results/fastq.gz"`
* An error will occur if `output_dir`already exists.
{% endhint %}

{% hint style="danger" %}
**For Ecker Lab users**, do not run this step on DDN drive, `cutadapt demultiplex` \(what `yap` is based on\) constantly raise error on DDN drive. More safely, do not run mapping on DDN drive.
{% endhint %}

## Output

* The random index sequence will be removed from the reads
  * 6bp removed from R1 5' in V1 indexed libraries.
  * 8bp removed from R1 5' in V2 indexed libraries.
* Each cell will have two FASTQ files in the output directory, with a fixed name pattern:
  * `{cell_id}-R1.fq.gz` for R1
  * `{cell_id}-R2.fq.gz` for R2
* Files are organized by the following structure**, a minimum example is also attached below.**

```text
output_dir
├── CEMBA200709_9E_4-1-E18  # a set of FASTQ files
│   ├── fastq
|   |   ├──{cell1}-R1.fq.gz
|   |   ├──{cell1}-R2.fq.gz
|   |   ├──{cell2}-R1.fq.gz
|   |   ├──{cell2}-R2.fq.gz
|   |   ├──...
|   |   ├── skipped  # some FASTQ files may be skipped due to too less or too much reads
|   |   |   ├──...
│   └── Snakefile  # command files for snakemake
├── (Other sets)
│   ├── fastq
|   |   ├──...
|   |   ├── skipped
|   |   |   ├──...
│   └── Snakefile
├── mapping_config.ini  # mapping config copied here
├── snakemake  # this only occur when using yap in Ecker Lab server
│   ├── qsub  # job script for qsub on gale
│   └── sbatch  # job script for sbatch on stampede2
└── stats  # place for summary stats
    ├── demultiplex.stats.csv
    ├── fastq_dataframe.csv
    └── UIDTotalCellInputReadPairs.csv
```

{% file src=".gitbook/assets/snmc-seq3.miseq.v2.tgz" caption="snmC-seq3, MiSeq, V2 barcode, demultiplex results" %}

