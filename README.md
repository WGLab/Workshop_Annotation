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







