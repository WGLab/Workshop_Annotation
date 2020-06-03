# Introduction
This repository contains the course materials for hands-on exercise session of the "Variants Annotate and Phenotype Analysis" workshop. 

# Preparation of computing environment
Both the lectures and hands-on exercises will be taught via video conference online. To ensure the cross-platform compatibility, we will only use tools that are developed in Perl and Python. As most users are using either Windows or MacOS in your personal computers, below we describe the preferred means to prepare computing environment using Conda. 

## Windows
The suggested way to perform the hands-on exercises is to install [Anaconda](https://www.anaconda.com/products/individual), which is an open source, flexible solution that provides the utilities to build, distribute, install, update, and manage software in a cross-platform manner. Note that the Windows versions of several widely graphical user interface (GUI) packages, including Jupyter Notebook and Spyder, are already included within Anaconda by default; additionally, Rstudio can be also installed by one-click installation within Anaconda Navigator.

Once you go to the website, click "Download" button (see image below), and then install in your Windows computer by accpeting all default options.

![Anaconda Installation](img/anaconda.png)


Once installation is successful, you can launch the Anaconda Navigator, and see the interface below.

![Anaconda Navigator](img/navigator.png)

Of course, for some users, Conda is not strictly required if you are already familiar with running command-line driven software tools in Windows via WSL or PowerShell and has Perl/Python pre-installed in your Windows computer. So if you are among this group of users, you can skip this step and go directly to the exercises itself.



## MacOS
Since MacOS has built-in terminal and Linux-like enrivonment for executing command-line software tools, in general you do not need any specific set up. However, you may want to install [Miniconda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html).


# Installation of software tools and data sets

## Install Perl

Click "CMD.ext prompt" or "Powershell prompt", and you will see a terminal that has "(base) C:\Users\Kai Wang>" as the prompt.

By default, we will start in a `base` environment. For this course, we will create an environment called "annotation" to use for the variants annotation and phenotype analysis. 

```
(base) C:\Users\Kai Wang>conda create --name annotation
```

Next, we will enter the new environment that was just created to perform the exercise:

```
(base) C:\Users\Kai Wang>conda activate annotation

(annotation) C:\Users\Kai Wang>
```

You can see that the `(base)` in command prompt is changed to `(annotation)` indicating that we are now in a different environment.

For running ANNOVAR, we need to have Perl installed in the computer. You can do `conda install perl`, and press "y" when prompted. See image below.

![conda perl](img/conda_perl.png)

## Install ANNOVAR

### 1. Install ANNOVAR dependent packages

There are several steps to run ANNOVAR. Firstly, you need to download the ANNOVAR from `https://github.com/WGLab/Workshop_Annotation/releases/edit/v1.0.0`. Within Anaconda Powershell prompt, you can dirctly using `tar -xvf annovar.latest.tar.gz` to untar the downladed file, and then go next section to run ANNOVAR.

### 2. Run ANNOVAR

We need to download some annotation databases for ANNOVAR. Type `cd annovar` to enter the `annovar` directory. (Note that users can find more databases [here](https://doc-openbio.readthedocs.io/projects/annovar/en/latest/user-guide/download/#-for-filter-based-annotation).
```
perl annotate_variation.pl -buildver hg19 -downdb -webfrom annovar gnomad211_exome  humandb/ 
perl annotate_variation.pl -buildver hg19 -downdb -webfrom annovar dbnsfp35a   humandb/ 
```

```
table_annovar.pl example/ex2.vcf humandb/ -buildver hg19 -out myanno -remove -protocol refGene,gnomad211_exome,dbnsfp35a -operation g,f,f -nastring . -vcfinput -polish
```
After that, you will find the result files whose filenames starts with `myanno`

## Install Phen2Gene

One need to install Phen2Gene using the command below. Please deactivate other conda environments if you are not in conda base.

To make the tutorial easy, the users can just download the source code for Phen2Gene from the release:

```
wget https://github.com/WGLab/Phen2Gene/archive/1.2.1.zip -O Phen2Gene.zip
```

Then extract either with 7zip, WinRAR or

```
unzip Phen2Gene.zip -d Phen2Gene
```

If you are more experienced, and you want to download Phen2Gene from github, users can install git using the command below and git clone.
```
conda install git
git clone https://github.com/WGLab/Phen2Gene.git
cd Phen2Gene
```

### Running environment for Phen2Gene

To create your environment (necessary for *ALL* operating systems):

```
conda env create -f environment.yml
conda activate phen2gene
```

If on `MacOS` or `Linux` run:

```
bash setup.sh
```
And the installation will be extremely easy for you.  The database and all will be downloaded and you can install P2G in your path.

If on `Windows`:

```
wget https://github.com/WGLab/Phen2Gene/releases/download/1.1.0/H2GKBs.zip -O H2GKB.zip
```

Then extract either with 7zip, WinRAR or

```
unzip H2GKB.zip -d H2GKB
```

*We recommend extracting the file into lib for ease of use for this tutorial, but you can put the file wherever you want.*

### Run Phen2Gene

If on Windows, and you do not have the space to download and extract the `H2GKB.zip` in the `lib` folder (recommended default) you will have to use `-d full_path_to_H2GKB.zip_extraction_folder`.  This means wherever you decided to download and unzip `H2GKB.zip`, you have to add that path to each use of `phen2gene.py` as below:

1. Input HPO IDs via input file (typical use case)

Default command:
```
python phen2gene.py -f example/HPO_sample.txt -out out/prioritizedgenelist
```
Alternate folder for H2GKB, add `-d`:
```
python phen2gene.py -f example/HPO_sample.txt -out out/prioritizedgenelist -d full_path_to_H2GKB.zip_folder
```
2. Input HPO IDs manually, if desired
```
python phen2gene.py -m HP:0000021 HP:0000027 HP:0030905 HP:0010628 -out out/prioritizedgenelist
```

### A real world use case of Phen2Gene using ANNOVAR

We're going to get actual variants from a proband with developmental disease from a CSH Molecular Case Studies paper.

So first we download it.

In the `ANNOVAR` folder:

```
wget http://molecularcasestudies.cshlp.org/content/suppl/2016/10/11/mcs.a001131.DC1/Supp_File_2_KBG_family_Utah_VCF_files.zip -O Supp2.zip
perl annotate_variation.pl -buildver hg19 -downdb -webfrom annovar refGene humandb
```

UNIX (`Windows` users, just unzip here, and *rename folder to `VCF_files`*):

```
unzip Supp_File_2_KBG_family_Utah_VCF_files.zip -d VCF_files
rm -rf __MACOSX; rm Supp_File_2_KBG_family_Utah_VCF_files.zip
```

Run ANNOVAR on the VCF file:
```
perl table_annovar.pl VCF_files/proband.vcf -buildver hg19 humandb -out proband.annovar -remove -protocol refGene,gnomad211_exome -operation g,f -nastring . -vcfinput
```

#### *Now move `proband.annovar.hg19_multianno.txt` to the `Phen2Gene` folder!*

We already have the HPO IDs for this patient in the `example` folder of `Phen2Gene` so just run:

```
python phen2gene.py -f example/ANKRD11_id.txt -w sk -out ankrd11
```

Now, let's use `awk`, one of Jim's favorite tools, to do some fancy filtering on gnomAD allele frequency (column 11, across 125,748 exomes).  We want rare variants (<1% freq.).

```
conda install gawk
awk '$11 <= 0.01 || $11 == "."' FS="\t" proband.annovar.hg19_multianno.txt > filtered.proband.annovar.hg19_multianno.txt
```

Now using a `python` script that we pre-wrote in the `example` folder, we can create a newly sorted list of genes from `Phen2Gene` based on the genes with rare variants present in the `ANNOVAR` output:

```
python example/filterbyannovar.py -pre ankrd11/output_file.associated_gene_list -post ankrd11filter -anno filtered.proband.annovar.hg19_multianno.txt
```

Then view the newly created file `ankrd11filter` and note the top 10 genes, and our causal gene ANKRD11 at number 1.  It was previously number 2 if you check `ankrd11/output_file.associated_gene_list`.
