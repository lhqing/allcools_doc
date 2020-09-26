---
description: All mapping metrics from the mapping pipeline
---

# All Mapping Metrics

## Cell ID

The first column \(row index\) of the mapping summary file is the cell ID. The cell ID pattern for [V1 barcoding](../tech-background/barcoding.md#version-1-v-1-before-spring-2020) and [V2 barcoding](../tech-background/barcoding.md#version-2-v-2-spring-2020-to-now) is different.

#### V1 cell ID 

`{Plate1}-{Plate2}-{PCRIndex}-{RandomIndex}`, the Plate1 and Plate2 are two plates that multiplexed together by the eight random indexes. The Plate column \(see below\) is the actual plate that the cell comes from.

#### V2 cell ID 

`{Plate}-{MultiplexGroup}-{PCRIndex}-{RandomIndex}`. 

## Plate and Barcode Information

#### Plate

The 384-plate ID. Information from the in PlateInfo file.

#### PCRIndex

The PCR index name. Information from the in PlateInfo file.

#### MultiplexGroup （V2 barcoding only）

The multiplex group number, a int from 1 to 6. Information from the in PlateInfo file.

#### RandomIndex

The random index name. Assigned during `yap demultiplex`.

#### Col384

The original column in the 384-plate.

#### Row384

The original row in the 384-plate.

## FASTQ Metrics

### Raw FASTQ

#### R1InputReads

Total number of R1 generated from `yap demultiplex`. This equals to `CellInputReadPairs` and `R2InputReads`.

#### R1InputReadsBP

Total number of R1 base pairs generated from `yap demultiplex`.

#### R2InputReads

Total number of R2 generated from `yap demultiplex`. This equals to `CellInputReadPairs` and `R1InputReads`.

#### R2InputReadsBP

Total number of R2 base pairs generated from `yap demultiplex`.

#### CellInputReadPairs

Total number of read pairs generated from `yap demultiplex`. This equals to `R1InputReads` and `R2InputReads`.

#### CellBarcodeRatio

Calculated by `CellInputReadPairs / sum(CellInputReadPairs of the same multiplex group)` .

### Trimmed FASTQ

#### R1WithAdapters

Number of R1 trimmed due to having illumina adapter.

#### R1QualTrimBP

Number of R1 base pairs trimmed due to low base quality.

#### R1TrimmedReads

Number of R1 **remained** after adapter and quality trimming.

#### R1TrimmedReadsBP

Number of R1 base pairs **remained** after adapter and quality trimming.

#### R1TrimmedReadsRate

Calculated by `R1TrimmedReads / R1InputReads`.

#### R2WithAdapters

Number of R2 trimmed due to having illumina adapter. 

#### R2QualTrimBP

Number of R2 base pairs trimmed due to low base quality.

#### R2TrimmedReads

Number of R2 **remained** after adapter and quality trimming.

#### R2TrimmedReadsBP

Number of R2 base pairs **remained** after adapter and quality trimming.

#### R2TrimmedReadsRate

Calculated by `R2TrimmedReads / R2InputReads`.

## BAM Metrics

### Bismark Mapped BAM

#### R1UniqueMappedReads

#### R1MappingRate

#### R1UnmappedReads

#### R1UnuniqueMappedReads

#### R1OT

#### R1OB

#### R1CTOT

#### R1CTOB

#### R1TotalC

#### R1TotalmCGRate

#### R1TotalmCHGRate

#### R1TotalmCHHRate

#### R2UniqueMappedReads

#### R2MappingRate

#### R2UnmappedReads

#### R2UnuniqueMappedReads

#### R2OT

#### R2OB

#### R2CTOT

#### R2CTOB

#### R2TotalC

#### R2TotalmCGRate

#### R2TotalmCHGRate

#### R2TotalmCHHRate

### Filtered BAM

#### R1MAPQFilteredReads

#### R1DuplicatedReads

#### R1DuplicationRate

#### R1FinalBismarkReads

#### R2MAPQFilteredReads

#### R2DuplicatedReads

#### R2DuplicationRate

#### R2FinalBismarkReads

#### FinalmCReads

## ALLC Metrics

#### mCHmC

#### mCHCov

#### mCHFrac

#### mCGmC

#### mCGCov

#### mCGFrac

#### mCCCmC

#### mCCCCov

#### mCCCFrac

#### GenomeCov

