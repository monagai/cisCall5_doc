## Running cisCton
cisCton is a copy number amplifications (CNAs) caller, which detects the CNAs by comparing target samples and normal samples.

Running cisCton is performed in the same fashion as described for cisMuton;

```
cd /path_to/work/
perl /path_to_install_directory/qc_run.pl ${TargetSAMPLE}:${NormalSAMPLE}:${GROUP}:CTON
```

## cisCton Output
Running cisCton will create following files as output in `/path_to/work/Cton/` directory

| File name                                               | Description                       |
| ---                                                     | ---                               |
| **intersect/**                                          |                                   |
| (_TargetSampleName_)-(_NormalSampleName_)_intersect.tsv | Detection of CNV                  |
| (_TargetSampleName_).exonlrr.pdf                        | Copy Number Ration in exon region |
| (_NormalSampleName_).gccnv.pdf                          | Distribution of GC contents       |


### Output Format

| Column                          | Description                                                                                                                                          |
| ---                             | ---                                                                                                                                                  |
| Chr                             | Chromosome Name                                                                                                                                      |
| Start                           | Start position (1-based)                                                                                                                             |
| End                             | End position (1-based)                                                                                                                               |
| amp/del                         | Specify if it is amplification or deletion                                                                                                           |
| Type                            | Specify calling type:&lt;br&gt;_ExomeCNV called ExomeCNV_&lt;br&gt;_Varscan called Varscan_&lt;br&gt;_Intersection called both varscan and exomeCNV_ |
| Fragment                        | Fragment ID                                                                                                                                          |
| DuplicateFlg(Mn:M=Prev, N=Next) |                                                                                                                                                      |

In addition to a tabular output format, the cisCton output plot for genome wide CNAs copy number ration is also available.
