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

There are several steps to run ANNOVAR. Firstly, you need to download the ANNOVAR from `https://doc-openbio.readthedocs.io/projects/annovar/en/latest/user-guide/download/`. You need the registration and then you will receive any email to download it. If users use `Annoconda Powershell prompt`, you can dirctly using `tar -xvf ANNOVAR.tar.gz` to untar the downladed file, and then go next section to run ANNOVAR; if users use `Annoconda prompt`, please go to next step. Secondly, you need to install 7-zip so that you can untar the ANNOVAR.tar.gz. Thirdly, to run ANNOVAR directly, we need to associate `.pl` file with `perl`. Right click `Annoconda prompt` and then run it as administrator. In the command, run the following two commands
```
assoc .pl=PerlScript
ftype PerlScript=C:\Users\%USERNAME%\Anaconda3\pkgs\perl-5.26.2.1-h0c8e037_0\Library\bin\perl.exe "%1" %*
```
If your installation folder of perl is different from the perl path above, please change the path corresponding.



### 2. Run ANNOVAR

We need to download some DB for ANNOVAR. Users can find more db [here](https://doc-openbio.readthedocs.io/projects/annovar/en/latest/user-guide/download/#-for-filter-based-annotation)
```
annotate_variation.pl -buildver hg19 -downdb -webfrom annovar gnomad211_genome  humandb/ 
annotate_variation.pl -buildver hg19 -downdb -webfrom annovar 1000g2015aug   humandb/ 
```

```
table_annovar.pl example/ex2.vcf humandb/ -buildver hg19 -out myanno -remove -protocol refGene,gnomad211_genome,1000g2015aug -operation g,f,f -nastring . -vcfinput -polish
```
After that, you will find the result files whose filenames starts with `myanno`

## Install Phen2Gene

One need to install Phen2Gene using the command below. Please deactivate other conda environments if you are not in conda base.
```
git clone https://github.com/WGLab/Phen2Gene.git
cd Phen2Gene
conda env create -f environment.yml #(I remove readline, ncurses)
conda activate phen2gene
```

After that, download the database from https://github.com/WGLab/Phen2Gene/releases/download/1.1.0/H2GKBs.zip and unzip it. You need to copy unzip folder to `lib/h2gpath.config` under Phen2Gen folder.

### Run Phen2Gene (from Phen2Gene github)

1. Input HPO IDs via input file (typical use case)
```
python phen2gene.py -f example/HPO_sample.txt -out out/prioritizedgenelist
```
2. Input HPO IDs via input file, and candidate gene list file (another common use case)
```
python phen2gene.py -f example/HPO_sample.txt -out out/prioritizedgenelist -d example/1000genetest.txt
```
3. Use Skewness and Information Content

  * `-w sk` uses a skewness-based weighting of genes for each HPO term (default, and recommended)
  * `-w w` and `-w ic` do not use skew, but utilize information content in the tree structure (slightly worse performance)
  * `-w u` is unweighted

```
python phen2gene.py -f example/HPO_sample.txt -w sk -out out/prioritizedgenelist
```
4. Run Phen2Gene with verbose messages
```
python phen2gene.py -f example/HPO_sample.txt -v -out out/prioritizedgenelist
```
5. Input HPO IDs manually, if desired
```
python phen2gene.py -m HP:0000021 HP:0000027 HP:0030905 HP:0010628 -out out/prioritizedgenelist
```





