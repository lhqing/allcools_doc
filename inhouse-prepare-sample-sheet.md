---
description: Prepare bcl2fastq sample sheet for demultiplexing illumina primer index
---

# \[inhouse\] Prepare Sample Sheet

## Related Commands

```text
# Print out template of the plate info
yap default-plate-info

# Make bcl2fastq sample sheet based on the plate info file
yap make-sample-sheet
```

## Input

Library preparation information, most importantly:

* The plate IDs in this library
* The barcode information in this library

## Step 1: Prepare a PlateInfo file

### What is the PlateInfo file?

* A plain text file with experimental, library, and barcoding information.
* This file needs to be made manually for each library.
* The main content of this file is the **barcoding information for each plate in the library**, so the pipeline can properly **demultiplex and name the single-cell files** with that information
* The initial 8-random-index barcoding version is V1, the 384-random index barcoding version is V2

### Get plate\_info.txt template and manually edit plate and barcode information

```text
# V1
yap default-plate-info -v V1

# V2
yap default-plate-info -v V2
```

### PlateInfo Examples

{% tabs %}
{% tab title="V1 Index Library" %}
* This example contains eight plates
* Every two plates share a primer quarter
* Possible primer\_quarter values are:
  * SetB\_Q1, SetB\_Q2, SetB\_Q3, SetB\_Q4
  * Set1\_Q1, Set1\_Q2, Set1\_Q3, Set1\_Q4
* Each primer\_quarter appears no more than twice for the same NovaSeq run.
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

{% tab title="V2 Index Library" %}
* This example contains four plates
* Every plate has six multiplex groups
* All primer names must be unique for the same NovaSeq run.
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
{% endtabs %}

## Step 2: Run `yap make-sample-sheet`

* `yap make-sample-sheet` take a V1 or V2 plate info file to generate a bcl2fastq sample sheet.
* The sample sheet and name pattern are automatically generated so the pipeline can automatically parse cell information during and after mapping.
* See usage in the command line `yap make-sample-sheet -h`

## Output

* PlateInfo file recording library preparation information
* Two sample sheets for bcl2fastq demultiplexing. One for MiSeq, one for NovaSeq.



