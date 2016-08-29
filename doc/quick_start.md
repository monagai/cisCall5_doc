# Overview
cisCall has three modules: cisMuton, cisCton, and cisFusion.
cisMuton calls point mutations (Single nucleotide variants), cisCton calls copy number amplifications (CNAs), and cisFusion detects fusion genes.

right now, it is best to use Cton of CisCall version7 and version5 for Muton and Fusion
Since Muton and Fusion of Ciscall7 is under development, this doc will be updated later.

since version5 is included in [Ciscall7 repository](https://github.com/NCCJapan/CisCall7), you can download from there at once.

# running Muton and Fusion

## Before Running
### <a name ="prepare"> I. Prepare working directory and samples

1. Create a working directory. **All of the data prepared in this chapter should be located under the working directory**.
    ```
    mkdir /path_to/work
    cd /path_to/work
    ```

2. Prepare sample files
    - cisCall will process the data labeled **Sample** in a group labeled **Group**.
    - cisCall is compatible with both `.fastq` and `.bam` as input.
    - If you want to run with multiple `.fastq` files (for biological/technical replicates), concatenate files together as follows:

    In the case of single-end
    ```
    cat sample1-1.fastq ... sample1-4.fastq &gt; /path_to/work/${SampleName}.${GroupName}.fastq
    ```

    In the case of pair-end
    ```
    cat sample1-1r1.fastq ... sample1-4r1.fastq &gt; /path_to/work/${SampleName}.${GroupName}.fastq.R1
    cat sample1-1r2.fastq ... sample1-4r2.fastq &gt; /path_to/work/${SampleName}.${GroupName}.fastq.R2
    ```

### II. Prepare prerequisite files
cisCall requires some prerequisite files for processing. Following table shows the list of prerequisite files and sources to prepare the files for analysis of hg19 samples for instance;

**Table. Prerequisite files**

| File type                     | Source                                                                                                                  | Info                                       |
| :--                           | :--                                                                                                                     | :--                                        |
| ${GROUP}.DBexome              | http://www.genome.med.kyoto-u.ac.jp/SnpDB/HGVD1208-V1_41-dbSNP137.tar.gz                                                |                                            |
| ${GROUP}.bedgraph             | http://hgdownload.cse.ucsc.edu/goldenPath/hg19/encodeDCC/wgEncodeMapability/wgEncodeDukeMapabilityUniqueness20bp.bigWig | converted from .bigWig                     |
| ${GROUP}.fasta                | hg19 genome                                                                                                             | concatenate into single fasta              |
| ${GROUP}.fusion.gene.txt      | data set of fusion gene, should be self-prepared                                                                        |                                            |
| ${GROUP}.geneName.txt         | http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/geneName.txt.gz                                                 |                                            |
| ${GROUP}.genefam_list.txt     | ftp://ftp.ebi.ac.uk/pub/databases/genenames/genefam_list.txt.gz                                                         |                                            |
| ${GROUP}.genomicSuperDups.txt | http://hgdownload.cse.ucsc.edu/goldenPath/hg38/database/genomicSuperDups.txt.gz                                         |                                            |
| ${GROUP}.hs37d5cs.fa          | http://ftp.1000genomes.ebi.ac.uk/vol1/ftp/technical/reference/phase2_reference_assembly_sequence/hs37d5cs.fa.gz         |                                            |
| ${GROUP}.refGene.txt          | http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/refGene.txt.gz                                                  |                                            |
| ${GROUP}.rmsk                 | http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/rmsk.txt.gz                                                     | remove file extension `.txt`               |
| ${GROUP}.simpleRepeat         | http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/simpleRepeat.txt.gz                                             | remove file extension `.txt`               |
| ${GROUP}.snp.dbsnp            | http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/snp138.txt.gz                                                   | edit file extension `.txt` to `.snp.dbsnp` |
| ${GROUP}.target.bed           | bed file for capture region, depend on sample kit used                                                                  |                                            |
| ${GROUP}.gene.bed             | bed file for capture region annotation                                                                                  |                                            |
| dgvMerged.txt.gz              | http://hgdownload.cse.ucsc.edu/goldenPath/hg19/database/dgvMerged.txt.gz                                                | ???                                        |
| bin/                          | (symbolic link to cisCall/bin/)                                                                                         |                                            |

- For **cisFusion**, you also require  to prepare a `fusion.bed` file, which indicate the region targeted for fusion mutation. It is a tab-deliminated file consist of four column, [Chromosome], [start position(1 base)], [end position(1 base)], and [gene name.GeneID].
e.g. `chr1	11810133	11810828	AGTRAP.57085`
- Some of the files required to be preprocessed before it is used by cisCall. Please read the INSTALL for details.

## Run

### 1. Set running parameters
Execute the following commands in the work directory;

```
perl /path_to_install_directory/Ciscall5/bin/qc_run.pl ::${GroupName}:PARAM
```

Now, the parameter setup window should be appeared. In this window;
1. Choose parameters based on the sequencing platform and sample type
2. When the edit parameter window appears, Select **2: Save**
3. When **Save param-ID** appears, Select **0: \&lt;To be automatically named&gt;**
4. When the edit parameter window reappears, Select **1: Quit** or further edit parameters if necessary

### 2. Run cisCall5

Execute the following commands will run mutation calls for SNVs (Muton) and fusion gene detection (Fusion);

```
perl /path_to_install_directory/Ciscall5/bin/qc_run.pl ${TargetSampleName}:${NormalSampleName}:${GroupName}:MUTON, FUSION
```

e.g. if your target_sample.fastq file named **target.EXAMPLE.fastq** and normal_sample.fastq file named **normal.EXAMPLE.fastq**, then the command should be as follows;

```
perl /path_to_install_directory/bin/qc_run.pl target:normal:EXAMPLE:MUTON, CTON, FUSION
```

# Running Cton

[Prepare data as same as Muton and Fusion](#prepare) in e.g.`path/to/data/`. additionary, download following data to same directory.

*

and run following command.

```
python /path_to_install_directory/src/ciscall.py -a 'CTON' \
    -d path/to/data \
    -m "path/to/samtools" \
    -b "path/to/bigWigtobedGraph" \
    "/path/to/tumor_sample.bam" \ # it will be "output/${TargetSampleName}.${GroupName}.MUTON.TARGET/common.fastq.aln.bam" if you have already run Muton before
    "/path/to/normal_sample.bam" # it will be "output/${NormalSampleName}.${GroupName}.MUTON.TARGET/common.fastq.aln.bam" if you have already run Muton before
    -p "{GroupName}"
```

- It would takes time to complete process for the first run because cisCall will create index file for some reference files.
- cisCall is able to run SNVs, CNAs calls and fusion genes detection independently, also with several optional process. Please read cisCall Options for more detail.
