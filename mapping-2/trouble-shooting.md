# Mapping Locally

{% hint style="info" %}
This section is only for debugging purposes. **Do not run mapping on the local server or the login node using a large number of cores.**
{% endhint %}

## Run snakemake directly

In each of the sub-directory, you can directly run snakemake to map or **dry-run** the mapping.

All mapping commands depend on each other, **the last command can visualize the command dependency graph for this sub-dir. An example `dag.svg` is attached below.**

```text
# go to a certain sub-dir that has the Snakefile
cd output_dir/sub_dir

# snakemake dry-run, this will walk through all the commands to map this sub-dir
snakemake -np

# a cool feature to visualize the 
$ snakemake --dag | dot -Tsvg > dag.svg

```

{% file src="../.gitbook/assets/dag \(1\).svg" caption="Visualization of snmC-seq3 mapping commands of a sub-directory" %}

## Troubleshooting

As shown in the visualization above, Snakefile contains dependent rules for the sub-directory. **Each rule corresponding to a shell command.** If you see any error that occurs during the execution of snakemake on qsub or sbatch, you need to read the stderr and find out which command/rule is the reason causing failure. You can then copy the command and analyze the error information. You may execute that command again locally \(or via a separate job\) to see if it reoccur.

