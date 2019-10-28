# Genre Classifier
We are data mining a corpus of ancient texts to train machine learning classifiers that distinguish between different genres.
Link to paper: https://www.aclweb.org/anthology/W19-2507/

## Setup (Instructions for Mac)

Open the Terminal app

1. Check if you have `Python 3.6` installed:
	```bash
	which python3.6
	```
	If it is installed, this command should have output a path. For example: `/Library/Frameworks/Python.framework/Versions/3.6/bin/python3.6`. If nothing was output, download `Python 3.6` here: https://www.python.org/downloads/release/python-368/

1. Ensure that you have the Xcode command-line tools installed on your Mac by running the following:
	```bash
	xcode-select --install
	```
	If you are prompted with a dialog box, then select `Install`. This step ensures you have `git` and `svn` installed which are necessary to run the code in this project.

1. Check that you have `brew` installed:
	```bash
	which brew
	```
	If it is installed, this command should have output the following path: `/usr/local/bin/brew`. If nothing was output, install `brew` with the following command: 
	```bash
	/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	```

1. Install `pipenv`:
	```bash
	brew install pipenv
	```
	If `pipenv` had already been installed in the past but is not working, you may have to run `brew reinstall pipenv`.

1. Clone this repository - click on green 'clone' button on right side of github webpage for this repo to copy the link:
	```bash
	git clone <link you just copied>
	```

1. Navigate inside the project folder:
	```bash
	cd <the project folder you just cloned>
	```

1. Run
	```bash
	PIPENV_VENV_IN_PROJECT=true pipenv --python 3.8
	```
	This will generate a virtual environment called `.venv` in the current directory that will contain the Python dependencies for this project.<sup id="a1">[1](#f1)</sup>

1. Activate virtual environment:
	```bash
	pipenv shell
	```
	Now, running `Python` commands will ignore the system-level `Python` version & packages, and only use the packages from the virtual environment.

1. Install dependencies: 
	```bash
	pipenv install
	```
	This will install all the packages with versions specified by `Pipfile.lock` into the virtual environment.

1. To leave the virtual environment, use 
	```bash
	exit
	```
	This will restore the system-level Python configurations to your shell.

1. To start the virtual environment again, use the following while in the project directory:
	```bash
	pipenv shell
	```
	This will again make `Python` use the configurations in the project's virtual environment.

## Analysis
Here are examples of commands you can run:

Run the demo (this does a feature extraction for a small sample of files, and analyzes the results in one step):
```bash
python demo.py
```

Extract features from all files:
```bash
python run_feature_extraction.py all_data.pickle
```

Extract features from only drama and epic files:
```bash
python run_feature_extraction.py drama_epic_data.pickle drama epic
```

Run all model analyzer functions on the data from all files to classify prose from verse:
```bash
python run_ml_analyzers.py all_data.pickle labels/prosody_labels.csv all
```

Run all model analyzer functions on the data from only drama and epic files to classify drama from epic:
```bash
python run_ml_analyzers.py drama_epic_data.pickle labels/genre_labels.csv all
```

## Footnotes

<b id="f1">1)</b> The `pipenv` tool works by making project-specific directories (called virtual environments) that hold the dependencies for that project. Setting the `PIPENV_VENV_IN_PROJECT` environment variable will indicate to `pipenv` to make this virtual environment within the same directory as the project so that all the files corresponding to a project can be in the same place. This is [not default behavior](https://github.com/pypa/pipenv/issues/1382) (e.g. on Mac, the environments will normally be placed in `~/.local/share/virtualenvs/`). [↩](#a1)
