# my-python-journey

Here are all the things nobody told me about Python, and that made me spend several hours on Google and Stackoverflow.

What I describe here is something I consider good practice, in a way that this allows you to track the dependencies for your projects, and then upload your code to GitHub or copy it on a USB stick, and it will work on other computer with already installed Python and Conda.

## Step 1: Install Conda

This simplifies Python version problems on posterior steps as it simplifies using a specific Python version.

For example, the numba library needs Python version 3.7.0 to 3.11.0 and I have version 3.11.2, therefore the installation fails with an error message telling me that my Python version is not compatible.

Go to https://docs.conda.io/en/latest/miniconda.html and download the latest version for your system.

I am using Ubuntu, and this is also tested with Red Hat, for both systems we can install without root privileges.

```bash
~ $ bash ~/Downloads/Miniconda3-latest-Linux-x86_64.sh
```

Install to the default folder, and when the installer asks you "Do you wish the installer to initialize Miniconda3 by running conda init?" select "yes".

Close the terminal, re-open it, and then paste this command:

```bash
~ $ conda config --set auto_activate_base false
```

The reason for the last command is to avoid that every time you open the terminal it activates an environment like this:

```bash
(base) ~ $
```

## Step 2: Create virtual environments

From the command line create a new folder and create an environment in the `venv` folder. Skip ignore the text before the `$`, that is the command line prompt which shows on which folder we are at the moment.

I created a virtual environment with Python 3.8.0 to solve that with

```bash
~ $ mkdir pol2578
~ $ cd pol2578
pol2578 $ conda create -n "venv" python=3.8.0 ipython
```

## Step 3: Activate the virtual environment

After closing and reopening the command line I activated the virtual environment with

```bash
pol2578 $ conda activate venv
```

Note that this changes the prompt to `(venv) pol2578 $`

## Step 4: Install pip inside the environment

In order to be able to install packages directly from Visual Studio Code (VSC), we need to install `pip, the Python package manager, inside the virtual environment, In this way, VSC will be able to install any missing packages when we get a Python notebook from a colleague.

```bash
(venv) pol2578 $ python -m ensurepip --upgrade
```

## Step 5: Start a Python notebook from VSC

Open VSC, go to `File -> Open Folder`, and open the `pol2578` folder just created. Then, at the top right corner, click the `environment` tab and select `Python Environments -> venv (Python 3.11.2) venv/bin/python Recommended`.

Now you are ready to edit any Python notebook shared with you or create your own with `.ipynb` extension by clicking `File -> New File -> `Jupyter Notebook .ipynb support`.

## Step 6: Install additional packages

Using and environment in the command line and in VSC are not the same.

If VSC needs an additional package such as `pandas`, you can install it from the command line.

```
(venv) pol2578 $ pip install pandas
```

When you are ready using the virtual environment, deactivate the environment in the command line. From VSC side, it is sufficient to close the window.

```bash
(venv) pol2578 $ conda deactivate
```

The prompt should read `pol2578 $` afterwards.

## Step 7: Special packages

`sklearn` must be installed with `pip install scikit-learn`, just `pip install sklearn` does not work.

`pandas` needs `pip install openpyxl` to export to Excel.

`keras` requires `pip install tensorflow`.
