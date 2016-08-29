## Running cisFusion
cisFusion is a fusion gene detecter, which detects the fusion gene by comparing target samples and normal samples.

Running cisFusion is performed in the same fashion as described for cisMuton and cisCton;

```
cd /path_to/work/
perl /path_to_install_directory/qc_run.pl ${TargetSAMPLE}:${NormalSAMPLE}:${GROUP}:FUSION
```

## cisFusion Output
Running cisFusion will create following files as output in `/path_to/work/Fusion/` directory

| File name                                                                                                                   | Description                                      |
| ---                                                                                                                         | ---                                              |
| **Call.(_NormalSampleName_)/**                                                                                              |                                                  |
| (AlnTarget&amp;#x7c;AlnWexome&amp;#x7c;AlnGeneme)\_&lt;br&gt;(LmtBthside&amp;#x7c;LmtOneside)\_mq(5&amp;#x7c;10)_Single.txt | Call table with pair ends are counted separately |
| (AlnTarget&amp;#x7c;AlnWexome&amp;#x7c;AlnGeneme)\_&lt;br&gt;(LmtBthside&amp;#x7c;LmtOneside)\_mq(5&amp;#x7c;10)_Paired.txt | Call table with pair ends counted as 1           |

### Output Format

| Column                            | Description      |
| ---                               | ---              |
| Pair                              |                  |
| Call                              |                  |
| Nrmcnt_total                      | Norm count total |
| Nrmcnt_2map                       |                  |
| Nrmcnt_2map+paired                |                  |
| 2map_count                        |                  |
| 2map&amp;VF_count                 |                  |
| VF_count                          |                  |
| Paired_count                      |                  |
| OnlyVF_Prop(OnlyVF/Total)         |                  |
| OnlyVF_Prop(OnlyVF/2map)          |                  |
| OnlyVF_Prop(OnlyVF/(2map+paired)) |                  |
| MapCount_Pval                     |                  |
| GeneDepth:BiasG1G2                |                  |
| GeneDepth:TotalG1G2               |                  |
| Gene1                             |                  |
| Gene1:Breakpoint                  |                  |
| Gene1:Nrmcnt                      |                  |
| Gene1:Count                       |                  |
| Gene1:Count_SN                    |                  |
| Gene1:GeneDepth                   |                  |
| Gene2                             |                  |
| Gene2:Breakpoint                  |                  |
| Gene2:Nrmcnt                      |                  |
| Gene2:Count                       |                  |
| Gene2:Count_SN                    |                  |
| Gene2:GeneDepth                   |                  |
