# Mapping

## Input

* `yap demultiplex` output directory, refer to as `{output_dir}` below.

## Cell batches and snakemake

During demultiplex, cells are divided into small batches based on their PCR index. FASTQ files of each batch are saved together in a sub-directory of the `{output_dir}` . Each of the sub-directory is mapped together in a single job, all the steps that need to be done are written in the `{output_dir}/{sub_dir}/Snakefile` , a file needed by [snakemake](https://snakemake.github.io/), and contain all the commands to map the files in this sub-directory. 

Here is a single command used to execute the Snakefile, but you don't need to do this by yourself \(see below\):

```text
# to map cells in a single sub directory

snakemake \
-d {output_dir}/{sub_dir} \
--snakefile {output_dir}/{sub_dir}/Snakefile \
-j {parallel_cores_to_use_for_this_job}
```

{% hint style="info" %}
[What is snakemake?](../other/faq.md#what-is-snakemake)
{% endhint %}

## Execute snakemake commands

In the `{output_dir}/snakemake` , you should be able to find a list of snakemake commands like the above, one command for each PCR index sub-directory. You have three ways to execute these commands.

### For MiSeq

{% page-ref page="mapping-via-qsub.md" %}

### For NovaSeq

{% page-ref page="mapping-via-sbatch.md" %}

### For troubleshooting

{% page-ref page="trouble-shooting.md" %}

