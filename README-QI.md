Prepared by M. Garces, UH ISLA/ARL
These notes are specific to implementing a fork and a branch via VSCode and a Conda environment.
It builds on the detailed instructions provided in:
https://github.com/librosa/librosa?tab=contributing-ov-file
with some modifications on the python version and pointing to the conda forge env in VSCode (VSC).

First, ensure GIT is installed and current.
For Mac, use Brew.

The first step for forking librosa is as in the URL above:
The preferred way to contribute to librosa is to fork the main repository on GitHub:

1. Fork the project repository: click on the 'Fork' button near the top of the page. This creates a copy of the code under your account on the GitHub server.

The next steps are specific to VSCode

2. Clone this copy to your local disk:
Point VSCode to your GitHub fork
Clone to a local directory
This automatically does:
   $ cd librosa 
   $ git pull --recurse-submodules
3. $ git remote add upstream git@github.com:librosa/librosa.git
So no need to do again, but if one does, nothing bad happens.

Next is as in URL, but recommend using latest stable supported version 3.12
4. Create a new conda environment in order to install dependencies:

   $ conda create -n librosa-dev python=3.12
   $ conda env update -n librosa-dev --file .github/environment-ci.yml

Note the preferred channel is conda-forge.

This command will state where that environment is saved, and it can be repurposed for other projects.

In the case of the Mac, it was saved at:
/usr/local/Caskroom/miniforge/base/envs/librosa-dev

From VSC View/Command Palette, choose Select Interpreter and direct to this path.
From VSC View/Command Palette, choose Python: Create Terminal
In Python Terminal, confirm prompt starts with (librosa-dev)
   conda activate librosa-dev
   python -m pip install -e '.[tests]' 

5. Create a branch to hold your changes, named this branch librosa-qi:

   $ git switch -c librosa-qi

and start making changes. Never work in the main branch!

Work on this copy on your computer using Git to do the version control. You can check your modified files using:

   $ git status 

7. Use VSCode Git interface to opdate

8. The first time around, using the Python terminal, to record your branch changes in Git, push them to GitHub with:

   (librosa-dev)% git push --set-upstream origin librosa-qi

Verify on GitHub

VSCode clone on PC with Anaconda:
There are USG licensing issues with Anaconda, but ISLA/ARL supports it and this section documentis it.
Used the Anaconda Prompt to accept the TOR's, without which things grind to a halt.
Since my code fork/branch already exists (created from Mac), I use the VSC to clone from my fork/branch from GitHub
I the Anaconda Navigator to create a new Python 3.12 Conda environment, and added the conda-forge channel.
The Conda enviroment was saved under:
C:\Users\Milton.Garces\.conda\envs\librosa-dev
View/Command Palette/ Python: Select Intepreter
Chose librosa-dev 3.12.12 conda
From VSC View/Command Palette, choose Python: Create Terminal
(librosa-dev) shows in the prompt
Ran:
conda env update -n librosa-dev --file .github/environment-ci.yml
conda activate librosa-dev
python -m pip install -e '.[tests]' - failed! Works on Mac, but [extras] falied on WinOS
   python -m pip install -e .  - worked, reads off pyproject.toml

From AI Overview:
   The difference between pip install -e . and pip install -e '.[tests]' is that the second command installs the package in editable mode along with the additional dependencies required for testing, as defined in your project's configuration file (e.g., pyproject.toml or setup.py). 
   [tests]: This is an "extra" or "optional dependency group". It tells pip to install the dependencies listed under the specifically named tests section in your pyproject.toml or setup.py file, in addition to the main dependencies.
   Noted the pyprojects.toml file does not have a tests section.

NOTES: 
Tried running: tests/make_mel_norm_test_data Jupyter
ipykernel was missing. Can't run Jupyter without it
'data/feature-melfb-001.mat' is empty, requires Matlab to run

docs/examples
mir_eval is missing