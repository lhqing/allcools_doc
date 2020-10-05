---
description: Important mapping metrics for evaluating cell quality
---

# Key Mapping Metrics

## snmC-seq 2/3

Below is the minimum mapping metric I used to evaluate cell and library quality before any computational analysis is done. The numbers here related to how the library is sequenced, I gave this number based on loading 16 plates \(3072 wells\) in a MiSeq run or a NovaSeq run using S4 flowcell. If your library is loaded differently \(e.g., 32 plates in a NovaSeq run using S4 flowcell\), you need to change the cutoffs accordingly.

* [FinalmCReads](all-mapping-metrics.md#finalmcreads), this is the final number of reads used in methylation calling, therefore, represents the real genome coverage.
  * MiSeq cutoff: FinalmCReads &gt; 100
  * NovaSeq cutoff: FinalmCReads &gt; 500,000
  * The library average is ~1.6 M reads/cell. 
* [mCCCFrac](all-mapping-metrics.md#mcccfrac), this is the upper bound of non-conversion rate. mCCC fraction is usually close to the non-conversion rate measured by lambda DNA spike-in, but it is positively correlated with the cell's mCH fraction, therefore, can be a bit higher in cells with high mCH \(e.g., some inhibitory neurons\). Therefore, I recommend using different thresholds for neurons and other tissues:
  * For neuronal related sample, use mCCC fraction &lt; 0.03
  * For other tissue that known to have low mCH fraction, use mCCC fraction &lt; 0.01
* [R1MappingRate](all-mapping-metrics.md#r-1-mappingrate), this metric is species-specific, the library average usually between 65% - 75%. I use R1MappingRate &gt; 50% as the cutoff. A low mapping rate indicates potential contamination.
* [R2MappingRate](all-mapping-metrics.md#r-2-mappingrate), this metric is lower than R1MappingRate, because the R2 base quality is not as good as R1, the average is usually 10% lower than R1 \(but highly correlated\).
* R1\(R2\)DuplicationRate, the library average usually between 25% - 35%. I do not filter cells based on this metric. 
* Overall success rate: after filtering by FinalmCReads, mCCCFrac, R1MappingRate, we usually got ~80% wells \(or cells\) remaining. The success rate between MiSeq and NovaSeq should be very close. **If the MiSeq success rate is below 65% \(&lt; 2000 success in a total of 3072\), I do not recommend proceeding to NovaSeq.** There must be some quality issues either during FACS or due to the library preparation.

## snmCT-seq

## snm3C-seq



