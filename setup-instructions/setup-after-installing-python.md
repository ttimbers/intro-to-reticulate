## Using Python in RStudio

### Mac & Linux users

You can now use RStudio as an effective Python IDE. To do so, follow these steps after installing miniconda:

1. Install the {reticulate} package: `install.packages("reticulate")`

2. Install the {png} package (a dependency of reticulate that is not well managed yet): `install.packages("png")`

3. Find your path to miniconda by typing `which python` in a terminal (Git Bash on Windows) outside of RStudio

4. Specify that {reticulate} should use the miniconda version of Python in your `.Rprofile` file:

  - type `usethis::edit_r_profile` into the R console inside RStudio, and an `.Rprofile` file from your HOME directory should open in RStudio
  - add this to your `.Rprofile` file: `Sys.setenv(RETICULATE_PYTHON = "path_to_miniconda's_python")` replacing `"path_to_miniconda's_python"` with the path to your miniconda Python
  
5. In terminal type `code ~/.bash_profile` and add the line `export PATH="/opt/miniconda3/bin:$PATH"`, replacing `/opt/miniconda3/bin` with the path to the folder containing your miniconda Python (be careful not to include `python` at the end of this path). 
  
6. **Restart R!**

7. Start using Python in RStudio by typing `repl_python()` in the R console, or running a line of Python code from a Python script from the RStudio editor by Cntrl + enter. Or by running scripts from the terminal inside RStudio.

### Windows users

1. Install the {reticulate} package: `install.packages("reticulate")`

2. Install the {png} package (a dependency of reticulate that is not well managed yet): `install.packages("png")`

3. Find your path to miniconda by typing `which python` in a terminal (Git Bash on Windows) outside of RStudio

4. Specify that {reticulate} should use the miniconda version of Python in your `.Rprofile` file:

  - type `usethis::edit_r_profile` into the R console inside RStudio, and an `.Rprofile` file from your HOME directory should open in RStudio
  - add this to your `.Rprofile` file: `Sys.setenv(RETICULATE_PYTHON = "path_to_miniconda's_python")` replacing `"path_to_miniconda's_python"` with the path to your miniconda Python. In Windows, you need `\\` instead of a `\` to separate the directories, for example my path here would be: `C:\\Users\\tiffany.timbers\\miniconda3\\python.exe`.
  
5. Open Global Options in RStudio and in the Terminal sub-menu, select "Custom" as the "New terminals to open with" option, and add the path to GitBash (should be something like `C:/Program Files/Git/bin/bash.exe`) as the "Custom shell binary" option. Finally set `-l` (lower case L) as the option for "Custom shell command-line options".

<img src="../imgs/custom-terminal.png" width=500>

6. **Restart R!** Open R and close the terminal tab. Open a new terminal.

<img src="../imgs/new-terminal.png" width=y00>

7. Start using Python in RStudio by typing `repl_python()` in the R console, or running a line of Python code from a Python script from the RStudio editor by Cntrl + enter. Or by running scripts from the terminal inside RStudio.