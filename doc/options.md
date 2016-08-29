## cisCall Options
cisCall is able to execute the mutant calling with several optional process by adding arguments to running command:

### 1. Remove adaptors
Removing adaptors from reads should be done before running any calling/detecting modules, and this is capable with cisCall by running with argument `RMADP`. This creates fastq files with the -RA suffix, which adaptors have been removed, as output. The files with the -RA suffix should be used as input for cisCall.

e.g. To remove adaptors from both foreground and background files:

```
perl /path_to_install_directory/bin/qc_run.pl ${TargetSampleName}::${GroupName}:RMADP
perl /path_to_install_directory/bin/qc_run.pl ${NormalSampleName}::${GroupName}:RMADP
```

### 2. Remove duplications
Option `DUP` removes duplications from foregroud (TargetSample) files, and option `DUP_BG` removes duplications from background (NormalSample) files.

e.g. To run cisMuton and remove duplications from both foreground and background samples:

```
$ perl /path_to_install_directory/bin/qc_run.pl ${TargetSampleName}:${NormalSampleName}:${GroupName}: MUTON, DUP, DUP_BG
```

### 3. Alignment option
Option `TARGET` will instruct mapper (BWA) to map the reads in targeted region, specified by target.bed. Without `TARGET` option, mapper will align the read onto whole reference genome (equivalent to add option `GENOME`).
