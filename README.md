# Ancient Greek Genre Classifier
We are data mining a corpus of ancient texts to train machine learning classifiers that distinguish between different genres.  
Replication code for Gianitsos et al., "Stylometric Classification of Ancient Greek Literary Texts by Genre," LaTeCH-CLfL 2019  
Link to paper: https://www.aclweb.org/anthology/W19-2507/

## Setup (Instructions for non-technical users on Mac)

Open the Terminal app

1. Check that you have `Python 3.6` installed:
	```bash
	which python3.6
	```
	If it is installed, this command should have output a path. For example: `/Library/Frameworks/Python.framework/Versions/3.6/bin/python3.6`. If nothing was output, download `Python 3.6` here: https://www.python.org/downloads/release/python-368/

1. Ensure that you have the Xcode command-line tools installed on your Mac by running the following. If the tools are already installed, it will not do anything harmful. This step ensures you have `git` and `svn` installed which are necessary to run the code in this project.
	```bash
	xcode-select --install
	```

1. Install `pipenv`<sup id="a1">[1](#f1)</sup>. If already installed, this command will not do anything harmful.
	```bash
	pip install pipenv
	```

1. Clone this repository - click on green 'clone' button on the right side of the Github webpage for this repo to copy the link:
	```bash
	git clone <link you just copied>
	```

1. Navigate inside the project folder:
	```bash
	cd <the project folder you just cloned>
	```

1. Now that you are in the project directory, run the following command. This will generate a virtual environment called `.venv` in the current directory<sup id="a2">[2](#f2)</sup> that will contain the Python dependencies for this project.
	```bash
	PIPENV_VENV_IN_PROJECT=true pipenv install
	```

1. This will activate the virtual environment. After activation, running `Python` commands will ignore the system-level `Python` version & packages, and only use the packages from the virtual environment.
	```bash
	pipenv shell
	```

Using `exit` will exit the virtual environment i.e. it restores the system-level `Python` configurations to your shell. You can also simply close the terminal. Whenever you want to resume working on the project, run `pipenv shell` while in the project directory to activate the virtual environment again.

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

<b id="f1">1)</b> The `pipenv` tool works by making a project-specific directory called a virtual environment that hold the dependencies for that project. After a virtual environment is activated, newly installed dependencies will automatically go into the virtual environment instead of being placed among your system-level `Python` packages. This precludes the possiblity of different projects on the same machine from having dependencies that conflict with one another. [↩](#a1)

<b id="f2">2)</b> Setting the `PIPENV_VENV_IN_PROJECT` variable to true will indicate to `pipenv` to make this virtual environment within the same directory as the project so that all the files corresponding to a project can be in the same place. This is [not default behavior](https://github.com/pypa/pipenv/issues/1382) (e.g. on Mac, the environments will normally be placed in `~/.local/share/virtualenvs/` by default). [↩](#a2)
