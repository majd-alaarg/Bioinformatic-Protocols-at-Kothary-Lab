


# Bioinformatics Protocols at Kothary Lab

The following repository contains the protocols and logs of bioinformatics use in the Kothary Lab. Includes installation processes, pipeline configurations, test logs and outputs of bioinformatic processes/experiments run. Main contents is RNASeq analysis, conducted on Graham Cluster from DRAC.

Author: Majd Al-Aarg

Date of creation: August 21, 2023

Contact: majd.alaarg@gmail.com 


# Table of Contents (RNASeq)
1. [Getting Started: Installing nf-core and RNASeq pipeline](https://github.com/majd-alaarg/Bioinformatic-Protocols-at-Kothary-Lab/blob/main/RNASeq/Guides/Getting%20Started%3A%20Installing%20nf-core%20and%20RNASeq%20pipeline.md)
2.  [Downloading Data from The Centre for Applied Genomics Portal (TCAG)](https://github.com/majd-alaarg/Bioinformatic-Protocols-at-Kothary-Lab/blob/1a8fcb7e59a4c5da75ac4fa32cc6ee53c7118d85/RNASeq/Guides/Downloading%20Data%20from%20The%20Centre%20for%20Applied%20Genomics%20Portal%20(TCAG).pdf)
3. [Running RNASeq pipeline](https://github.com/majd-alaarg/Bioinformatic-Protocols-at-Kothary-Lab/blob/main/RNASeq/Guides/Running%20RNASeq%20pipeline.md)

# Projects/Experiments Run
| Project/Pipeline Name                                                               | Date run        | Description                                                                                              |
|-------------------------------------------------------------------------------------|-----------------|----------------------------------------------------------------------------------------------------------|
| [Investigation of Liver Intrinsic Defects in  Spinal Muscular Atrophy (Rerun Aug.27)](https://github.com/majd-alaarg/Bioinformatic-Protocols-at-Kothary-Lab/tree/main/RNASeq/Projects/Investigation%20of%20Liver%20Intrinsic%20Defects%20in%20Spinal%20Muscular%20Atrophy%20(Rerun%20Aug.27)) | August 27, 2023 | Rerun of nf-core rnaseq pipeline initially  conducted by OBCF to test functionality/reproducibility of updated protocol. DESeq2 analysis for differential gene expression completed, troubleshooting for adding/matching gene names and gene id to final datasheet.|
|                                                                                     |                 |                                                                                                          |
|                                                                                     |                 |                                                                                                          |



## Additional help

If you run into major issues or require help, you can consult the [nf-core documentation](https://nf-co.re/docs/usage/introduction) (click on link or just Google nf-core documentation)

If the pipeline fails, check the  [troubleshooting docs](https://nf-co.re/docs/usage/troubleshooting/)  and ask for help on the nf-core Slack channel for that particular pipeline (see  [https://nf-co.re/join](https://nf-co.re/join)).

### Acknowledgment
The rnaseq protcol in this repository are based on a [guide from the Ottawa Bioinformatics Core Facility (as of Aug. 21)](https://gitlab.com/ohri/obcf-documentation/-/blob/a6394dbc256054447e1a3478e8503b4e16f0f762/Files/nfcore-rnaseq-graham-HOWTO.md) that I redeveloped specifically for the Kothary Lab operations/experiments and to account for the changes in the Nextflow nf-core system at the time.

Current OBCF repository (for additional reference): [https://gitlab.com/ohri/obcf-documentation/-/blob/master/Files/nfcore-rnaseq-graham-HOWTO.md](https://gitlab.com/ohri/obcf-documentation/-/blob/master/Files/nfcore-rnaseq-graham-HOWTO.md)
