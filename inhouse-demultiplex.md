# \[inhouse\] Demultiplex

In the previous step, we generated sample sheets based on the PlateInfo file and then used Illumina bcl2fastq to demultiplex BCL files from the sequencer. The bcl2fastq command only demultiplexed the barcodes on the Illumina primers. Therefore, each set of FASTQ files still contain reads mixed from multiple cells \(eight cells in V1; 384 cells in V2\). This step further demultiplex barcodes on the random primers, generating raw FASTQ file pairs for every single cell.

## Related Commands

```text
yap demultiplex
```

## Input

Illumina \`bcl2fastq\` demultiplexed FASTQ files.

## Demultiplex

```text
$ yap demultiplex -h
usage: yap demultiplex [-h] --fastq_pattern FASTQ_PATTERN --output_dir
                       OUTPUT_DIR --barcode_version {V1,V2} --mode
                       {mc,mct,mc2t} --cpu CPU

optional arguments:
  -h, --help            show this help message and exit

Required inputs:
  --fastq_pattern FASTQ_PATTERN
                        FASTQ files with wildcard to match all bcl2fastq
                        results, pattern with wildcard must be quoted.
                        (default: None)
  --output_dir OUTPUT_DIR
                        Pipeline output directory, will be created
                        recursively. (default: None)
  --barcode_version {V1,V2}
                        Barcode version of this library, V1 for the 8 random
                        index, V2 for the 384 random index. (default: None)
  --mode {mc,mct,mc2t}  Technology used in this library. (default: None)
  --cpu CPU             Number of cores to use. Max is 12. (default: None)
```

{% hint style="info" %}
* It took several minutes to demultiplex MiSeq files, several hours to demultiplex NovaSeq FASTQ files \(~80GB / h with 12 cores\). 
* This command creates lots of files simultaneously, in order to prevent too much burden on the file system, I set max CPU = 12
* Remember to use " to quote the fastq pattern like this: `--fastq_pattern "path/pattern/to/your/bcl2fastq/results/fastq.gz"`
* An error will occur if `output_dir`already exists.
{% endhint %}

## Output

* This step demultiplexes raw FASTQ files into single-cell raw FASTQ files.
* The random index sequence will be removed from the reads
  * 6bp from R1 5' in V1 indexed libraries.
  * 8bp from R1 5' in V2 indexed libraries.
* Each cell will have two FASTQ files in the output directory, with a fixed name pattern:
  * `{cell_id}-R1.fq.gz` for R1
  * `{cell_id}-R2.fq.gz` for R2

