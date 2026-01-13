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
   $ conda activate librosa-dev
   $ python -m pip install -e '.[tests]'

5. Create a branch to hold your changes, named this branch librosa-qi:

   $ git switch -c librosa-qi

and start making changes. Never work in the main branch!

Work on this copy on your computer using Git to do the version control. You can check your modified files using:

   $ git status 

7. Use VSCode Git interface to opdate

8. The first time around, using the Python terminal, to record your branch changes in Git, push them to GitHub with:

   (librosa-dev)% git push --set-upstream origin librosa-qi

Verify on GitHub

NOTES: 
Tried running: tests/make_mel_norm_test_data Jupyter
ipykernel was missing. Can't run Jupyter without it
'data/feature-melfb-001.mat' is empty, requires Matlab to run

docs/examples
mir_eval is missing