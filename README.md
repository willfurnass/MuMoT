# MuMoT
Multiscale Modelling Tool
---

## Introduction / overview

TODO

## Installation

TODO: intro

### Prerequisite: LaTeX

The visualisation of particular representations of models requires that you have a [LaTeX distribution](https://www.latex-project.org/get/) installed.

* macOS: install [MacTex](http://www.tug.org/mactex/)
* Linux: install [TexLive](http://www.tug.org/texlive)
* Windows: install [MiKTeX](http://miktex.org/) or [TexLive](http://www.tug.org/texlive)

### Within a Conda environment

 1. [Clone](https://help.github.com/articles/cloning-a-repository/) this repository.
 1. Install the conda package manager by [installing a version of Miniconda](https://conda.io/miniconda.html) appropriate to your operating system.
 1. Open a terminal within which conda is available; you can check this with 
 
    ```sh
    conda --version
    ```
 
 1. Create a new conda environment containing MuMoT and all dependencies: within the terminal navigate to the directory containing the clone of this repository and run:
 
    ```sh
    conda update conda
    conda env create -n mumot-env -f environment.yml
    ```

 1. Check that conda environment has been created: `mumot-env` should appear in the output from:
 
    ```sh
    conda env list
    ```

 1. *Activate* the environment:
 
    ```sh
    source activate mumot-env    # on macOS/Linux
    activate mumot-env           # on Windows
    ```

 1. *Install* MuMoT and dependencies into this conda environment:

    ```sh
    python -m pip install mumot
    ```

### Within a VirtualEnv

 1. [Clone](https://help.github.com/articles/cloning-a-repository/) this repository.
 1. Ensure you have the following installed:

     * [Python >= 3.4](https://www.python.org/downloads/)
     * the [pip](https://pip.pypa.io/en/stable/installing/) package manager (usually comes with Python 3.x but might not for certain flavours of Linux)
     * the [virtualenv](https://virtualenv.pypa.io/en/stable/) tool for managing Python virtual environments
     * [graphviz](https://graphviz.gitlab.io/download/)

    You can check this by opening a terminal and running:

    ```sh
    python3 --version
    python3 -m pip --version
    python3 -m virtualenv --version
    ```

 1. Create a Python virtualenv in your home directory:

    ```sh
    cd 
    python3 -m virtualenv mumot-env
    ```

 1. *Activate* this Python virtualenv:

    ```sh
    source mumot-env/bin/activate    # on macOS/Linux
    mumot-env/bin/activate           # on Windows
    ```

 1. *Install* MuMoT and dependencies into this Python virtualenv, then enable interactive Notebook widgets:

    ```sh
    python -m pip install mumot
    jupyter nbextension enable --py widgetsnbextension --sys-prefix
    ```

**STILL NEEDED?**
* if installed on Linux system you need to delete the following line (on macOS you can skip this step): - appnope=0.1.0=py35_0 as it is macOS specific (this is the first line under dependencies in the environment.yml file). 
* If you are using Ubuntu 16.04 or Mac osX the package graphviz is probably not working correctly (when installed via pip - this is done when creating the environment via the environment.yml file). This can be resolved by installing it again by typing: `sudo apt-get install graphviz` (Ubuntu) or `conda install graphviz` (Mac) in a terminal (you need to have root permissions, and make sure you have already run `activate MumotEnv`)

### (Optional) Enable tables of contents for individual Notebooks

Hyperlinked tables of contents can be userful when viewing longer Notebooks such as the [MuMoT User Manual](docs/MuMoTuserManual.ipynb).
Tables of contents can be displayed if you enable the **TOC2** Jupyter Extension as follows:

 1. If using conda:

    ```sh
    conda install -c conda-forge jupyter_nbextensions_configurator
    ```

    Or if using a virtualenv instead:

    ```sh
    pip install jupyter_nbextensions_configurator  # AND 
    jupyter nbextensions_configurator enable --user
    ```
    
 1. Start a Jupyter Notebook server with

    ```sh
    jupyter notebook
    ```
    
 1. Click the *nbextensions* tab and enable the *TOC2* extension.
 1. Subsequently, within any Notebook you can toggle the table of contents by clicking on the appropriate button in the toolbar.

## Starting using MuMoT

 1. Follow the install and post-install instructions above.  
    If you have already created your MuMoT conda environment or virtualenv you only need to *activate* it.
 1. Start a Jupyter Notebook server, unless you have done so already.

    ```sh
    jupyter notebook
    ```

 1. Within the Jupyter file browser, 
    browse to your clone of this repository, 
    find the `docs` subdirectory then 
    open [MuMoTuserManual.ipynb](docs/MuMoTuserManual.ipynb), which is the MuMoT User Manual.

## Testing

At present, MuMoT is tested by running several Jupyter notebooks:

* [docs/MuMoTuserManual.ipynb](docs/MuMoTuserManual.ipynb)
* [TestNotebooks/MuMoTtest.ipynb](TestNotebooks/MuMoTtest.ipynb)
* Further test notebooks in [TestNotebooks/MiscTests/](TestNotebooks/MiscTests)

To locally automate the running of all of the above Notebooks in an isolated Python environment containing just the necessary dependencies:

 1. Install the [tox](https://tox.readthedocs.io/en/latest/) automated testing tool
 2. Run 

    ```sh
    tox
    ```

This:
 
 1. Creates a new virtualenv (Python virtual environment) containing just 
      * MuMoT's dependencies  (see `install_requires` in [setup.py](setup.py))
      * the packages needed for testing (see `extras_require` in [setup.py](setup.py))
 1. Checks that all of the above Notebooks can be run without any unhandled Exceptions or Errors being generated 
    (using [nbval](https://github.com/computationalmodelling/nbval)).
    If an Exception/Error is encountered then a Jupyter tab is opened in the default web browser showing its location 
    (using [nbdime](https://nbdime.readthedocs.io/en/stable/)).
 1. Checks that the [docs/MuMoTuserManual.ipynb](docs/MuMoTuserManual.ipynb) and [TestNotebooks/MuMoTtest.ipynb](TestNotebooks/MuMoTtest.ipynb) Notebooks 
    generate the same output cell content as is saved in the Notebook files when re-run 
    (again, using [nbval](https://github.com/computationalmodelling/nbval)).
    If a discrepency is encountered then a Jupyter tab is opened in the default web browser showing details 
    (again, using [nbdime](https://nbdime.readthedocs.io/en/stable/)).
    
## Documentation

The [docs/MuMoTuserManual.ipynb](docs/MuMoTuserManual.ipynb) Notebook provides the most accessible introduction to working with MuMoT.

For more technical information read the documentation at [https://diodeproject.github.io/MuMoT/](https://diodeproject.github.io/MuMoT/)

## Contributing

If you want to contribute a feature or fix a bug then:

* Fork this repository and create a [feature branch](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
* Make commits to that branch
    * Style: write code using Python [naming conventions](https://www.python.org/dev/peps/pep-0008/#naming-conventions)
    * Testing: if you add new features, fix bug(s) or change existing functionality:
        * Add (lower-level) [unit tests](https://en.wikipedia.org/wiki/Unit_testing) to the Python source files in the [tests/](tests/) directory.
        * Add (higher-level) [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing)/[regression](https://en.wikipedia.org/wiki/Regression_testing) tests to 
          [TestNotebooks/MuMoTtest.ipynb](TestNotebooks/MuMoTtest.ipynb) or test notebooks to [TestNotebooks/MiscTests/](TestNotebooks/MiscTests). 
    * Documentation: Include Python docstrings documentation in the [numpydoc](http://numpydoc.readthedocs.io/en/latest/format.html) format 
      for all modules, functions, classes, methods and (if applicable) attributes.
    * Use `@todo` for reminders.
* When you are ready to merge that into the `master` branch of the 'upstream' repository:
    * Run all tests using `tox` (see [Testing](#testing)) *first*.


## Contributors

### Core Development Team:

* James A. R. Marshall
* Andreagiovanni Reina
* Thomas Bose

### Packaging, Documentation and Deployment:

* [Will Furnass](http://learningpatterns.me)

### Windows Compatibility

* Renato Pagliara Vasquez

## Funding

MuMoT developed with funds from the European Research Council (ERC) under the European Union's Horizon 2020 research and innovation programme (grant agreement number 647704 - [DiODe](http://diode.group.shef.ac.uk)).

## Included third-party code

* [mumot/process_latex/](mumot/process_latex): LaTeX parser; taken from [latex2sympy](https://github.com/augustt198/latex2sympy) project and updated for Python 3) ((C) latex2sympy, under the MIT license)
* [mumot/gen](mumot/gen): includes submodules used by MuMoT
* [mumot/__init__.py](mumot/__init__.py): contains functions (C) 2012 Free Software Foundation, under the MIT Licence
