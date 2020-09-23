# Mapping

## Input

* `yap demultiplex` output directory, refer to as `{output_dir}` below.

## Cell batches and snakemake

During demultiplex, cells are divided into small batches based on their PCR index. FASTQ files of each batch are saved together in sub-directory of the `{output_dir}` . Each of the sub-directory is mapped together in a single job, all the steps need to be done are written in the `{output_dir}/{sub_dir}/Snakefile` , following snakemake's special format. The single command to achieve thatL

```text
# to map cells in a single sub directory

snakemake \
-d {output_dir}/{sub_dir} \
--snakefile {output_dir}/{sub_dir}/Snakefile \
-j {cores_to_use_for_this_job}
```

{% hint style="info" %}
[What is snakemake?](../other/faq.md#what-is-snakemake)
{% endhint %}

## Step 1. Execute snakemake commands

In the `{output_dir}/snakemake` , you should be able to find a list of snakemake commands, one for each PCR index sub-directory. You have three ways to execute these commands to map the files.

### For MiSeq

{% page-ref page="mapping-via-qsub.md" %}

### For NovaSeq

{% page-ref page="mapping-via-sbatch.md" %}

### For trouble shooting

{% page-ref page="trouble-shooting.md" %}

## Output

Different technologies has different output file structure, see [corresponding mapping examples](example.md).



