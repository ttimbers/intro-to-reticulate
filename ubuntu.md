These instructions were created using computers that satisfied these requirements (i.e., no promises they will work on other systems):

 - runs one of the following operating systems: macOS 10.15.X (Catalina), Ubuntu 20.04, Windows 10 Professional, Enterprise or Education; version 2004.
    - **Windows 10 Home is not sufficient** as not all the software required for the program can be installed on that OS. [Click here to download Windows 10 Education for free from UBC.](https://it.ubc.ca/software-downloads)
    - When installing Ubuntu, checking the box "Install third party..." will (among other things) install proprietary drivers, which can be helpful for wifi and graphics cards.
- can connect to networks via a wireless connection for on campus work
- has access to an internet connection that is fast and stable enough for video calling and conducting online quizzes
- has at least 50 GB disk space available
- has at least 8 GB of RAM
- uses a 64-bit CPU
- is at most 6 years old
- uses English as the default language

Table of Contents:
- [Python and Conda](#python-and-conda)
- [R and RStudio](#r-and-rstudio)

## Python and Conda

We will be using Python for this demo, and `conda` as our Python package manager. To install Python and the `conda` package manager, we will use the [Miniconda platform (read more here)](https://docs.conda.io/en/latest/miniconda.html), for which the [Python 3.8 64-bit version can be downloaded here](https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh).

Once the download is finished, open Terminal and execute the following commands:
```
bash path/to/file
```

> Note: most often this file is downloaded to the `Downloads` directory, and thus the command will look like this:
>
>```
>bash Downloads/Miniconda3-latest-Linux-x86_64.sh
>```

The instructions for the installation will then appear:

(1) Press Enter.
(2) Once the licence agreement shows, you can press space scroll down, or press `q` to skip reading it.
(3) Type `yes` and press enter to accept the licence agreement.
(4) Press enter to accept the default installation location.
(5) Type `yes` and press enter to instruct the installer to run `conda init`, which makes `conda` available from the terminal/shell.

After installation, restart the terminal. If the installation was successful, you will see `(base)` prepending to your prompt string. To confirm that `conda` is working, you can ask it which version was installed:
```
conda --version
```
which should return something like this:

```
conda 4.8.3
```

Next, type the following to ask for the version of Python:
```
python --version
```
which should return something like this:

```
Python 3.8.3
```

> Note: If instead you see `Python 2.7.X` you installed the wrong version. Uninstall the Miniconda you just installed (which usually lives in the `/home/<USER>` directory), and try the installation again, selecting **Python 3.8**.

## Essential Python packages

`conda` installs Python packages from different online repositories which are called "channels".
A package needs to go through thorough testing before it is included in the default channel,
which is good for stability,
but also means that new versions will be delayed and fewer packages are available overall.
There is a community-driven effort called the [conda-forge (read more here)](https://conda-forge.org/),
which provides more up to date packages
To enable us to access the most up to date version of the Python packages we are going to use,
we will add the more up to date  channel,
To add the conda-forge channel by typing the following in the terminal:

```
conda config --add channels conda-forge
```

To install packages individually, we can now use the following command: `conda install <package-name>`. Let's install the key packages needed for the start of our program:

```
conda install \
 numpy=1.* \
 pandas=1.* 
```

`conda` will show you the packages that will be downloaded,
and you can press enter to proceed with the installation.
If you want to answer `yes` by default and skip this confirmation step,
you can replace `conda install` with `conda install -y`.

## R, IRkernel, and RStudio

R is another programming language that we will be using a lot in the MDS program. We will use R both in Jupyter notebooks and in RStudio.

#### R

The version of R available in the default Ubuntu repositories (`3.6.*`) is older than the one we use in MDS (`4.*`). To obtain the latest R `4.*` packages, we need to add a new repository which is maintained directly by the r-project. To do this, first add the key for this repository by typing the following:

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
```

Then add the URL to the repository:

```
sudo apt-add-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
```

Next, install `r-base` and `r-base-dev` (useful for compiling R packages from source):

```
sudo apt install r-base r-base-dev
```

After installation, type the following in a terminal to ask for the version:
```
R --version
```

You should see something like this if you were successful:

```
R version 4.0.2 (2020-06-22) -- "Taking Off Again"
Copyright (C) 2020 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```

> Note: Although it is possible to install R through conda, we highly recommend not doing so. In case you have already installed R using conda you can remove it by executing `conda uninstall r-base`.

### RStudio

Download the Ubuntu 18/Debian 10 Desktop version of RStudio Preview from [https://rstudio.com/products/rstudio/download/preview/](https://rstudio.com/products/rstudio/download/preview/). Open the file and follow the installer instructions.

> Note that there is not yet an official RStudio version for Ubuntu 20.04, so it is recommended to use the Ubuntu 18 version. Also note that if you select "open with" and try to open the file directly with the Ubuntu Software app instead of downloading it first, the software app might complain that the file is not supported.

To see if you were successful, try opening RStudio by clicking on its icon or typing `rstudio` in a terminal. It should open and look something like this picture below:

![](imgs/RStudio-ubuntu.png)

> Note that since we installed RStudio directly from a deb file rather than from a repository or a snap package, it will not be updated when we run `sudo apt upgrade` and not automatically as for snap packages. Instead, RStudio will notify you of any available updates when the program is launched.

### Essential R packages

The `tidyverse` R package (and some others) have external dependencies on Ubuntu outside of R. We need to install these first before we install such R packages:

```
sudo apt install libcurl4-openssl-dev libssl-dev libxml2-dev
```

Next, install the key R packages needed for the start of MDS program,
by opening up RStudio and
typing the following into the R console inside RStudio:

```
install.packages('tidyverse')
```

> Note: we will install reticulate together during the demo.
