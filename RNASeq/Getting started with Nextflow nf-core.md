# Getting started with Nextflow's nf-core for RNASeq
## Introduction
[Nf-core](https://nf-co.re/) provides highly optimised bioinformatic pipelines with excellent reporting. Validated releases ensure reproducibility.
The [RNASeq pipeline](https://nf-co.re/rnaseq/3.12.0) is used.

The Digital Research Alliance of Canada's GRAHAM is a computing system that allows for powerful computing on their remote servers. Sessions can be run overnight, for long-periods of time with large resource allocation (more than 128GB of RAM, multiple processor cores etc). Account must be made on the DRAC website, after which the lab PI can add you (assuming the PI has already joined as a member. See the [DRAC website](https://alliancecan.ca/en/services/advanced-research-computing/account-management/apply-account) for more details.


# Getting started

First, you must connect/login to the Graham computing cluster via your terminal or command prompt. However, there are terminal emulator software that **emulate the functionalities of classic computer terminals** but make it easier by providing graphical user interface.

I use [Mobaxterm](https://mobaxterm.mobatek.net/), a free software, however, others exist. It's easy-to-use and makes working on the computing cluster easy if you have no previous experience working with terminal or databases.

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

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

## Delete a file

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## Export a file

You can export the current file by clicking **Export to disk** in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.
