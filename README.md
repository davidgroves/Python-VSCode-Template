
# OUTDATED. SEE REPLACEMENT.
# This is out of date, and has been replaced with a similar version which uses ruff rather than flake8 and black.
# See [Python-VSCode-Template2](https://github.com/davidgroves/Python-VSCode-Template2).

---
---
---
---

# Overview

This is a highly opininated guide on how to setup VScode for Python Development the way I personally like it, with a baseline Python project the way I also like it.

This doesn't mean I am correct, or someone with other preferences is incorrect, but this is what works for me.

Note this only works for pure Python projects. If your project requires C extensions or rust code, you will need to replace the flit builder with one that supports those things.

## The application

The application itself is a useless script called `my_script`, which is installed as a script. It adds two integers together that are given on the command line.

```console
$ my_script 2 3
5
```

There are also tests that use the Pokemon API to get pokemon by id.

FIXME: Add a script that uses that as well for better demoing.

This application can be installed with `pip install python_vscode_template`, but the point of this repository is to show you how that application was created, tested, packaged and distributed, not the actual application itself.

## What is included in this skeleton

1. My vscode setup for Python, including what plugins I use (in `.vscode/settings.json`)
1. Automatic Formatting with [black](https://black.readthedocs.io/en/stable/) and [isort](https://pycqa.github.io/isort/).
1. Testing with [pytest](https://docs.pytest.org/) (including documentation testing)
1. Documentation building with [mkdocs](https://www.mkdocs.org/)
1. Linting with [pylint](https://pypi.org/project/pylint/)
1. Static type checking with [mypy](https://mypy.readthedocs.io/en/stable/)
1. Automatic testing in multiple environments with [tox](https://tox.wiki/)
1. Examples for [Github Actions](https://github.com/features/actions) automation for running your tox test suite on commit.

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
- Make a `~/.pypirc` file in your homedirectory, based off [.pypirc-template](.pypirc-template)

You then need to install the development dependancies, and then the package in installable mode.

```console
pip install -r requirements-dev.txt
flit install
```

## Stuff you will need to edit in your own projects.

- [tox.ini](tox.ini): Make sure `envlist` contains the versions of Python you want to test again. This example includes
- [requirements-dev.txt](requirements-dev.txt): Make sure this includes any developer only dependancies.
- [requirements.txt](requirements.txt): This should contain dependancies required to run the application or library. If you are making an application, you should pin each package to a specific version. If you are making a library, you should accept the minimum required version to allow users more choice. A library with a pinned version FORCES the user to install that version too, and is likely to clash with other libraries.
- [docs/](docs/): The entry document is index.md, but you should write the docs as you see fit.
- [src/](src/): Update this with your package name.
- [tests/](tests/): This is where to write your tests. Files must start `test_` to be picked up by tests/


## My developer workflow

1. Use vscode tools while developing, [running tests out of vscode](#testing-from-within-vscode).
1. View the "problems" tab for things the linter has caught.
1. When ready to commit, I run `tox` from the command line.
1. If `tox` returns no errors, I can commit and push.
1. I can then verify github actions produces no errors on that push.
1. If I am publishing to pypi, I then run `flit --publish prodpypi`  


## Stuff you can do

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

```console
$ pytest --doctest-modules src/
====================================== test session starts ======================================
platform linux -- Python 3.11.4, pytest-7.4.0, pluggy-1.2.0
rootdir: /home/dwg/CODE/Python-VSCode-Template
configfile: pyproject.toml
plugins: asyncio-0.21.1, anyio-3.7.1, cov-4.1.0
asyncio: mode=Mode.STRICT
collected 1 item                                                                                                                      

src/python_vscode_template/arithmetic.py .                                                [100%]                                          
====================================== 1 passed in 0.03s =======================================
```

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

### Testing From within vscode

You can verify the tests using the testing flask icon on the left.

1. Brings up the testing dialog.
2. Can run or debug individual tests, by selecting them and using the icons.
3. Can rediscover, run all tests or debug all tests.

![vscode testing example](images/vscode_testing.png "VSCode Testing Example")

### On commit hooks on github.

A small icon will have been added to github by github actions. It will be a ✅ if the tests are passing, a ❌ if they are failing and a 🟤 if the tests are still running.

You can click on it to view the logs and see what tests have passed, or what tests are still running.

![github tests example](images/github_tests_passing.png "Github Tests Passing")

### Publishing docs to Github pages

You can do this with `mkdocs gh-pages`. This will push the documentation in `site/` to a github page.
You will get the URL to it from the command.

### Uploading to pypi

If you have never done this before, you need to make an account at [Pypi](https://pypi.org/).
Then in [Pypi - Manage Accounts](https://pypi.org/manage/account/), add 2FA and an API token.

Then repeat this for [TestPypi](https://test.pypi.org/) and [TestPypi - Manage Accounts](https://test.pypi.org/manage/account), add 2FA and a API token.

Then edit `.pypirc` in your home directory, and make it similar to [.pypirc-template](.pypirc-template) in this repo, except with the appropriate tokens.

To upload to pypi, make sure your git repo and working directory are up to date, and run `flit publish --repository prodpypi` or `flit pubish --repository testprod` as required. Running without `--repository` will specifically not work. This is done to make you select where to upload to.

If you publish to test and want to use it, from another virtual environment, do `pip install --index-url https://test.pypi.org/simple/ python_vscode_template`, or of course just `pip install python_vscode_template`.

The name of the package is decided by what is in [pyproject.toml](pyproject.toml), in the `[project]`, `name=` key.

---

## Misc Notes

### Docstrings

See [arithmetic.py](src/python_vscode_template/arithmetic.py) for example docstrings. These are in [Google Docstring Format](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html).

### Dist

`flit build` will put two files in the `dist/` directory. A source file and a wheel. Both of these are directly usable by pip to install.

## My Global VSCode Settings

- Press `CTRL K` then `CTRL T`, and select `Dark+` as the theme (or your prefered theme).
- Press `CTRL ,` then make sure `Auto Save` is set to `After Delay`.
- In the File menu, make sure `Auto Save` is ticked.
