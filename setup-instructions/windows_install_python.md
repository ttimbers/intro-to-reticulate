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
- [Git and Bash](#git-and-bash)
- [Python and Conda](#python-and-conda)
- [R, IRkernel, Rtools, and RStudio](#r-irkernel-rtools-and-rstudio)

## Git and Bash

Although Git and Bash are two separate programs,
we are including them in the same section here 
since they are packaged together in the same installer on Windows.
Briefly, we will be using the Bash shell to interact with our computers via a command line interface,
and Git to keep a version history of our files and upload to/download from to GitHub.
We will be using the command line version of Git as well as Git through RStudio and JupyterLab. Some of the Git commands we will use are only available since Git 2.23, so if you're Git is older than this version, we ask you to update it.

Go to <https://git-scm.com/download/win> and download the windows version of git. After the download has finished, run the installer and accept the default configuration for all pages except for the following:

- *Optional* On the **Select Components** page, check "On the Desktop" under "Additional icons".
- On the **Choosing the default editor used by Git** page, select "Use Visual Studio Code as Git's default editor" from the drop-down menu'

![](imgs/vscode-as-git-editor.png)

> Note if you wish to pin Git Bash to the taskbar, you need to search for the program in the start menu, right click the entry and select "Pin to taskbar". If you instead first launch the program and pin it by right clicking on the taskbar icon, Git Bash will open with the wrong home directory (`/` instead of `/c/users/$USERNAME`.

After installation, test if you were successful by opening the Git Bash program. Below is a picture of the Git Bash icon on the Desktop and an opened instance of the Git Bash terminal (we will often refer to this as just "the terminal"):

![](imgs/gitbash.png)

In the terminal, type the following to check which version of Bash you just installed:

```
bash --version
```

The output should look similar to this:

```
GNU bash, version 4.4.23(1)-release (x86_64-pc-sys)
Copyright (C) 2019 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>

This is free software; you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
```

> If you tried to paste the above into the Git Bash terminal, you will have noticed that `Ctrl+V` does not work in Git Bash. Instead you need to right click and select "Paste" or use the `Shift+Insert` shortcut. To copy from the Git Bash terminal you simply select the text you want and it is copied automatically.

> Via right click you can also reach the settings menu where you can configure Git Bash to your preferences, a couple of tips would be to check "Mouse -> Clicks place command line cursor" and change the font to something more legible, e.g. Consolas ("Text -> Select").

## Python and Conda

We will be using Python for this demo, and `conda` as our Python package manager. To install Python and the `conda` package manager, we will use the [Miniconda platform (read more here)](https://docs.conda.io/en/latest/miniconda.html), for which the [Python 3.8 64-bit version can be downloaded here](https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe). After the download has finished, run the installer and accept the default configuration for all pages.

> Do *not* add miniconda to PATH. We will set this up later.

After installation, open the Start Menu and search for the program called "Anaconda Prompt (miniconda3)". When this opens you will see a prompt similar to `(base) C:\Users\your_name`. Type the following to check that your Python installation is working:

```
python --version
```

which should return something like this:

```
Python 3.8.3
```

> If instead you see `Python 2.7.X` you installed the wrong version. Follow [these instructions](https://docs.anaconda.com/anaconda/install/uninstall) to delete this installation and try the installation again, selecting **Python 3.8**.

### Integrating Python with the Git Bash terminal

To avoid having to open the separate Anaconda Prompt every time we want to use Python, we can make it available from the (Git Bash) terminal, which is what we will be using most of the time. To set this up, open the "Anaconda Prompt (miniconda3)" again and type:

```
conda init bash
```

You will see that this modified a few configuration files, which makes `conda` visible to the terminal. Close all open terminal windows and launch a new one, you should now see that the prompt string has changed to include the word `(base)` as in the screenshot below:

![](imgs/add-conda-env-to-ps1.png)

If you type

```
python --version
```

you should now see the same output as above:

```
Python 3.8.3
```

> Note that if you want to run Python interactively from the Git Bash terminal, you need to prepend the `winpty` command, so the full command would be `winpty python` (if you run this, note that you can exit the Python prompt by typing `exit()`). Running just `python` works on other setups, but will freeze the Git Bash terminal.

Let's also check the version of the `conda` package manager. If you type

```
conda --version
```

you should see something like this

```
conda 4.8.3
```

### Essential Python packages

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

To install packages individually, we can now use the following command: `conda install <package-name>`. Let's install the key packages needed for the start of the MDS program:

```
conda install \
 numpy=1.* \
 pandas=1.* 
```

`conda` will show you the packages that will be downloaded,
and you can press enter to proceed with the installation.
If you want to answer `yes` by default and skip this confirmation step,
you can replace `conda install` with `conda install -y`.

## R, Rtools, and RStudio

R and RStudio will also be used in this demo. 

### R

Go to <https://cran.r-project.org/bin/windows/base/> and download the latest version of R for Windows (4.0.2 at the time of writing). Open the file and follow the installer instructions accepting the default configuration.

After the installation is complete, we will add the R executables to the PATH variable in terminal so that you can use it without typing the full path to R each time. Open a terminal and type:

```
code ~/.bash_profile
```

Append the following line to the file

```
# Add R and Rscript to PATH
export PATH="/c/Program Files/R/R-4.0.2/bin/x64":$PATH
```

Then save the file and exit VS Code.
Now you can open terminal and type

```
R --version
```

which should return something like:

```
R version 4.0.2 (2020-06-22) -- "Taking Off Again"
Copyright (C) 2020 The R Foundation for Statistical Computing
Platform: x86_64-w64-mingw32/x64 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under the terms of the
GNU General Public License versions 2 or 3.
For more information about these matters see
https://www.gnu.org/licenses/.
```

> Note: Although it is possible to install R through Anaconda, we highly recommend not doing so. In case you have already installed R using Anaconda you can remove it by executing `conda uninstall r-base`.

### RStudio

Download the Windows version of RStudio from <https://www.rstudio.com/products/rstudio/download/preview>. Open the file and follow the installer instructions.

To see if you were successful, try opening RStudio by clicking on its icon. It should open and looks something like this picture below:

![](imgs/RStudio.png)

Next, we will make sure that Rstudio uses the same directories as R from terminal for its configuration. To do this, we will need to set an environmental variable in Windows. First, open the start menu, type "env" and select the match that reads "Edit the system environment variables". Click the button at the bottom that reads "Environmental Variables...":

![](imgs/sys-props-env-vars.png)

Under "User variable" click the "New..." button:

![](imgs/env-vars-new-user-var.png)

And type in `R_USER` as the "Variable name" and `C:\Users\username` as the "Variable value", replacing `username` with your actual user name (if you don't know your user name, look at the top of the screenshot above where it says "User variables for your_username"):

![](imgs/new-user-var-values.png)

Click "OK" on all of the three windows we opened above and you're done! If you open RStudio and R from terminal and type the following in both:

```
.libPaths()
```

both applications should return the same values, and the first one should be a path inside your user directory e.g.

```
"C:/Users/joelo/R/win-library/4.0"   "C:/Program Files/R/R-4.0.2/library"
```

If they don't return the same paths, please try to setting up your environmental variable again
and making sure that it is pointing to the correct folder.

**Do not continue unless both R from terminal and R from RStudio return the same paths here or later parts of the installation will fail.**

### Rtools

Windows users will also need to install Rtools, which will allow you to use external libraries. Go to <http://cran.r-project.org/bin/windows/Rtools/> and download the latest version (e.g., Rtools40.exe). After the download has finished, run the installer with the default configuration. Do *not* follow the Rtools' website instructions for "Putting Rtools on the PATH". RStudio will put Rtools on the PATH automatically when it is needed.

To test if you're installation was successful, open RStudio and type the following into the Console:

```
install.packages("jsonlite", type = "source")
```

If the `jsonlite` package installs without errors, Rtools is setup correctly.

### {tidyverse} R package

Next, install the key R packages needed for the start of MDS program,
by opening up RStudio and
typing the following into the R console inside RStudio:

```
install.packages('tidyverse')
```

If you get a prompt asking if you want to install packages that need compilation from sources, click "Yes".

> Note: we will install reticulate together during the demo.
