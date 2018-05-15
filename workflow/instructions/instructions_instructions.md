# INSTRUCTIONS ON WRITING INSTRUCTIONS

The goal of the `ll-docs` repository is to offer thorough documentation of all the various things we need to know how to do, and to do so with new LL team members in mind.  These instructions will live on GitHub, and everyone will be learning how to add to them there.

## SETTING UP WORKING ENVIRONMENT

Before you even start typing instructions, you'll need to do a few things:
1. You'll need to make sure that you have git installed on the machine you're working on, which shouldn't be a problem if you are using one of the LL machines.  Try typing `git --version` into the Terminal.  If you don't see anything, you can install it [here](https://git-scm.com/download/mac).
2. You'll need to make sure that you have a text editor--we should have [Atom](https://atom.io/) installed on all the LL machines, and it's easily one of the best free options. Once you install it, be sure to click `Install Shell Commands`, which you'll find in the `Atom` menu once you open the app.
3. Get yourself into your working directory--we typically ask people on the team to use the `Development` folder we've created in the `Home` directory.  To get there, type `cd ~/Development`.  If you don't have that folder, or want to create another folder, go ahead and type something like
    ```
    cd ~
    mkdir Development
    cd Development
    ```
4. Log into GitHub (create an account if you don't already have one), and **fork** the repository by clicking the `fork` button on (this page)[https://github.com/learninglab-dev/ll-docs].  
5. Once on your new fork of the `ll-docs` repository, you'll want to click the green "clone or download" button and copy the code you see there. Making sure that you are in your `Development` directory, type `git clone` and then your url, making the whole command look something like `git clone https://github.com/learninglab-dev/ll-docs.git`.  This will create a new folder for `ll-docs` (go ahead and type `ls` to list the contents of your present working directory to confirm).
6. type `cd ll-docs` to change directories
7. type `atom .` to open up the root folder and all of its contents in Atom (this will only work if you have Atom Shell Commands installed).
