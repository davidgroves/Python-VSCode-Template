# Overview

This is a highly opininated guide on how to setup VScode for Python Development the way I personally like it, with a baseline Python project the way I also like it.

This doesn't mean I am correct, or someone with other preferences is incorrect, but this is what works for me.

## What is included in this skeleton

1. My vscode setup for Python, including what plugins I use (in `.vscode/settings.json`)
1. Examples for automated formatting with [black](https://black.readthedocs.io/en/stable/) and [isort](https://pycqa.github.io/isort/).
1. Examples for automated testing with [pytest](https://docs.pytest.org/).
1. Examples for automatically testing the documentation examples with pytest.
1. Examples for automated documentation building with [mkdocs](https://www.mkdocs.org/)
1. Examples for automatic linting with [pylint](https://pypi.org/project/pylint/)
1. Examples for automatic type checking with [mypy](https://mypy.readthedocs.io/en/stable/)
1. Examples for automatic testing in multiple environments with [tox](https://tox.wiki/)

## Software you need

Make sure the following applications are installed on your system globally. How you do this obviously varies depending on if you are using Windows, OSX or Linux.

- Python3
- Git
- Visual Studio Code

Note on Debian/Ubuntu based distributions, you will need to `apt-get install python3 python3-pip python3-venv git code`.

## How to setup

- Copy the contents of this git repo to your new project directory.
- Make a venv with `python -m venv .venv`.
- Update the `LICENSE` file with your appropriate license information.
- Replace this `README.md` file with an appropriate readme file.

You then need to install the development dependancies, and then the package in installable mode.

```console
pip install -r requirements-dev.txt
flit install
```

## How to use as a developer

### Use the package. It is fully installed and usable

```console
$ python
>>> import python_vscode_template.arithmetic as ar
>>> ar.add_ints(2,3)
5
```

### Format it with the [black](https://black.readthedocs.io/en/stable/) formatter

```console
$ black .
All done! ✨ 🍰 ✨
6 files left unchanged.
```

### Correct the import order with [isort](https://pycqa.github.io/isort/)

```console
$ isort .
Skipped 5 files
```

### Run the tests (from the commmand line)

```console
$ pytest
======================================= test session starts ========================================
platform linux -- Python 3.11.4, pytest-7.4.0, pluggy-1.2.0
rootdir: /home/dwg/CODE/Python-VSCode-Template
configfile: pyproject.toml
testpaths: tests
plugins: asyncio-0.21.1, anyio-3.7.1, cov-4.1.0
asyncio: mode=Mode.STRICT
collected 5 items                                                                                  

tests/test_arithmetic.py ....                                                                [ 80%]
tests/test_pokemon.py .                                                                      [100%]

======================================== 5 passed in 0.27s =========================================
```

### Verify the documentation tests (from the command line)




### Verify the type checking

```console
$ mypy src/
Success: no issues found in 4 source files
```

### Build the documentation and place the results in `site/`

```console
mkdocs build
```

### Start a documentation mini-webserver, that automatically updates

```console
mkdocs serve
```

### Run tests in multiple python environments

```console
tox
```

***

## Stuff you will need to edit

- `tox.ini`: Make sure `envlist` contains the versions of Python you want to test again. This example inclujdes
- `requirements-dev.txt`: Make sure this includes any developer only dependancies.
- `requirements.txt`: This should contain dependancies required to run the application or library. If you are making an application, you should pin each package to a specific version. If you are making a library, you should accept the minimum required version to allow users more choice. A library with a pinned version FORCES the user to install that version too, and is likely to clash with other libraries.
- `docs/`: The entry document is index.md, but you should write the docs as you see fit.
- `src/YOURPACKAGENAME`: This is where you will put the actual code you write
- `tests/`: This is where to write your tests. Files must start `test_` to be picked up by tests/

## Docstrings

See [arithmetic.py](src/python_vscode_template/arithmetic.py) for example docstrings. These are in [Google Docstring Format](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html).

## My Global VSCode Settings

- Press `CTRL K` then `CTRL T`, and select `Dark+` as the theme (or your prefered theme).
- Press `CTRL ,` then make sure `Auto Save` is set to `After Delay`.
- In the File menu, make sure `Auto Save` is ticked.
