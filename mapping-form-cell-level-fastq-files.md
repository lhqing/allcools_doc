# Mapping Form Cell-Level FASTQ Files

{% hint style="warning" %}
If you start from `yap demultiplex`, you do not need to follow this page. This page is for the situation where you directly start from cell-level FASTQ files.
{% endhint %}

If you directly downloaded **demultiplexed** cell-level FASTQ files from the database, you can skip the `yap demultiplex` step and directly prepare the `Snakefiles` for mapping using `yap start-from-cell-fastq`.

## Requirements on FASTQ files

* The FASTQ file name must follow the following pattern, especially the suffix part:
  * For R1 FASTQ: `{cell_id}-R1.fq.gz`
  * For R2 FASTQ: `{cell_id}-R2.fq.gz`
* The `{cell_id}` must be unique, it will be used as cells' ID in the mapping summary.
* Each cell must have one R1 and one R2 FASTQ file.

## Input

* FASTQ files prepared as the above section
* Mapping config INI file of corresponding technology, see how to prepare that file [here](prepare/prepare-mapping-config/).

{% hint style="info" %}
If you don't know the barcode version, you may have a guess based on the [file name](mapping-metrics/all-mapping-metrics.md#cell-id) pattern. If the file name does not follow a normal pattern, just use "V2"

the algorithm will skip generating plate information if the file name pattern is not following YAP's pattern, but plate information is not necessary for the following analysis.
{% endhint %}

## Prepare Mapping

This is a single command that finishes quickly. It does not run any mapping command, instead, it generates a very similar directory structure as the `yap demultiplex` will do. It also generates all the `Snakefile` that contain the actual mapping commands and can be executed using `snakemake`. 

```text
$ yap start-from-cell-fastq -h
usage: yap start-from-cell-fastq [-h] --output_dir OUTPUT_DIR --config_path
                                 CONFIG_PATH --fastq_pattern FASTQ_PATTERN

optional arguments:
  -h, --help            show this help message and exit

Required inputs:
  --output_dir OUTPUT_DIR, -o OUTPUT_DIR
                        Pipeline output directory, if not exist, will create
                        recursively. (default: None)
  --config_path CONFIG_PATH, -config CONFIG_PATH
                        Path to the mapping config, see 'yap default-mapping-
                        config' about how to generate this file. (default:
                        None)
  --fastq_pattern FASTQ_PATTERN, -fq FASTQ_PATTERN
                        Path pattern with wildcard to match all cell-level 
                        FASTQ files, pattern with wildcard must be quoted.
                        (default: None)
```

{% hint style="info" %}
One technical note, here I randomly group FASTQ pairs into several groups, each group got one `Snakefile` and will be mapped together. This step does not impact any of the mapping results.
{% endhint %}

## Execute Mapping

Just like the [previous page](mapping-2/#execute-snakemake-commands), all you need to do is execute the snakemake commands. All commands should be summarized in the `{output_dir}/snakemake` directory.

## Output

The output is just like [this example](mapping-2/mapping-via-qsub.md#output). The `MappingSummary.csv.gz` in each group directory is the final target file, if this file exists, all command must be executed successfully in that group directory.

After mapping, you can also run `yap summary` as explained on the next page.

## More customized mapping

The scope of YAP is just for some fixed mapping pipeline that consistent with our publications. If you do want to have more finner control of the mapping steps, I suggest you read the Snakefile templates and make your own versions by yourself.

The main work YAP did is generating the `Snakefile` based on file inputs and the `Snakefile` templates. The resulting `Snakefile` contains all steps to map the data.

 [Snakefile templates](https://github.com/lhqing/cemba_data/tree/master/cemba_data/mapping/Snakefile_template) are part of YAP's source code and are pretty straightforward to read. If you need any help on the Snakefile format, you can go to [snakemake's documentation](https://snakemake.readthedocs.io/en/stable/index.html).





