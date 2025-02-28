# Steps

An example data science project to demonstrate GitHub.

## 1. [Create a conda environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-with-commands)  

Ensure you have 1 conda environment per project.

You can install any libraries you like.  

For example, here we're installing Python 3.8, [Jupyter Lab](https://jupyter.org/) for the [Integrated Development Environment (IDE)](https://carpentries-incubator.github.io/python-intermediate-development/13-ides/index.html), [Jupyter Book](https://jupyterbook.org/intro.html) for the [documentation](https://www.software.ac.uk/blog/2019-06-21-what-are-best-practices-research-software-documentation), [NumPy](https://numpy.org/) for some scientific computing, [cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) for a project template, and [pytest](https://docs.pytest.org/en/6.2.x/) for [testing](https://alan-turing-institute.github.io/rse-course/html/module05_testing_your_code/05_00_introduction.html).  

```bash
conda create -n example_project -c conda-forge python==3.8.* jupyterlab jupyter-book numpy cookiecutter pytest
conda activate example_project
```    

To recreate this environment from the conda file (you may want to rename the project first on line 1 within this file):

```bash
conda env create --file environment.yml
```

If you also want to use Jupyter Lab for development, then create a [kernel](https://jupyterlab.readthedocs.io/en/stable/user/running.html) for this environment:
```bash
python -m ipykernel install --user --name example_project --display-name "example_project"
```

## 2. Create a structure for the project

You can search for different project templates [here](http://cookiecutter-templates.sebastianruml.name/).  

For example, using [cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) and the [data science template](https://github.com/drivendata/cookiecutter-data-science):

```bash
cookiecutter -c v1 https://github.com/drivendata/cookiecutter-data-science
# fill in details
cd example_project
```    

Read the [templates documentation](http://drivendata.github.io/cookiecutter-data-science/) for more information.

### Project Organization

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io

## 3. [Create a GitHub repository](https://docs.github.com/en/get-started/quickstart/create-a-repo)  

[Initialise the repository](https://docs.github.com/en/get-started/importing-your-projects-to-github/importing-source-code-to-github/adding-an-existing-project-to-github-using-the-command-line).  

For example (remember to replace _username_ with your GitHub username):

```bash
git init
git add .
git commit -am "Initialising repository"
git branch -M main
git remote add origin git@github.com:username/example_project.git
git push -u origin main
```    

More information:
- [Version control (Software Carpentry)](https://swcarpentry.github.io/git-novice/)
- [Version control (The Alan Turing Institute)](https://alan-turing-institute.github.io/rse-course/html/module04_version_control_with_git/04_00_introduction.html)

## 4. Create the [documentation](https://www.software.ac.uk/blog/2019-06-21-what-are-best-practices-research-software-documentation)

For (at least) the key functionality.  

For example, using [Jupyter Book](https://jupyterbook.org/start/your-first-book.html):

```bash
rm -rf docs # as the default within the template uses Sphinx

jupyter-book create docs

jupyter-book build docs

git add docs
git commit -am "Adding documentation"
git push
```

Can view the documentation locally by viewing the file `docs/_build/html/intro.html` within a browser.

## 5. Add code and data

- Source code: [`src/`](https://github.com/ARCTraining/example_project/tree/main/src)  
    For example:  
    ```bash
    (example_project)$ pwd
    /home/lukeconibear/example_project
    (example_project)$ python
    Python 3.8.12 | packaged by conda-forge | (default, Jan 30 2022, 23:53:36)
    [GCC 9.4.0] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>> from src.data import make_dataset
    >>> make_dataset
    <module 'src.data.make_dataset' from '/home/lukeconibear/example_project/src/data/make_dataset.py'>
    >>>
    ```
- Jupyter notebooks: [`notebooks/`](https://github.com/ARCTraining/example_project/tree/main/notebooks) 
- Data: [`data/`](https://github.com/ARCTraining/example_project/tree/main/data)    

## 6. Add [tests](https://alan-turing-institute.github.io/rse-course/html/module05_testing_your_code/05_00_introduction.html)

For (at least) the key functionality.  

For example, [`pytest`](https://docs.pytest.org/en/6.2.x/):

```bash
mkdir tests
```

Create files within `tests/` e.g., `test_example.py`:

```python
def increment_by_one(x):
    return x + 1


def test_increment_by_one():
    assert increment_by_one(3) == 4
    
```

Then run pytest in the terminal:

```bash
$ pytest
================================================ test session starts ================================================
platform linux -- Python 3.10.2, pytest-7.0.0, pluggy-1.0.0
rootdir: /home/earlacoa/repos/example_project
plugins: anyio-3.5.0
collected 1 item                                                                                                    

tests/test_example.py .                                                                                       [100%]

================================================= 1 passed in 0.02s =================================================
```

## 7. Automate your workflow

To build the documentation, run tests, build modules, release packages, publish to GitHub pages, and more.  

For example, using [GitHub Actions](https://github.com/features/actions), see [`.github/workflows/deploy.yml`](https://github.com/ARCTraining/example_project/blob/main/.github/workflows/deploy.yml).

## 8. [Capture your environment](https://the-turing-way.netlify.app/reproducible-research/renv.html)

For reproducibility.

For example, using [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#sharing-an-environment):

```bash
conda env export --name example_project > environment.yml

rm -f requirements.txt # alternate method

git add environment.yml
git commit -am "Adding conda environment"
git push
```

## 9. [Choose a software license](https://the-turing-way.netlify.app/reproducible-research/licensing.html)

- Create/update the [`LICENSE`](https://github.com/ARCTraining/example_project/blob/main/LICENSE) file

## 10. Update [README](https://the-turing-way.netlify.app/project-design/project-repo/project-repo-readme.html)

- Describe project
- Steps to reproduce
- Key resources
- How to cite
- How to contribute

## 11. Publish online

For example, using [GitHub Pages](https://pages.github.com/) (for a [Jupyter Book](https://jupyterbook.org/start/publish.html)):

- Settings > Pages > Source = `Branch: gh-pages`.

Now, viewable [here](https://arctraining.github.io/example_project/).

## 12. [Release your project and make it citable](https://the-turing-way.netlify.app/communication/citable.html)

- [Create the release](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)
    - e.g., [v0.0.1: Pre-release](https://github.com/ARCTraining/example_project/releases/tag/v0.0.1)
- [Cite it](https://docs.github.com/en/repositories/archiving-a-github-repository/referencing-and-citing-content) using [Zenodo](https://zenodo.org/)
    - [Create](https://the-turing-way.netlify.app/communication/citable/citable-cff.html#) the [`CITATION.cff`](https://github.com/ARCTraining/example_project/blob/main/CITATION.cff) file
