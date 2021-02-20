---
description: Prepare the Snakemake file for generating pseudo-bulk files
---

# Methylome Pseudo-bulk

After single-cell level analysis, the next step is to merge the single-cell methylome \(ALLC files\) into the pseudo-bulk level to increase the whole genome coverage. This allows us to generate the genome browser and identify potential regulatory elements at high genomic resolution.

## Input

* single-cell ALLC files from mapping
* cell group labels from the metadata or clustering analysis

These two kinds of inputs need to be organized in a **Tab-separated** **ALLC table** like this:

| NO HEADER |  |
| :--- | :--- |
| /path/to/allc/file/cell1.allc.tsv.gz | group1 |
| /path/to/allc/file/cell2.allc.tsv.gz | group1 |
| /path/to/allc/file/cell3.allc.tsv.gz | group2 |
| /path/to/allc/file/cell4.allc.tsv.gz | group2 |
| ... | ... |

## Generate Snakefile

Just like mapping, we use the `snakemake` to execute all the specific commands. YAP is just helping prepare a Snakefile for the whole process to

1. Generate a group-merged pseudo-bulk ALLC file for each group. These ALLC files have the same format as single-cell ALLC files. All the base counts in the same position are added together.
2. Generate BigWig files for each pseudo-bulk ALLC file. The mC context and bin size of the BigWig are provided by you.
3. OPTIONAL: Extract mCG sites from the merged ALLC. These files can be used to call CpG Differential Methylated Regions \(CG-DMRs\)

To generate the Snakefile, just run

```text
$ yap mc-bulk -h
usage: yap mc-bulk [-h] --allc_table ALLC_TABLE --output_dir OUTPUT_DIR
                   --bigwig_contexts BIGWIG_CONTEXTS [BIGWIG_CONTEXTS ...]
                   --chrom_size_path CHROM_SIZE_PATH [--extract_mcg]
                   [--bigwig_bin_size BIGWIG_BIN_SIZE]
                   [--merge_allc_cpu MERGE_ALLC_CPU]
                   [--mcg_context MCG_CONTEXT]

optional arguments:
  -h, --help            show this help message and exit

Required inputs:
  --allc_table ALLC_TABLE, -p ALLC_TABLE
                        Path of the allc table. The allc table is a two column
                        tsv file. The first columns is the absolute ALLC file
                        paths; the second column is the group name of each
                        file. (default: None)
  --output_dir OUTPUT_DIR, -o OUTPUT_DIR
                        Path of the output directory, will be created if not
                        exist. (default: None)
  --bigwig_contexts BIGWIG_CONTEXTS [BIGWIG_CONTEXTS ...]
                        mC contexts for generating the bigwig tracks.
                        (default: None)
  --chrom_size_path CHROM_SIZE_PATH
                        Path of the chromosome size file path. (default: None)

Optional inputs:
  --extract_mcg         Whether run the step to extract mCG sites from the
                        merged ALLC. If your input ALLC only contains mCG
                        sites, this can be skipped. Otherwise, this needs to
                        be done before running the CG-DMR calling. (default:
                        False)
  --bigwig_bin_size BIGWIG_BIN_SIZE
                        Bin size used to generate bigwig. (default: 50)
  --merge_allc_cpu MERGE_ALLC_CPU
                        Number of CPU to use in individual merge-allc job.
                        (default: 8)
  --mcg_context MCG_CONTEXT
                        mC context for extract_mcg step, only relevant when
                        extract_mcg=True. (default: CGN)
```

After running `yap mc-bulk` , there will be Snakefile in the `output_dir`, this Snakefile contains all the steps to generate the output files.

## Execute Snakefile

### Single command

To execute the Snakefile, simply run

```text
# this means snakemake will and parallel the jobs automatically 
# and try to use 20 cores in total.
snakemake --cores 20

```

Snakemake will parallel all the jobs for you.

### Execute in batches

If you are merging a large number of files, you may want to execute the Snakefile in multiple batches and parallel each batch to speed up merging.

To execute the Snakefile in batches, simply run

```text
# For each single command, it will only aim to execute 1/5 of the cell groups 
# and try to use 20 cores in total.
snakemake --cores 20 --batch main=1/5
snakemake --cores 20 --batch main=2/5
snakemake --cores 20 --batch main=3/5
snakemake --cores 20 --batch main=4/5
snakemake --cores 20 --batch main=5/5
```

You can any number of batches between 2 and N-cell-groups, just be consistent among your commands so no group is missed. Snakemake will automatically determine subsets to run in each command.

These commands can be executed in parallel, for example, if you separated five batches like above, you can submit five qsub/sbatch jobs to parallel them.

{% hint style="danger" %}
Currently, the merging step using `allcools merge` is still very I/O intensive, especailly when each of your group contains hundreds of cells. It can easily cause very high server load with high number of cores. Please monitor your jobs and use appropreate number of cores.
{% endhint %}

