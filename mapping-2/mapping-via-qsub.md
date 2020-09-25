# Mapping Via Qsub

{% hint style="warning" %}
Content on this page only related to the Ecker Lab servers. But the same idea can be apply to any other servers with some modification.
{% endhint %}

{% hint style="info" %}
[Read more about SGE qsub here.](http://bioinformatics.mdc-berlin.de/intro2UnixandSGE/sun_grid_engine_for_beginners/how_to_submit_a_job_using_qsub.html)
{% endhint %}

## Input

After demultiplex, all the snakemake command is also summarized in the `{output_dir}/snakemake/qsub` directory. 

The `snakemake_cmd.txt` contains all the snakemake command for all PCR index sub-directories. 

The `qsub.sh` is a submission script file that can automatically submit all these commands via `yap qsub`. `yap qsub` will control the total number of jobs run in parallel on the qsub. 

```text
output_dir
├── snakemake
│   ├── qsub
│   │   ├── qsub.sh
│   │   └── snakemake_cmd.txt
```

### qsub.sh

```text
# these qsub parameters are for the job submitter, not for the mapping jobs.
#!/bin/bash
#$ -N {lib_name}
#$ -V
#$ -l h_rt=999:99:99
#$ -l s_rt=999:99:99
#$ -wd {output_dir}/snakemake/qsub
#$ -e {output_dir}/snakemake/qsub/qsub.error.log
#$ -o {output_dir}/snakemake/qsub/qsub.output.log
#$ -pe smp 1
#$ -l h_vmem=3G

# yap qsub is an job submitter for SGE qsub
yap qsub \
--command_file_path {output_dir}/snakemake/sbatch/snakemake_cmd.txt \
--working_dir {output_dir}/snakemake/qsub \
--project_name {lib_name} \
--total_cpu 96 \  # a total of 96 cores, so 12 job will run in parallel
--qsub_global_parms "-pe smp=8;-l h_vmem=5G"  
# this means each job use 8 cores, each core use 5 Gb MEM, a total of 40 MEM.

```

## Execute

the yap qsub command will not exit until all the mapping finished, so you better execute this command in the following options:

### Option 1 - use a screen

```text
# open a screen
screen -R qsub

# in that screen, activate the mapping environment
conda activate mapping

# run the submitter interactively
sh qsub.sh
```

### Option 2 - qsub the submitter

```text
# in that screen, activate the mapping environment
conda activate mapping

# run the submitter interactively
qsub qsub.sh
```

## Output

The hallmark of successful snakemake execution is the existence of a `MappingSummary.csv.gz` in that sub-directory. Because this file is the final target of snakemake. This file will only occur when all the previous mapping command is executed successfully.

Except for this summary file, you will also see the actual data file \(ALLC, BAM, etc.\) organized in sub-directories. Different technology will have different output. For example, this is the directory structure of snmC-seq3 V2 barcoding, the minimum example files is also attached:

```text
output_dir
├── sub_dir
│   ├── allc
│   │   └── (cell ALLC files and index files)
│   ├── bam
│   │   └── (cell final BAM files and index files)
│   ├── fastq
│   │   └── (cell raw FASTQ files, this is unchanged) 
│   ├── MappingSummary.csv.gz  # this is the final targets of this sub-dir
│   └── Snakefile
├── (other sub-dirs)
├── mapping_config.ini
├── snakemake
└── stats
```

{% file src="../.gitbook/assets/snmc-seq3.v2.mapped.tgz" caption="Mapped directory of snmC-seq3, V2 barcode" %}

