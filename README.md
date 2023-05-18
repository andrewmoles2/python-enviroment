# my-python-journey

Here are all the things nobody told me about Python, and that made me spend several hours on Google and Stackoverflow.

What I describe here is something I consider good practice, in a way that this allows you to track the dependencies for your projects, and then upload your code to GitHub or copy it on a USB stick, and it will work on other computer with already installed Python and Conda.

## Step 1: Install Miniconda

This simplifies Python version problems on posterior steps as it simplifies using a specific Python version. For example, transcription libraries such as `whisper` do not work with the most recent Python version, so creating an environment with Python 3.8.0 guarantees it will work. This happens because `whisper` depends on the `numba` library, which requires Python version 3.7.0 to 3.11.0 and I my Ubuntu version ships Python 3.11.2. Therefore, without creating an environment the installation fails with an error message telling me that my Python version is not compatible.

Go to https://docs.conda.io/en/latest/miniconda.html and download the latest version for your system. I prefer to install Miniconda because it is a lightweight version of Anaconda. The difference is that Miniconda uses around 200 MB on disk, and Anaconda around 3 GB. For most common tasks, you do not need the full Anaconda, and you can always install the parts that you need to run your project.

It is recommended to install Miniconda to the default folder.

### Windows

Stick to the default options in the graphical installer, but be sure to select "Add Miniconda 3 to my PATH"  after you select the destination folder. Then reboot your system.

### Linux / OS X

For both systems we can install Miniconda without root privileges. Open the terminal and run:

```bash
~ $ bash ~/Downloads/Miniconda3-latest-Linux-x86_64.sh
```

When the installer asks you "Do you wish the installer to initialize Miniconda3 by running conda init?" select "yes".

Close the terminal, re-open it, and then paste this command to avoid that every time you open the terminal it activates the base environment:

```bash
~ $ conda config --set auto_activate_base false
```

Close the terminal again, re-open it, and check that the prompt does *not* look like this:

```bash
(base) ~ $
```

## Step 2: Create virtual environments

On Windows, the terminal corresponds to the "Anaconda prompt (miniconda3)" application.

From the terminal, create a new folder and an environment. The environments will be stored in the `~/miniconda3/envs` directory. It is recommended that you create one environment per project, as these are independent from each other.

I created a virtual environment with Python 3.8.0 to solve the requirements problem previously described with:

```bash
~ $ mkdir pol2578
~ $ cd pol2578
pol2578 $ conda create -n "pol2578" python=3.8.0 ipython
```

## Step 3: Activate the virtual environment

After closing and reopening the command line I activate the virtual environment with

```bash
pol2578 $ conda activate pol2578
```

Note that this changes the prompt to `(pol2578) pol2578 $`.

## Step 4: Install pip and ipykernel inside the environment

In order to be able to install packages directly from Visual Studio Code (VSC), we need to install `pip`, the Python package manager, and `ipykernel`, an execution backend, inside the virtual environment. In this way, VSC will be able to install any missing packages when we get a Python notebook from a colleague.

```bash
(pol2578) pol2578 $ python -m ensurepip --upgrade
(pol2578) pol2578 $ pip install ipykernel
```

## Step 5: Start a Python notebook from VSC

Open VSC, go to `File -> Open Folder`, and open the `pol2578` folder just created. Then, at the top right corner, click the `environment` tab and select `Python Environments -> pol2578 (Python 3.8.0) ~/miniconda/envs/pol2578/bin/python`.

Now you are ready to edit any Python notebook shared with you or create your own with `.ipynb` extension by clicking `File -> New File -> `Jupyter Notebook .ipynb support`.

## Step 6: Install additional packages

Using and environment in the command line and in VSC are not the same.

If VSC needs an additional package such as `pandas`, you can install it from the command line.

```
(pol2578) pol2578 $ pip install pandas
```

When you you have finished using the virtual environment, deactivate the environment in the command line. From VSC side, it is sufficient to close the window.

```bash
(pol2578) pol2578 $ conda deactivate
```

The prompt should read `pol2578 $` afterwards.

## Step 7: Special packages

`sklearn` must be installed with `pip install scikit-learn`, just `pip install sklearn` does not work.

`pandas` needs `pip install openpyxl` to export to Excel.

`keras` requires `pip install tensorflow`.
