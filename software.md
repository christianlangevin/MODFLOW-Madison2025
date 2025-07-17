# Software Installation
To get the most out of this workshop, you will need to come prepared with a laptop computer that has Python installed.  **If you are familiar with conda environments and know how to create a new conda environment using an environment.yml file, then skip ahead to Part 2**.  For all others, we recommend using the Miniforge software to download and install Python and required dependencies needed for the workshop.  

The following instructions will guide you through the installation process and setup of a `madison25flopy` environment.

## Part 1 -- Install Miniforge
1. Download and run the Miniforge installer (https://github.com/conda-forge/miniforge) for your platform.

2. Click through the installer options, and select "Just Me (recommended)" if asked.  Default installation options should be fine, with the exception that you should select an installation location that does not have any special characters or spaces in it.

3. After installation, you should see "Miniforge Prompt" as a program under the Windows Start menu.

## Part 2 -- Create an Environment File
We will use an environment file to create a containerized version of Python and the Python packages needed for the class.  An environment file is simply a list of packages that we want to install in our environment.

1. Using a text editor, such as Notepad or Notepad++, create a file called `environment.yml`.  It should contain the information in [this environment file](https://github.com/christianlangevin/MODFLOW-Madison2025/blob/main/environment.yml).  Save this file to your hard drive, preferably in your user home folder so that it can be easily accessed in the next step. (Caution!  Notepad will automatically append a .txt suffix to your file name; you don't want this to happen.)

<!-- 2. **For Mac and Linux users only!** You will need to add six additional dependencies to the `environment.yml` file from step 1.  The following dependencies are also required: 

```
  # parallel modflow build dependencies
  - pkg-config
  - meson
  - ninja
  - gfortran
  - openmpi
  - libnetcdf
  - netcdf-fortran
  - petsc=3.20.5
```   -->

## Part 3.  Create the `madison25flopy` Environment

1. Start the miniforge prompt from the Windows start menu (or equivalent on Mac or Linux) to bring up a terminal.

2. At the terminal prompt enter the following command, where `<path to file>` is the location of the `environment.yml` file that you created in Part 2.  You will need to be connected to the internet for this to work properly.  The installation process may take a couple of minutes.
```
mamba env create --file <path to file>/environment.yml
```

3.  After the environment has been installed, you may activate this new class environment with the following command
```
conda activate madison25flopy
```

4.  The windows terminal prompt should reflect the current environment:
```
(madison25flopy) C:\Users\JaneDoe>
```

5.  We will be using jupyter notebooks in the workshop.  To test if jupyter is installed and working properly use the following command.  After entering this command, the default web browswer should open to a Jupyter Lab page.
```
jupyter lab
```

For most users, the setup is complete at this point.  For those working on a Mac or Linux laptop, please proceed to Part 4.


## Part 4.  Obtaining MODFLOW 6

We will be using the extended version of MODFLOW 6 in this workshop.  

### Windows

If you are working on Windows, you can install the extended version of MODFLOW 6 by activating the workshop environment using:

```
conda activate madison25flopy
```

and then running:
```
get-modflow --repo modflow6 --ostag win64ext :python
```

and finally running:
```
get-modflow --subset gridgen,triangle :python
```

You can also download the extended version of MODFLOW 6 from [here](https://github.com/MODFLOW-ORG/modflow6/releases).  

Note that we will also walk through this step during the workshop.  The distribution file for windows that includes the parallel version is called `mf6.2.2_win64ext.zip`.

# Mac and Linux

If you are using a Mac or Linux laptop for the workshop, then you will need to build the parallel version of MODFLOW.  We have simplified the build process, which can be completed in just a few minutes. You will need to install git on your laptop if you don't already have it. 

1. Download the workshop GitHub repository using:
```
git clone https://github.com/christianlangevin/MODFLOW-Madison2025.git
```

2. Activate the madison25flopy environment
```
conda activate madison25flopy
```

3. Navigate to the root directory of the workshop GitHub repository and run the MODFLOW 6 build script using:
```
sh nix-build.sh  
```

4. If the build is successful you should see the following:
```
 Normal termination of simulation.
――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――
5/5 Parallel simulation test - 2 cores  OK              0.10s


Ok:                5   
Fail:              0   

Full log written to /path/to/the/class/github/repo/MODFLOW-Madison2025/modflow6/builddir/meson-logs/testlog.txt

Finished...


```
