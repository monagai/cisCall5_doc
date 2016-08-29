## Running cisMuton
cisMuton is a point mutation caller, which detects the SNVs by comparing target samples and normal samples.

To run the cisMuton, execute the following commands;

```
cd /path_to/work/
perl /path_to_install_directory/qc_run.pl ${TargetSAMPLE}:${NormalSAMPLE}:${GROUP}:MUTON
```

if several normal samples are given, cisMuton selects the most similar sample to the target sample, considering the correlating value;

**EXAMPLE**
If you have `target1.group3.fastq` `normal1.group3.fastq` `normal2.group3.fastq` `group3.fa` `group3.target.bed` in working directory, execute following command to run the cisMuton with most simlar normal sample;

```
perl /path_to_install_directory/qc_run.pl target1:normal1:normal2:group3:MUTON, TARGET
```

## cisMuton Output
Running cisMuton will create following files as output in `/path_to/work/Muton/` directory

| File name                                           | Description                                |
| ---                                                 | ---                                        |
| **Call.(_NormalSampleName_)/**                      |                                            |
| **info.filter/**                                    | Call table with filters                    |
| call.case[0-9].txt                                  | Call table                                 |
| call.case[0-9].txt.vcf                              | Call table(vcf format)                     |
| **CallQC.Filter.Fisher/**                           |                                            |
| M01.PValue.hist.pdf                                 | Distribution of chisq.test p value         |
| M01.PValue.qq.pdf                                   | qq plot of chisq.test p value              |
| M01.VFreqRation.hist.pdf                            | Distribution of proportion ratio           |
| **CallQC.Filter.StrandBias/**                       |                                            |
| Proportion.depth300.fg.pdf                          | Distribution of strand bias over depth 300 |
| **CallQC.VFreq.M03_wLeesVAF.(_NormalSampleName_)/** |                                            |
| M03A.Variant-Propotion.snv.1.case1.pdf              | Distribution of SNV mutation rate          |
| M03A.Variant-Propotion.indel.1.case1.pdf            | Distribution of INDEL mutation rate        |

### Output Format

| Column                                                      | Description                                                |
| ---                                                         | ---                                                        |
| Chr                                                         | Chromosome Name                                            |
| Start                                                       | Start position (1-based)                                   |
| End                                                         | End position (1-based)                                     |
| Reference                                                   | Reference nucleotide/sequence                              |
| Variant                                                     | Variant nucleotide                                         |
| FPscore                                                     |                                                            |
| VFreqRatio                                                  |                                                            |
| VariantFreq                                                 | Variant allel frequency                                    |
| DelPivotPosInsertion                                        |                                                            |
| Depth:FG                                                    | Depth of Foreground                                        |
| Depth:BG                                                    | Depth of Background                                        |
| &amp;#x7c;C&amp;#x7c;G&amp;#x7c;T&amp;#x7c;D&amp;#x7c;I:FG  | Nucleotide counts for this position in the foreground file |
| A&amp;#x7c;C&amp;#x7c;G&amp;#x7c;T&amp;#x7c;D&amp;#x7c;I:BG | Nucleotide counts for this position in the background file |
| Homopolymer:Length                                          |                                                            |
| CopyNumber:Ratio                                            | Copy number ration defined as counts_tumor/count_normal    |
| Variant SNP:MajorAlleleFreq                                 |                                                            |
| DBSnp                                                       | Variant info in DBsnp                                      |
| JPSnp                                                       | Variant info in JPsnp                                      |
| RepeatMasker                                                |                                                            |
| SimpleRepeat                                                |                                                            |
| Regions syn_nonsyn                                          |                                                            |
| Gene                                                        |                                                            |
| RNA                                                         |                                                            |
| ljb_pp2 ljb2_ma ljb2_fathmm                                 |                                                            |
| Score_of_segmental_duplications                             |                                                            |
| 1stRNA 1stRNA:ChangeRNA                                     |                                                            |
| 1stRNA:ChangeProtein                                        |                                                            |
| AAChange.refGene                                            |                                                            |
