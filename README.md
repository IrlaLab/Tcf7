# Tcf7 controls thymic function by regulating core transcriptional programs in thymic epithelial cells

## Article information

**Title:** HTcf7 controls thymic function by regulating core transcriptional programs in thymic epithelial cells

**Authors:** 
Romain Trubert1, Adrien Meraud1, Jérémy Santamaria1, Ismaël Malki1, Raphaël Corre1, Matthieu Giraud2, Arnauld Sergé3, Magali Irla1* 

1 Center of Immunology of Marseille Luminy (CIML), INSERM, CNRS, Aix-Marseille-University, 13288, Marseille, France.
2 Nantes Université, INSERM, Center for Research in Transplantation and Translational Immunology, UMR 1064, Nantes, France.
3 Laboratoire adhésion inflammation (LAI),Turing Centre for Living Systems, CNRS, INSERM, Aix-Marseille University, 13288, Marseille, France.

& Corresponding author: Magali Irla (Magali.Irla@inserm.fr)

**Summary:**
The transcription factor Tcf7 (T cell factor 7) is essential for T-cell development in the thymus by controlling T-cell lineage commitment, thymocyte survival and differentiation. Nevertheless, its role in other thymic cell types is less well defined. Here, we found that Tcf7 is upregulated in mature medullary thymic epithelial cells (mTECs) during interactions with autoreactive CD4+ thymocytes. Using a conditional mouse model, we show that Tcf7 in TEC controls T-cell production and selection by regulating mTEC cellularity and differentiation into Aire+ mTEC and specific mimetic subsets. Transcriptomic analyses revealed that Tcf7 governs core mTEC transcriptional programs by regulating Foxn1, its downstream targets, and tissue-restricted antigen (TRA) expression. TEC-specific deletion of Tcf7 promoted signs of autoimmune manifestations and rescued melanoma-specific T cells through impaired melanoma-associated TRA, enhancing tumor eradication. These findings identify Tcf7 as a key regulator of mTEC differentiation and function required to establish a self-tolerant T cell repertoire.

**DOI:**

---

---

## Goal of the GitHub
This GitHub project contains the instructions and materials to reproduce the analyses reported in the article (and more).
Source code (scripts and dockerfile) are available in the GitHub repository. Processed data, analysis results, and built Docker/Singularity images are available for download from Zenodo. Instructions to reproduce the analyses are provided below.

---

## Description of the datasets

As described in the article, there are 2 libraries in this study, each of which has been sequenced in paired-end , generating 4 files.

The libraries are the result of the composition of two genotypes (WT and Tcf7KO).

A dataset name contains the information required to identify it uniquely as follows:
```
[EXPERIMENT]_[CONDITION]_[STRAND]
```

where:

 * EXPERIMENT is GEX_TEC
 * CONDITION is one of "WT" and "TCF7KO"
 * STRAND is one of R1 or R2


| Dataset name | title | genotype	| description
| :--------------- |:--------------- |:-------|:-------|
| GEX_TEC_TCF7KO_S2_R1_001	| Mus Musculus C57BL/6 J TEC Tcf7KO forward reads (mouse age: 6 weeks)
| GEX_TEC_TCF7KO_S2_R1_001	| Mus Musculus C57BL/6 J TEC Tcf7KO reverse reads (mouse age: 6 weeks)
| GEX_TEC_TCF7WT_S1_R1_001	| Mus Musculus C57BL/6 J TEC Control forward reads (mouse age: 6 weeks)
| GEX_TEC_TCF7WT_S1_R2_001	| Mus Musculus C57BL/6 J TEC Control reverse reads (mouse age: 6 weeks)

---

## Description of the main analysis

During the analysis process of the datasets, several steps were applied to combine and merge the datasets. Here is a quick description.

### First step : Individual dataset analysis

All the datasets were analyzed separately to validate their quality and get a first insight into the cell heterogeneity. 

The analysis code and analysis results for this step are in folders with the dataset name.

### Second step : Merge all datasets

All the datasets were merged together to compare condition effects.

The analysis code and analysis results for this step are in a folder called Integrated.

---

## Structure of the data and code

### Folders of the datasets

The project is organized by dataset. Each dataset has its own folder. Due to the analysis steps described above, when downloading the code and data (see below), you will obtain several sub-folders with names as below:

```
.
└── Tcf7
    ├── Tcf7WT_sc
    ├── Tcf7KO_sc
    └── Integrated
``` 

### Folders inside the datasets

Each dataset folder contains an ordered series of sub-folders. Theses sub-folders are organized in two sets : the code and the data and analysis results.

 * From the GitHub, you will be able to download the code set of files. It contains the analysis code (__03_Scripts__) and the Docker container definition file (__02_Container__). Some dataset also contains a Snakemake workflow definition (__04_Worflow__). For instance : 

```
.
└── Tcf7
    ├── Tcf7WT_sc
    │   ├── 02_Container
    │   ├── 03_Scripts
```

 * From Zenodo, you will be able to download the data and analysis results set of files. It contains the compiled docker images (_02_Container__) and the analysis results (05_Output)
 
```
.
└── Tcf7
    ├── Tcf7WT_sc
    │   ├── 02_Container
    │   ├── 05_Output
```

---
---

## Prepare the environments

In order to prepare the environment for analysis execution, it is required to:

- Clone the GitHub repository and set the WORKING_DIR environment variable
- Download the data
- Install the Docker environment to run the analysis interactively

Below you will find detailed instruction for each of these steps.

---

#### Clone the GitHub repository

Use you favorite method to clone this repository in a chosen folder. This will create a folder **Tcf7** with all the source code.

#### Set the Working Dir variable

Then, you must set an environment variable called **WORKING_DIR** with a value set to the path to this folder.

For instance, if you have chosen to clone the Git repository in __"/home/malki/workspace"__, then the **WORKING_DIR** variable will be set to __"/home/malki/workspace/Tcf7"__

**On linux:**

```
    export WORKING_DIR=/home/malki/workspace/Tcf7
```

#### Add your working dir in the code

The code uses variables that are stored in different "parameters" file. One important variable is the PATH_PROJECT which indicate to the code where your project is stored.
You have to modify this variable in the code to reflect your project setup. Each dataset has a file called **analysisParams.R** in the subfolder **03_Scripts**

For instance:

```
    Tcf7
    │
    ├── Tcf7WT_sc
    │   │
    │   └── 03_Script/analysisParams.R

```

Edit those files and in each of them locate the line defining the **PATH_PROJECT** variable and change its value to the same value as the **WORKING_DIR** variable you defined before. Then save the files.

```
PATH_PROJECT = "/home/malki/workspace/Tcf7"
```

---

### Download the data

The raw FASTQ files are available on GEO. The rest of the data are available on Zenodo :

- Tcf7_All_samples (lien zenodo) : All samples


Download the folders into WORKING_DIR, in order to keep the correct folder structure.

#### Download the analysis result

The analysis results can be found in the folder called "05_Output" in each dataset folder. These subfolders contains a series of subfolders, one for each analysis step. The same subfolders can be found in the 03_Scripts subfolders, since the analysis code and the analysis output have a bijective relation. 

**Note :** the analysis results contain also the Cell Ranger pre-processing results (including the count matrix and the bam files).

For instance:

```
    Tcf7
    │
    ├── Tcf7WT_sc
        └── 03_Script
            ├── 00_CellRanger
            └── 01a_GlobalHeterogeneity

```

#### Download the container images

The container images (tar.gz file for Docker and sif file for Singularity) can be found in the 02_Container sub-folder of each dataset folder. Singulairty images can be use directly while docker images must be loaded on your system (see below)

---

### Install the Docker environment to run the analysis interactively

#### Install Docker

You need install Docker on your system to take advantage of interactive analysis environment with Rstudio, follow the instructions here : https://docs.docker.com/get-docker/


#### Load the images

Once done, locate the tar.gz files of the docker images and use the following command

```
docker load -i <image_name>.tar.gz
```

#### Run the analysis individually using Docker

If you have loaded the docker images (see above), you can use Rstudio in Docker to run the analysis individually.

To start a docker container, use the following command:

```
docker run -d -p 8787:8787 -v /$WORKING_DIR:/$WORKING_DIR -e PASSWORD=<PASSWORD> -e USER=$(whoami) -e USERID=$(id -u) -e GROUPID=$(id -g)  <IMAGE_NAME>
```

where:

* <PASSWORD> is a simple string you will use as password to login into Rstudio
* <IMAGE_NAME> is the Docker image name to run

One started, you can open an internet browser and use the URL https://127.0.0.1:8787.

At the login prompt, enter the name of the user session you are connected with and the password you type in place of <PASSWORD>. You are now in a Rstudio environment and the container is able to connect to the **WORKING_DIR**
of your system. Inside you will find the project files. To tun the analysis, look at the scripts "launch_report.R" that is the main entry point to run the analysis.

