---
description: Prepare bcl2fastq sample sheet for demultiplexing illumina primer index
---

# Prepare PlateInfo & bcl2fastq SampleSheet

## Related Commands

```text
# Print out template of the plate info
yap default-plate-info

# Make bcl2fastq sample sheet based on the plate info file
yap make-sample-sheet
```

## Purpose

In this step, we prepare a **PlateInfo file** that contains sample metadata and **PCR index information** of the plates in your library. This information is used to generate a **SampleSheet** file for `bcl2fastq` to demultiplex the PCR index when generating raw FASTQ files.

{% hint style="info" %}
[What is the PlateInfo file?](../other/faq.md#what-is-plateinfo-file)
{% endhint %}

## Input

Library preparation information, most importantly:

* The sample metadata \(you determine what is necessary for your experiment\)
* The plate IDs of this library
* The barcode information of this library

## Step 1: Prepare a PlateInfo file

### Get the PlateInfo file template and manually edit plate and barcode information

```text
# print V1 template
yap default-plate-info -v V1

# print V2 template
yap default-plate-info -v V2
```

### PlateInfo Examples

{% tabs %}
{% tab title="V2 Index Library" %}
* This example contains four plates
* Every plate has six multiplex groups
* All primer names must be unique for the same sequencing run.
* **PlateInfo section must be Tab `\t` separated.**

```text
[CriticalInfo]
n_random_index=384
input_plate_size=384
pool_id=Pool_9
tube_label=Pool_9
email=hanliu@salk.edu;bawang@salk.edu;abartlett@salk.edu


[LibraryInfo]
lib_comp_date=200518
project=DVC
organism=mm
dev_stage_age=P120
tissue_cell_type=VC
lib_type=snmCT-seq
sequencer=NovaSeq
se_pe=pe
read_length=150
requested_by=HL


[PlateInfo]
plate_id	multiplex_group	primer_name
DVC200116_P120_VC_B_M_1_4	1	D11
DVC200116_P120_VC_B_M_1_4	2	F9
DVC200116_P120_VC_B_M_1_4	3	I10
DVC200116_P120_VC_B_M_1_4	4	C16
DVC200116_P120_VC_B_M_1_4	5	D2
DVC200116_P120_VC_B_M_1_4	6	I4
DVC200116_P120_VC_B_M_1_6	1	N6
DVC200116_P120_VC_B_M_1_6	2	J17
DVC200116_P120_VC_B_M_1_6	3	N12
DVC200116_P120_VC_B_M_1_6	4	L19
DVC200116_P120_VC_B_M_1_6	5	D7
DVC200116_P120_VC_B_M_1_6	6	J5
DVC200116_P120_VC_B_M_1_8	1	K22
DVC200116_P120_VC_B_M_1_8	2	J13
DVC200116_P120_VC_B_M_1_8	3	E10
DVC200116_P120_VC_B_M_1_8	4	M21
DVC200116_P120_VC_B_M_1_8	5	J6
DVC200116_P120_VC_B_M_1_8	6	C4
DVC200116_P120_VC_B_M_2_4	1	P8
DVC200116_P120_VC_B_M_2_4	2	J19
DVC200116_P120_VC_B_M_2_4	3	I21
DVC200116_P120_VC_B_M_2_4	4	C9
DVC200116_P120_VC_B_M_2_4	5	P10
DVC200116_P120_VC_B_M_2_4	6	J4
```
{% endtab %}

{% tab title="V1 Index Library" %}
* This example contains eight plates
* Every two plates share a primer quarter
* Possible primer\_quarter values are:
  * SetB\_Q1, SetB\_Q2, SetB\_Q3, SetB\_Q4
  * Set1\_Q1, Set1\_Q2, Set1\_Q3, Set1\_Q4
* Each primer\_quarter appears no more than twice for the same sequencing run.
* **PlateInfo section must be Tab `\t` separated.**

```text
[CriticalInfo]
n_random_index=8
input_plate_size=384
pool_id=Pool_73
tube_label=Pool_73
email=your_email_address@salk.edu

[LibraryInfo]
lib_comp_date=180101
project=CEMBA
organism=mm
dev_stage_age=P56
tissue_cell_type=9C
lib_type=snmCseq2
sequencer=NovaSeq
se_pe=pe
read_length=150
requested_by=HL

[PlateInfo]
plate_id	primer_quarter
CEMBA190530_9C_1	SetB_Q1
CEMBA190530_9C_2	SetB_Q1
CEMBA190530_9C_3	SetB_Q2
CEMBA190530_9C_4	SetB_Q2
CEMBA190620_9C_1	SetB_Q3
CEMBA190620_9C_2	SetB_Q3
CEMBA190620_9C_3	SetB_Q4
CEMBA190620_9C_4	SetB_Q4
```
{% endtab %}
{% endtabs %}

## Step 2: Run `yap make-sample-sheet`

* `yap make-sample-sheet` take a V1 or V2 plate info file to generate a bcl2fastq sample sheet.
* The sample sheet and name pattern are automatically generated so the pipeline can automatically parse cell information during and after mapping.
* See usage in the command line `yap make-sample-sheet -h`

```text
yap make-sample-sheet -h
usage: yap make-sample-sheet [-h] --plate_info_path PLATE_INFO_PATH
                             --output_prefix OUTPUT_PREFIX
                             [--header_path HEADER_PATH]

optional arguments:
  -h, --help            show this help message and exit

Required inputs:
  --plate_info_path PLATE_INFO_PATH, -p PLATE_INFO_PATH
                        Path of the plate information file. (default: None)
  --output_prefix OUTPUT_PREFIX, -o OUTPUT_PREFIX
                        Output prefix, will generate 2 sample sheets, 1 for
                        miseq, 1 for novaseq (default: None)

Optional inputs:
  --header_path HEADER_PATH
                        Path to the sample sheet header that contains
                        sequencer info. Will use default if not provided.
                        (default: None)
```

## Output

* PlateInfo file recording library preparation information
* Three sample sheets for `bcl2fastq` demultiplexing. One for MiSeq, two for NovaSeq \(v1, or v1.5\).

{% hint style="info" %}
For libraries sequenced with illumina v1.5 S4 kit, the i5 barcodes in the sample sheet are reverse complemented.
{% endhint %}

### Output after bcl2fastq

* The raw FASTQ generated by bcl2fastq using SampleSheet generated in this step will contain several \(8 in V1 and 64 in V2\) cells' reads. 
* The random index occurs at the 5' of R1.
* The PCR index is trimmed from both R1 and R2 and put into the read name.

