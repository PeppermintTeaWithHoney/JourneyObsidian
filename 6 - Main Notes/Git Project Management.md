2025-10-08 12:56

Status: Ongoing

Tags: [[Git]]


## Git Project Management


Git a is a decentralized version control system. Its remembers things you changed and lets you easily work with a team. You can see changes and commits to it and who made them. 


## The git command

The git command with its numerous options let you control your project in the terminal. It allows you to save changed items in a commit, or download files from a for example a GitHub repository.
It also allows you to make branches and change between them for example main and development branch. Also to revert changes.


## Git GUI

Most modern IDE'S / Text-editors have inbuilt git functionality, that lets you easily do the basics of gits without knowing much, you should still learn all the git functionality otherwise you will sooner or later get into trouble. 

## Git versus GitHub versus GitLab


GitHub and GitLab aren't a alternative to Git they are a addition, they are just websites where you can use git to host your files.  They make it easier to exchange data and act as another backup.


# Downloading software on GitHub

We could download it as zip, or we can use git clone exampleurl.git.
git clone unpacks all files in the current directory.



## How to set your git credentials

we can use git config --global user.name "Example Name"
and git config --global user.email "example@email.com"


## How to give other people access to your GitHub repository

Go to your repo open settings and collaborators, there you can add people.
The more common way is to make a fork, change the stuff you wanted to change and do a pull-request 

# GitHub organization

Via Settings, Organization you can make a organization. Its basically a account who multiple persons have access to.

## Personal Access Token

To make a token, you have to go to settings,developer settings. There you can create a PAT.
You can put a name in and how long it should be activated. If its only for basic git operations you can click only on "repo" and give it just a basic access. If you generate the Token its only visible once, right after creating it.

## Working with the git command

To start using git, you have to set user.name and user.email.
If you have one set globally but you want a different one for a certain project. You can just cd into the project and set it without the --global flag.

## Git clone

Via git clone websiteishere.com/test.git
You can clone a repo from GitHub into your local drive.

## Git add

To add something to git you have to write git add nameofprogram.py
You can also use git stage its the same as add.

##  Git commit

to actually commit something you added you have to use git commit - m "message". the m flag stands for message which is needed in git.
Don't forget that before every commit you have to add the new files or files you changed something in before committing. You can skip add/stage if you write the -a flag into your commit. This will automatically add all files you did changes on and commits them. THIS DOES NOT WORK WITH new files, you have to add/stage them.

Git commit is LOCALLY ONLY.

## Git status


If you lost track of your commits you can check them with git status. Which gives you a nice little overview. 


## .gitignore

To ignore files aka not adding them to git you can make a .gitignore file and write the files in there you don't want added to the repo.


## Git push

The git push updates the commits from the local repository to another external one(for example GitHub). If we downloaded the repo with git clone git push is the same as git push origin main


## Git pull

The opposite of push is pull. This command downloads changes from the external repo to our local one. 



## USE git pull before git push

There can always be new changes, so pull before you push

## Uploading local repo to GitHub/GitLab

In practice its usually that you already have a local repo, maybe with a few files and you want to have a repo on GitHub for example. 
First you have to go into the directory and write git init. After that you git add them to the repo and git commit -m right after. After that we write git remote add origin git@github.comblabla.git, to check if it worked we write git remote -v .  And with git branch -M "name-here" we can rename the branch. And with git push -u uploads the the whole repo for the first time. The -u flag makes the the repo the main upstream one.
















# References
