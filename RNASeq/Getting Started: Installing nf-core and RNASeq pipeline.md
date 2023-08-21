
# Getting Started: Installing nf-core and RNASeq pipeline

## Introduction
[Nf-core](https://nf-co.re/) provides highly optimised bioinformatic pipelines with excellent reporting. Validated releases ensure reproducibility.
The [RNASeq pipeline](https://nf-co.re/rnaseq/3.12.0) is used.

The Digital Research Alliance of Canada's GRAHAM is a computing system that allows for powerful computing on their remote servers. Sessions can be run overnight, for long-periods of time with large resource allocation (more than 128GB of RAM, multiple processor cores etc). Account must be made on the DRAC website, after which the lab PI can add you (assuming the PI has already joined as a member. See the [DRAC website](https://alliancecan.ca/en/services/advanced-research-computing/account-management/apply-account) for more details.


# Getting started

First, you must connect/login to the Graham computing cluster via your terminal or command prompt. However, there are terminal emulator software that **emulate the functionalities of classic computer terminals** but make it easier by providing graphical user interface.

I used [Mobaxterm](https://mobaxterm.mobatek.net/), a free software, however, others exist. It's easy-to-use and makes working on the computing cluster easy if you have no previous experience working with terminal or databases.

## Running a terminal session

Once Mobaxterm has been installed, create a new session by clicking the new tab button (+), or going **Terminal > New tab**.

To connect to the Graham cluster, you must ssh to the remote server using your DRAC username. Type into your terminal:

    ssh userName@graham.computecanada.ca
It will then prompt you for your password. Once connected, you will get a successful message.

## Tips

Using Linux is not that hard. If you ever need to do something that you don't know how to (e.g delting a file), just Google, "How to delete a file in linux terminal."
Here are some basic commands that I saw online:
![enter image description here](https://github.com/majd-alaarg/bioInformatics/blob/28fc76aaf0fd7a51715005981cae5fcf706c693e/Assets/Linux%20Commands.png)

## Rename a file

Once logged into the cluster, you should install nf-core. When on the cluster, you're automatically signed into the gra-login node, for the installation process, connect to a node dedicated for file transfers, dtn-1, as follows:

    ssh gra-dtn1
   Once on the node, type in **tmux**, this creates a tmux session which you can connect to by **tmux attach** if you get disconnected, allowing you to go on and off a session presumably.

To begin the download process, copy and paste the following onto your terminal:

    #create an nfcore directory
    mkdir -p /scratch/$USER/nf-core
    #cd to the new nfcore directory
    cd /scratch/$USER/nf-core
  
  Contrary to the OHRI's Ottawa Bioinformatics Core's documentation, I could not use their method of loading a python environment to then install packages with pip. With the help of the nf-core developer teams, I developed another installation process that does the exact same thing, except with a different python loading method based on the documentation from [The Python Packaging Authority (_PyPA_)](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/).

Based on that, execute the following commands to create the environment in which you can install nf-core:

    python3  -m  venv  tutorial_env
    source  tutorial_env/bin/activate
    python3  -m  pip  install nf-core

It will then guide you through the download process, prompting you to choose several options.

 - Select the latest pipeline revision
 - For containers, select **SINGULARITY**!!
 - Select **copy** when prompted to copy singularity images to target folders.
 - Compression type: **none**
 - Default institutional configuration: **yes**

## Delete a file

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## Export a file

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.
