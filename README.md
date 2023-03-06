What is this
============

This is a highly opininated guide on how to setup VScode for Python Development the way I personally like it.

This doesn't mean I am correct, or someone with other preferences is incorrect, but this is what works for me.

Software Installs
=================

Make sure the following applications are installed on your system globally. How you do this obviously varies depending on if you are using Windows, OSX or Linux.

 - Python3
 - Git
 - Visual Studio Code

Global VSCode Setup
===================

 - Press CTRL-K then CTRL-T, and select "Dark+" as the theme.
 - Press CTRL-, then make sure Auto Save is set to "On Delay".
 - In the File menu, make sure Auto Save is ticked.

Extensions
==========

See inside the `/template/` directory in this directory for an `extension.json` file. If this file is placed in your projects `.vscode` folder, the project will have my extensions as recommendations.

You can also manually search the VSCode store for the extension identifiers listed in that JSON document to install them manually.

Starting a New Project
======================

At a command prompt.

```bash
$ mkdir YOUR_PROJECT
$ cd YOUR_PROJECT
$ mkdir .vscode
$ cd .vscode
# Then copy the contents of .vscode/ from this git repo to the new folder you have created.
```