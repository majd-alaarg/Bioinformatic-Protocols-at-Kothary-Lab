
# Running RNASeq pipeline

## Testing nf-core and pipeline before running analysis
With nf-core downloaded and the rnaseq pipeline also installed, jobs can now be executed.

To test that nf-core and your pipeline and working, run the following individually:

-   Try running the Nextflow “hello world” example to make sure that the tools are working properly:

	`nextflow run hello `

-   To test that everything is working properly, try running the tests for your pipeline of interest in the terminal:

	`nextflow run /scratch/$USER/nf-core/<PATH TO PIPELINE> -profile test,singularity --outdir <OUTDIR>`

In my case, `<PATH TO PIPELINE>` was `nf-core-rnaseq_3.12.0/3_12_0` and `<OUTDIR>` was `/scratch/pipelinetest1`. 

Using MobaXTerm or your terminal emulator, you can browse through the file directories to your file paths.

 - So, I ran `nextflow run /scratch/$USER/nf-core/nf-core-rnaseq_3.12.0/3_12_0 -profile test,singularity --outdir /scratch/pipelinetest1`

If that's all good, you can proceed.

# Getting started

While installation and file transfers are run on gra-dtn1, jobs must be run on a computing node. Before computing, there are some files you need to upload to your working directory first.

I used [Mobaxterm](https://mobaxterm.mobatek.net/), a free software, however, others exist. It's easy-to-use and makes working on the computing cluster easy if you have no previous experience working with terminal or databases.

## Running a terminal session

Once Mobaxterm has been installed, create a new session by clicking the new tab button (+), or going **Terminal > New tab**.

To connect to the Graham cluster, you must ssh to the remote server using your DRAC username. Type into your terminal:

    ssh userName@graham.computecanada.ca
It will then prompt you for your password (Note: as you type your password, it will be hidden). Once connected, you will get a successful message.

## Tips

Using Linux is not that hard. If you ever need to do something that you don't know how to (e.g deleting a file), just Google, "How to delete a file in linux terminal."
Here are some basic commands that I saw online:
![enter image description here](https://github.com/majd-alaarg/bioInformatics/blob/28fc76aaf0fd7a51715005981cae5fcf706c693e/Assets/Linux%20Commands.png)

## Installing nf-core

Once logged into the cluster, you should install nf-core. When on the cluster, you're automatically signed into the gra-login node, for the installation process, connect to a node dedicated for file transfers, dtn-1, as follows:

    ssh gra-dtn1
Once on the node, type in **tmux**, this creates a tmux session which you can connect to by **tmux attach** if you get disconnected, allowing you to go on and off a session presumably.

To begin the download process, copy and paste the following onto your terminal:

    #create an nfcore directory
    mkdir -p /scratch/$USER/nf-core
    #cd to the new nfcore directory
    cd /scratch/$USER/nf-core
  
Contrary to the OHRI's Ottawa Bioinformatics Core's documentation available at he time, I could not use their protocol of loading a python environment to then install packages with pip due to recent updates in the nf-core pipeline. With the help of the nf-core developer teams, I developed another installation process that does the exact same thing, except with a different python loading method based on the documentation from [The Python Packaging Authority (_PyPA_)](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/).

Based on that, execute the following commands to create the environment in which you can install nf-core:

    python3  -m  venv  tutorial_env
    source  tutorial_env/bin/activate
    python3  -m  pip  install nf-core

Once that is completed, nf-core is downloaded and you now need to download the pipeline.

## Downloading pipeline

To download the pipeline, run the following: 

       nf-core download rnaseq

It will then guide you through the download process, prompting you to choose several options.

 - Select the latest pipeline revision
 - For containers, select **SINGULARITY**!!
 - Define $NXF_SINGULARITY_CACHEDIR for a shared singularity image download folder?: **Yes**
 - Select **amend** when prompted to copy singularity images to target folders.
 - Compression type: **none**
 - Default institutional configuration: **yes**


## Additional help

If you run into major issues or require help, you can consult the [nf-core documentation](https://nf-co.re/docs/usage/introduction) (click on link or just Google nf-core documentation)

If the pipeline fails, check the  [troubleshooting docs](https://nf-co.re/docs/usage/troubleshooting/)  and ask for help on the nf-core Slack channel for that particular pipeline (see  [https://nf-co.re/join](https://nf-co.re/join)).
