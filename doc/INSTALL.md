## Required Environment
Target OS: Linux
Following environments are required:
- Bash
- Java
- Perl
- Python(3.4=<)
- R(3.1=<)

## Required Packages

To run cisCall, following package tools are required:
- BWA
- Cutadapt
- Cython
- Samtools
- VarScan

In addition to above, following package tools are also required for each calling modules;
- **cisMuton**
    - Annovar
    - R packages
        - KernSmooth
        - MASS
        - RPMM
        - VGAM
- **cisFusion**
    - R packages
        -exactRankTests
- **cisCton**
    - R packages
        - coin
        - parallel
        - VGAM
        - grDevices
    - [bigWigtobedGraph](https://genome.ucsc.edu/goldenpath/help/bigWig.html)

## to install CisCall

just clone the repository.

```
git clone https://github.com/NCCJapan/CisCall7
```
