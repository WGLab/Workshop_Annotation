# Introduction
In addition to Anaconda, we want to evaluate alternative ways to enable running of the ANNOVAR/Phen2Gene exercise in all types of computating envionment (Linux, Windows, MacOS), within reasonable amount of time and complexity (exercise session lasts 1 hour and 15 minutes). Some suggested Docker or Git Shell or WSL.

# Git for Windows
Download Git Windows version from https://gitforwindows.org/. Install by accepting all default options.

Start git shell, and `pwd` to find current working directory. You may want to `mkdir annotation_exercise2` and then `cd annotation_exercise2` to enter this directory for the exercises below.

One small issue is that `wget` is not available from Git Windows. You have to manually download it from https://eternallybored.org/misc/wget/1.19.2/wget64.exe, and then put it in the current directory.

Run `./wget64.exe https://github.com/WGLab/Workshop_Annotation/releases/download/v1.0.0/annovar.latest.tar.gz` to download ANNOVAR.

Run `$ tar -xvf annovar.latest.tar.gz` to unzip the file.

I found a few issues: (1) Perl is available but many standard packages (such as Pod::Usage) is not installed (2) Python is not available.
