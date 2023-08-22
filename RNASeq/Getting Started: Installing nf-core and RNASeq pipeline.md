

# Getting Started: Installing nf-core and RNASeq pipeline

## Introduction
[Nf-core](https://nf-co.re/) provides highly optimized bioinformatic pipelines with excellent reporting. Validated releases ensure reproducibility.
The [RNASeq pipeline](https://nf-co.re/rnaseq/3.12.0) is used.

The Digital Research Alliance of Canada's GRAHAM is a computing system that allows for powerful computing on their remote servers. Sessions can be run overnight, for long-periods of time with large resource allocation (more than 128GB of RAM, multiple processor cores etc). Account must be made on the DRAC website, after which the lab PI can add you (assuming the PI has already joined as a member). See the [DRAC website](https://alliancecan.ca/en/services/advanced-research-computing/account-management/apply-account) for more details.


# Getting started

First, you must connect/login to the Graham computing cluster via your terminal or command prompt. However, there are terminal emulator softwares that **emulate the functionalities of classic computer terminals** but make it easier by providing graphical user interface.

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

    #load version of python needed
    module load python/3.10.2
    python3  -m  venv  tutorial_env
    source  tutorial_env/bin/activate
    python3  -m  pip  install nf-core
Note: After a lot of trial and error, I found that the correct version of python needed to be manually loaded (as shown above) before creating the python environment, otherwise your process will return back an error in the final step of the installation.

Once that is completed, nf-core is downloaded and you now need to download the pipeline.

## Downloading pipeline

To download the **rnaseq** pipeline, run the following: 

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
