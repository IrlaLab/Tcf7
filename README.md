# Tcf7 controls thymic function by regulating core transcriptional programs in thymic epithelial cells

## Article information

**Title:** Tcf7 controls thymic function by regulating core transcriptional programs in thymic epithelial cells

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

## Overview
This repository provides all scripts and supporting resources required to reproduce the single-cell analyses presented in the manuscript. It includes the analysis code, container definitions, and detailed instructions for reproducing each computational step. Processed datasets, generated outputs, and pre-built Docker and Singularity images are distributed through Zenodo.

---

## Description of the datasets

The study includes two sequencing libraries generated from paired-end sequencing, resulting in four FASTQ files.

These libraries correspond to two experimental conditions representing different genotypes: WT and Tcf7KO.

Each dataset follows the naming convention:

```
[EXPERIMENT]_[CONDITION]_[STRAND]
```
where:

 * EXPERIMENT = GEX_TEC
 * CONDITION = WT or TCF7KO
 * STRAND = R1 (Read 1) or R2 (Read 2)


| Dataset name | title | genotype	| 
| :--------------- |:--------------- |:-------|
| GEX_TEC_TCF7KO_S2_R1_001	| Mus Musculus C57BL/6 J TEC Tcf7KO forward reads (mouse age: 6 weeks) | Tcf7KO
| GEX_TEC_TCF7KO_S2_R1_001	| Mus Musculus C57BL/6 J TEC Tcf7KO reverse reads (mouse age: 6 weeks) | Tcf7KO
| GEX_TEC_TCF7WT_S1_R1_001	| Mus Musculus C57BL/6 J TEC Control forward reads (mouse age: 6 weeks) | WT
| GEX_TEC_TCF7WT_S1_R2_001	| Mus Musculus C57BL/6 J TEC Control reverse reads (mouse age: 6 weeks) | WT

---

## Description of the main analysis

The computational workflow is organized into two successive stages.

### First step : Individual dataset analysis

Each dataset is first processed independently to assess sequencing quality and characterize cellular heterogeneity prior to integration.

Scripts and corresponding outputs for this stage are stored within the folder associated with each dataset.

### Second step : Merge all datasets

After quality assessment, all datasets are combined into a single integrated analysis to enable comparisons between experimental conditions.

The scripts and outputs corresponding to this integrated analysis are available in the Integrated directory.

---

## Structure of the data and code

### Folders of the datasets

The repository is structured around individual datasets. Each dataset has its own directory containing the analysis resources. After downloading both the repository and associated data, the project hierarchy should resemble the following:

```
.
└── Tcf7
    ├── Tcf7WT_sc
    ├── Tcf7KO_sc
    └── Integrated
``` 

### Folders inside the datasets

Each dataset directory contains two complementary groups of files: one dedicated to the analysis code and another containing the generated outputs.

 * The GitHub repository provides the source code, including the scripts (03_Scripts) and Docker definition files (02_Container).
```
.
└── Tcf7
    ├── Tcf7WT_sc
    │   ├── 02_Container
    │   ├── 03_Scripts
```

 * The Zenodo archive contains the rawdata ,pre-built container images, processed data and analysis outputs.
 
```
.
└── Tcf7
    ├── Tcf7WT_sc
    │   ├── 00_RawData
    │   ├── 02_Container
    │   ├── 05_Output

```

---
---

## Prepare the environments

Before running the analyses, a few setup steps are required:

* clone the GitHub repository and define the WORKING_DIR environment variable;
* download the datasets;
* install Docker to execute the analyses within the provided containerized environment.

Detailed instructions are provided below.

---

#### Clone the GitHub repository

Clone the repository into the directory of your choice using your preferred Git client. This will create a local **Tcf7** directory containing all analysis scripts.

#### Set the Working Dir variable

Create an environment variable named **WORKING_DIR** pointing to the location of the cloned repository.

For example, if the repository was cloned into **/home/malki/workspace**, the variable should be defined as:

**On linux:**

```
    export WORKING_DIR=/home/malki/workspace/Tcf7
```

#### Add your working dir in the code

Several parameter files contain project-specific settings. In particular, each dataset includes a **projectParams.R** file located in **03_Scripts**, where the **PATH_PROJECT** variable specifies the project location.

Locate this file for each dataset and update **PATH_PROJECT** so that it matches your local **WORKING_DIR**.

For instance:

```
    Tcf7
    │
    ├── Tcf7WT_sc
    │   │
    │   └── 03_Script/projectParams.R

```

Edit those files and in each of them locate the line defining the **PATH_PROJECT** variable and change its value to the same value as the **WORKING_DIR** variable you defined before. Then save the files.

```
for example :

PATH_PROJECT = "/home/malki/workspace/Tcf7"
```

---

### Download the data

Raw FASTQ sequencing files are publicly available from GEO, whereas processed datasets and analysis outputs can be obtained from Zenodo.

- Tcf7_WT_sc (lien zenodo) : contains the rawdata , the result of Cell Ranger count analysis and the processed object for the WT sample
- Tcf7_KO_sc (lien zenodo) : contains the rawdata , the result of Cell Ranger count analysis and the processed object for the KO sample
- Tcf7_Integrated [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21395640.svg)](https://doi.org/10.5281/zenodo.21395640) : outputs and processed object of the final analysis after integration

To preserve the expected directory structure, extract the downloaded files directly into **WORKING_DIR**.

To download and uncompress the data, use the following code:

**On linux:**

```
    cd $WORKING_DIR
    wget https://zenodo.org/record/21217512/files/Tcf7_WT_sc.tar.gz -O Tcf7_WT_sc.tar.gz
    tar zxvf Tcf7_WT_sc.tar.gz
    
    wget https://zenodo.org/record/21395547/files/Tcf7_KO_sc.tar.gz -O Tcf7_KO_sc.tar.gz
    tar zxvf Tcf7_KO_sc.tar.gz

    wget https://zenodo.org/record/21395640/files/Tcf7_Integrated.tar.gz -O Tcf7_Integrated.tar.gz
    tar zxvf Tcf7_Integrated.tar.gz
```
 
Once done, you may obtain the following subfolder structure, each of them containing several files.

```
    Tcf7
    ├── Tcf7WT_sc
    │   ├── 00_RawData
    │   ├── 02_Container
    │   └── 05_Output
    ├── Tcf7KO_sc
    │   ├── 00_RawData
    │   ├── 02_Container
    │   └── 05_Output
    └── Tcf7_Integrated
        ├── 02_Container
        └── 05_Output

```

--- 

#### Download the container images

Docker archives (.tar.gz) are available in the **02_Container** directory of each dataset.

Docker archives must first be imported into your local Docker installation.

---

### Install the Docker environment to run the analysis interactively

#### Install Docker

To execute the analyses interactively through RStudio, install Docker by following the official installation guide:

https://docs.docker.com/get-docker/


#### Load the images

Once done, load the downloaded image using:

```
docker load -i <image_name>.tar.gz
```

#### Run the analysis individually using Docker

If you have loaded the docker images (see above), you can use Rstudio in Docker to run the analysis individually.

Launch the container with:

```
docker run -d -p 8787:8787 -v /$WORKING_DIR:/$WORKING_DIR -e PASSWORD=<PASSWORD> -e USER=$(whoami) -e USERID=$(id -u) -e GROUPID=$(id -g)  <IMAGE_NAME>
```

where:

* <PASSWORD> is a simple string you will use as password to login into Rstudio
* <IMAGE_NAME> is the Docker image name to run

Once the container is running, open a web browser and connect to:

https://127.0.0.1:8787

Authenticate using your Linux username together with the password specified above.

The RStudio session will have direct access to the mounted **WORKING_DIR** , allowing you to browse the project files and execute the analyses.

The main entry point of each workflow is the **launch_report.R** script.

