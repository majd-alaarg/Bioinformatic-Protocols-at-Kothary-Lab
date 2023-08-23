
# Running RNASeq pipeline
With nf-core downloaded and the rnaseq pipeline installed, jobs can now be executed.

Remember to always start a tmux session when you connect to the login page.

## Testing nf-core and pipeline before running analysis


To test that nf-core and your pipeline are working, run the following tests individually:  
-   Try running the Nextflow “hello world” example to make sure that the tools are working properly:

	`nextflow run hello `

-   To test that everything is working properly, try running the tests for your pipeline of interest in the terminal:

	`nextflow run /scratch/$USER/nf-core/<PATH TO PIPELINE> -profile test,singularity --outdir <OUTDIR>`

**Using MobaXTerm or your terminal emulator, you can browse through the file directories to your file paths.** 

In my case, `<PATH TO PIPELINE>` was `nf-core-rnaseq_3.12.0/3_12_0` and `<OUTDIR>` was `/scratch/pipelinetest1`. 

So, I ran:
 - ``nextflow run /scratch/$USER/nf-core/nf-core-rnaseq_3.12.0/3_12_0
   -profile test,singularity --outdir /scratch/pipelinetest1``

If that's all good, you can proceed.

# Preparation for pipeline: Uploading precursor files and configuration

While installation and file transfers are run on gra-dtn1, jobs must be run on a computing node. However, before computing, there are some files you need to upload to your working directory first. While in a computing node, I couldn't upload these files so make sure you are still in the `gra-dtn1` node.

### Uploading FASTQ files
Create a working directory for your project (I had to create it in scratch because I kept receiving an error that `DISK QUOTA EXCEEDED`-- scratch gets automatically purged by the cluster after 40-60 days so make sure to download everything once everything is completed or move to the project folder).

**Making project folder**

    #cd to scratch directory
    cd /scratch/$USER/
    #create a new working directory for your project
    mkdir -p /scratch/$USER/<DESIRED NAME>
    
**Uploading FASTQ files**
Before uploading your FASTQ files, it is assumed they were already downloaded.

To download our data, which was sequenced by SickKids and stored in The Center of Applied Genomics Portal, I used their Command Line Interface. For more information/help downloading files from TCAG using CLI, see the ****Downloading from TCAG Protocol****.

Once downloaded to an external hard drive (or your personal computer if you had enough space for 200gb worth files), use the `scp` command in terminal to upload the files.

    scp -r /path/to/local/directory userName@remote:/path/to/directory

In my case, where files were stored on an external hard drive, I did the following:

    scp -r D:\RNASEQDATA userName@graham.computecanada.ca:/scratch/$USER/rnaSeqProject

This step takes time and you must ensure that your device remains powered on.

## Samplesheet generation python script
Once you have all of your fastq files downloaded into a working directory, you need to create a configuration file in the form of a samplesheet to tell the pipeline the relationship between the files and how to process them.

There exists a python script, provided by nf-core, to automatically create a samplesheet based on the files in your working directory.

`curl https://raw.githubusercontent.com/nf-core/rnaseq/master/bin/fastq_dir_to_samplesheet.py > fastq_dir_to_samplesheet.py`
 
 I then ran the script as follows:
 
 ``python fastq_dir_to_samplesheet.py --strandedness="reverse" --read1_extension="_R1_001.fastq.gz" --read2_extension="_R2_001.fastq.gz" `pwd` samplesheet.csv``
 
The --read1 and --read2 extension parameters I wrote are based on the suffixes of sequencing files provided by The Centre for Applied Genomics (TCAG).

Resulting in the following output for our experiment:
![enter image description here](https://github.com/majd-alaarg/Bioinformatic-Protocols-at-Kothary-Lab/blob/main/Assets/RNASEQ%20Samplesheet%20output.png)

See [additional information](#python) for more.

## Uploading Gencode annotations
I then downloaded the latest version of the GENCODE annotations for mice (**MAKE SURE YOU ALIGN TO MOUSE GENOME, I accidentally aligned to human at first**).

You can see the latest release [here](https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_mouse/latest_release/). (vM33 at the time of writing this).

    wget https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_mouse/release_M33/gencode.vM33.basic.annotation.gtf.gz
    #unzip
    gunzip gencode.vM33.basic.annotation.gtf.gz
    
    wget https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_mouse/release_M33/GRCm39.primary_assembly.genome.fa.gz
    #unzip
    gunzip GRCm39.primary_assembly.genome.fa.gz

### Uploading OBCF config files
For the configuration, aside from nf-core/rnaseq default config, I also used a config file provided by the OBCF.

    curl https://gitlab.com/ohri/obcf-documentation/-/raw/master/Files/obcf-graham.cfg > obcf-graham.cfg

## Starting computing session 

The cluster has dedicated nodes for specific tasks; for analysis, we want to attach to a computing node using the slurm manager.

To attach to a computing node, you must specify the parameters, specifically under which account, how much memory (RAM), time, and processing cores.

At the time, with the large experiment we had, I specified 96G of memory, 12 cores and 24:00:00. Always set the time as the max, 24:00:00, as you don't want a job cut short.

So, login to a computing node, I run the following:

    salloc --account=def-rkothary --mem=96G --time=24:00:00 -c 14

It takes time for the resources to be allocated.

## Running analysis pipeline
Once connected to the computing node, load the necessary tools:

    module load python/3.10.2
    module load StdEnv/2020
    module load nextflow/22.10.6
    module load apptainer/1.1
    module load java/13.0.2

Giving Nextflow the needed parameters:

    export SLURM_ACCOUNT=def-rkothary
    export SALLOC_ACCOUNT=$SLURM_ACCOUNT
    export SBATCH_ACCOUNT=$SLURM_ACCOUNT

Ensuring default directories are good:

    #ensure that the temporary directory used by nf-core is the one provided by the SLURM session
    export TMPDIR=$SLURM_TMPDIR
    #ensure that the session information is cached in your scratch directory 
    NXF_SINGULARITY_CACHEDIR=/scratch/$USER/nf-core/

**STARTING RNASEQ PIPELINE**

    NXF_SINGULARITY_CACHEDIR=/scratch/$USER/nf-core/
    nextflow run /scratch/$USER/nf-core/nf-core-rnaseq_3.12.0/3_12_0 \
        	--input samplesheet.csv \
        	--outdir nfcore-results \
        	-c obcf-graham.cfg \
        	--gtf $NXF_SINGULARITY_CACHEDIR/gencode.vM33.basic.annotation.gtf \
        	--fasta $NXF_SINGULARITY_CACHEDIR/GRCm39.primary_assembly.genome.fa \
        	--gencode
        	
Above, it is assumed that your samplesheet is called `samplesheet.csv`, your configuration file is called `obcf-graham.cfg`(the configuration file provided by the OBCF at the OHRI) , and your gencode annotations are named as above.


## Additional information

### <a id=python></a> RNASEQ Configuration using python script
As per the [OHRI OBCF documentation](https://gitlab.com/ohri/obcf-documentation/-/blob/master/Files/nfcore-rnaseq-graham-HOWTO.md?ref_type=heads): 
-   `sample` is the sample identifier. The same identifier should be used for every fastq file associated with a specific sample, so there can be multiple lines with the same name but different fastq file references. There may be multiple fastq files for a given sample e.g. when there are multiple lanes, files may be named like `590934_S28_L001_R1_001.fastq.gz` where `L001` indicates lane 1. The sample identifiers will be used in reports and tables generated by `nf-core/rnaseq` so it should be distinct and informative.
-   `fastq_1` is the filename of the read 1 fastq file. If the sample sequencing is single ended, that will be the only file and if paired end there will be a second file described by the next column. Read 1 files usually have `R1` in the filename as with the example above or `_1.fastq.gz` suffix.
-   `fastq_2` is empty if the sample sequencing is single ended (so no text at all between the delimiting commans), and read 2 if it is paired ended; this will be a file of the same name as the R1 file with only read identifier differing.
-   `strandedness` indicates the sequencing strand orientation. For Illumina and BGI this is usually `reverse`.

## Tips

Using Linux is not that hard. If you ever need to do something that you don't know how to (e.g deleting a file), just Google, "How to delete a file in linux terminal."
Here are some basic commands that I saw online:
![enter image description here](https://github.com/majd-alaarg/bioInformatics/blob/28fc76aaf0fd7a51715005981cae5fcf706c693e/Assets/Linux%20Commands.png)

