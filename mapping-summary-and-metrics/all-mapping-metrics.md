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

Number of unique mapped R1 reported by bismark.

#### R1MappingRate

R1 mapping rate reported by bismark.

#### R1UnmappedReads

Number of unmapped R1 reported by bismark.

#### R1UnuniqueMappedReads

Number of ununique mapped R1 reported by bismark.

#### R1UnuniqueMappedReads \(m3C specific\)

Number of R1 that has unique read name \(to prevent recount split reads\) in MAPQ filtered BAM file.

#### R1MappingRate \(m3C specific\)

R1 mapping rate calculated by `R1UnuniqueMappedReads / R1TrimmedReads * 100` .

#### R1OT

Number of R1 mapped to Original Top strand reported by bismark.

#### R1OB

Number of R1 mapped to Original Bottom strand reported by bismark.

#### R1CTOT

Number of R1 that are ComplemenTary to the Original Top strand reported by bismark.

#### R1CTOB

Number of R1 that are ComplemenTary to the Original Bottom strand reported by bismark.

#### R1TotalC

Number of total Cytosine beed covered in R1 reported by bismark.

#### R1TotalmCGRate

mCG fraction in R1 reported by bismark.

#### R1TotalmCHGRate

mCHG fraction in R1 reported by bismark.

#### R1TotalmCHHRate

mCHH fraction in R1 reported by bismark.

#### R2UniqueMappedReads

Number of unique mapped R2 reported by bismark.

#### R2UnuniqueMappedReads \(m3C specific\)

Number of R2 that has unique read name \(to prevent recount split reads\) in MAPQ filtered BAM file.

#### R2MappingRate \(m3C specific\)

R2 mapping rate calculated by `R1UnuniqueMappedReads / R1TrimmedReads * 100` .

#### R2MappingRate

R2 mapping rate reported by bismark.

#### R2UnmappedReads

Number of unmapped R2 reported by bismark.

#### R2UnuniqueMappedReads

Number of ununique mapped R2 reported by bismark.

#### R2OT

Number of R2 mapped to Original Top strand reported by bismark.

#### R2OB

Number of R2 mapped to Original Bottom strand reported by bismark.

#### R2CTOT

Number of R2 that are ComplemenTary to the Original Top strand reported by bismark.

#### R2CTOB

Number of R2 that are ComplemenTary to the Original Bottom strand reported by bismark.

#### R2TotalC

Number of total Cytosine beed covered in R2 reported by bismark.

#### R2TotalmCGRate

mCG fraction in R2 reported by bismark.

#### R2TotalmCHGRate

mCHG fraction in R2 reported by bismark.

#### R2TotalmCHHRate

mCHH fraction in R2 reported by bismark.

### Filtered BAM

#### R1MAPQFilteredReads

Number of R1 after filtering by MAPQ.

#### R1DuplicatedReads

Number of R1 that are marked as PCR duplicates.

#### R1DeduppedReads \(m3C specific\)

Number of R1 **remained** after removing PCR duplicates. Counted reads that have unique read name \(to prevent recount split reads\) from dedupplicate BAM file.

#### R1DuplicationRate

Calculated as `R1DuplicatedReads / R1MAPQFilteredReads`.

#### R1DuplicationRate \(m3C specific\)

Calculated as `(1 - R1DeduppedReads(m3c) / R1UniqueMappedReads(m3c)) * 100` .

#### R1FinalBismarkReads

Final number of R1 used in generating ALLC file in mC mode. Calculated as `R2MAPQFilteredReads - R2DuplicatedReads`. In mCT mode, reads are further filtered by mC fraction \(see [FinalDNAReads](all-mapping-metrics.md#finaldnareads).\)

#### R2MAPQFilteredReads

Number of R1 after filtering by MAPQ.

#### R2DuplicatedReads

Number of R1 that are marked as PCR duplicates.

#### R2DeduppedReads \(m3C specific\)

Number of R2 **remained** after removing PCR duplicates. Counted reads that have unique read name \(to prevent recount split reads\) from dedupplicate BAM file.

#### R2DuplicationRate

Calculated as `R2DuplicatedReads / R2MAPQFilteredReads`.

#### R2DuplicationRate \(m3C specific\)

Calculated as `(1 - R2DeduppedReads(m3c) / R2UniqueMappedReads(m3c)) * 100` .

#### R2FinalBismarkReads

Final number of R2 used in generate ALLC file in mC mode. Calculated as `R2MAPQFilteredReads - R2DuplicatedReads`. In mCT mode, reads are further filtered by mC fraction \(see [FinalDNAReads](all-mapping-metrics.md#finaldnareads).\)

#### FinalmCReads

Final number of total reads \(R1 + R2\) used in generating ALLC file. Calculated as `R1FinalBismarkReads + R2FinalBismarkReads`.

#### FinalmCReads \(m3C specific\)

Final number of total reads \(R1 + R2\) that has unique read name \(to prevent recount split reads\). Counted as `R1DeduppedReads (m3c) + R2DeduppedReads (m3c)` .

## ALLC Metrics

#### mCHmC

Total methylated cytosine in the CH context.

#### mCHCov

Total covered cytosine in the CH context.

#### mCHFrac

Calculated as `mCHmC / mCHCov`

#### mCGmC

Total methylated cytosine in the CG context.

#### mCGCov

Total covered cytosine in the CG context.

#### mCGFrac

Calculated as `mCGmC / mCGCov`

#### mCCCmC

Total methylated cytosine in the CCC context.

#### mCCCCov

Total covered cytosine in the CCC context.

#### mCCCFrac

Calculated as `mCCCmC / mCCCCov`

#### GenomeCov

Percentage of cytosine in the genome that been covered by at least one read.

## DNA and RNA Reads Separation \(mCT specific\)

#### FinalDNAReads

Number of final DNA reads that passed read-level mC fraction filtering. These reads were used in generating ALLC file.

#### SelectedDNAReadsRatio

Calculated as `FinalDNAReads / FinalmCReads`.

#### RNAUniqueMappedReads

Number of reads uniquely mapped by STAR.

#### FinalRNAReads

Number of RNA reads \(assigned to gene\) counted by featureCount

#### FinalCountedReads

Number of reads counted by featureCount.

#### SelectedRNAReadsRatio

Calculated as `FinalRNAReads / RNAUniqueMappedReads`

#### GenesDetected

Number of genes that covered by at least one read.

## Chromatin Contact \(m3C specific\)

#### CisShortContact 

Number of contact whose two ends are from the same chromosome and closer than min\_gap parameter in the MappingConfig.

#### CisLongContact

Number of contact whose two ends are from the same chromosome and further than min\_gap parameter in the MappingConfig.

#### TransContact

Number of contact whose two ends are from different chromosome.

#### TotalContacts

Calculated as `CisShortContact + CisLongContact + TransContact` .

#### CisShortRatio

Calculated as `CisShortContact / TotalContacts` .

#### CisLongRatio

Calculated as `CisLongContact / TotalContacts` .

#### TransRatio

Calculated as `TransContact / TotalContacts` .



