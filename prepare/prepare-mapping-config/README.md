# Prepare Mapping Config

## Related Commands

```text
# Print out template of the mapping config
yap default-mapping-config
```

## Purpose

In this step, you need to prepare a MappingConfig file that contains all the parameters for the mapping pipeline. **Mainly, the path to the genome reference files.**

{% hint style="info" %}
[What is MappingConfig file?](../../other/faq.md#what-is-mappingconfig-file)
{% endhint %}

## Input

* All the genome reference files, [see how to prepare here](prepare-reference-files.md).
* Technology type
* Barcoding version

## Step 1 - Get a template of MappingConfig

```text
yap default-mapping-config -h

usage: yap default-mapping-config [-h] --mode {mct,mc} --barcode_version
                                  {V1,V2} --bismark_ref BISMARK_REF
                                  --genome_fasta GENOME_FASTA
                                  [--star_ref STAR_REF] [--gtf GTF] [--nome]

optional arguments:
  -h, --help            show this help message and exit
  --mode {mct,mc}       Library mode (default: None)
  --barcode_version {V1,V2}, -v {V1,V2}, -V {V1,V2}
                        Barcode version, V1 for 8 random index, V2 for 384
                        random index (default: None)
  --bismark_ref BISMARK_REF
                        Path to the bismark reference (default: None)
  --genome_fasta GENOME_FASTA
                        Path to the genome fasta file (default: None)
  --star_ref STAR_REF   [mct only] Path to the STAR reference, required if
                        mode is mct (default: None)
  --gtf GTF             [mct only] Path to the GTF annotation file, required
                        if mode is mct (default: None)
  --nome                Does this library have NOMe treatment? (default:
                        False)
```

### Example of MappingConfig files

{% file src="../../.gitbook/assets/mc-v2.mouse.mapping\_config.ini" caption="snmC-seq3, Mouse, V2 barcode" %}

{% file src="../../.gitbook/assets/mct-v2.mouse.mapping\_config.ini" caption="snmCT-seq, Mouse, V2 barcode" %}

{% file src="../../.gitbook/assets/m3c-v2.human.mapping\_config.ini" caption="snm3C-seq, Human, V2 barcode" %}

## Step 2 - Review

Review and modify the MappingConfig template as you need, each parameter is explained within the template.

{% hint style="warning" %}
Remember different server needs different MappingConfig \(different reference path\).
{% endhint %}

## Output

* mapping\_config.ini file, needed for `yap demultiplex`.

