# Mapping Via Sbatch

{% hint style="warning" %}
Content on this page only related to the Ecker Lab servers. But the same idea can be apply to any other servers with some modification.
{% endhint %}

{% hint style="info" %}
[Read more about Sbatch and Stampede2 user guide here.](https://portal.tacc.utexas.edu/user-guides/stampede2)
{% endhint %}

{% hint style="danger" %}
Remember you need to copy the genome reference files to stampede2 and use the corresponding MappingConfig file for demultiplex.
{% endhint %}

## Input

After demultiplex, all the snakemake command is also summarized in the `{output_dir}/snakemake/sbatch` directory. 

The `snakemake_cmd.txt` contains all the snakemake command for all PCR index sub-directories. 

The `sbatch.sh` is a submission script file that can automatically submit all these commands via `yap sbatch`. `yap sbatch` will control the total number of jobs run in parallel on the sbatch. 

```text
output_dir
├── snakemake
│   ├── sbatch
│   │   ├── sbatch.sh
│   │   └── snakemake_cmd.txt
```

### sbatch.sh

```text
# this command run all the snakemake commands for mapping
yap sbatch \
--project_name mc-V2 \
--command_file_path $SCRATCH/{lib_name}/snakemake/sbatch/snakemake_cmd.txt \
--working_dir $SCRATCH/{lib_name}/snakemake/sbatch \
--time_str 12:00:00
```

{% hint style="danger" %}
I assume you put the output\_dir on your stampede2 $SCRATCH directory with the same name. If you do not follow this assumption, you need to modify the sbatch and snakemake command by yourself.
{% endhint %}

## Transfer Files to Stampede2 Scratch

```text
# you can get your scratch dir location by
# on tacc login node
echo $SCRATCH

# and then make a soft link to your home dir
# on tacc login node
ln -s $SCRATCH ~/scratch

# on local server
rsync -arv {output_dir} tacc:scratch/
```

## Execute

Just like qsub, you only need to execute the sbatch.sh. It will generate all the sbatch script for each snakemake command and execute them. And it will also wait for all command to finish before exit. I do not recommend running this as a separate sbatch job, because the execution time could be long. You can just execute this in screen or `nohup`

```text
# open a screen
screen -R sbatch

# in that screen, activate the mapping environment
conda activate mapping

# run the submitter interactively
sh sbatch.sh
```

## Output

The output files are the same as [qsub output files](mapping-via-qsub.md#output).

## Transfer Files Back

After mapping, you can `rsync` the whole `output_dir` from the remove server back to the same location, while skip all the FASTQ files \(because they are unchanged\).

```text
# the {output_dir} is the same dir uploaded to tacc
rsync -arv --exclude "*fq.gz" tacc:scratch/{lib_name} {output_dir}
```



