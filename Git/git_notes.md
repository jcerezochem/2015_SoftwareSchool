23/06/2015
## GIT


If want to go back to a commit throwing away our last chages:

git reset --hard

The hystory keeps there forever. So take care with what you commit

If we accidently commit something private (e.g. a password), google for a solution..

REMOTES

All folder that are not on the current .git space. Could be a url (github), but also another folder in our computer
With a remote, we can:
 - Send things from our current folder: git push
 - Update our folder with the remote commetn: git pull

********************************************************************
To create an empty repo: do not click on add LICENSE nor README!!
********************************************************************

* Create link with github empty repo (inctruction also given by github)
git remote add origin https://github.com/jcerezochem/summer_school.git
git remote -v # check the remote
git push origin master # send my local repo to githum. Github says to use -u (which is used to add upstream (tracking) reference

Some notes abut markdown

--------------------------------
# Header 1
## Header 2
- bullets
  -indented
- another

1. item 1
  1. indented

1. numbering does not matter

--------------------------------

*****************
## Conflicts
*****************
If the same file changes in remote and in local and try to pull:
---------
error: Your local changes to the following files would be overwritten by merge:
        git_notes.md
Please, commit your changes or stash them before you can merge.
Aborting
-----------

We first commit our file. The git will try to do a good merge if there are no conflicts (e.g. differnt parts of the file were affected). If both changes were in the same part, the error is

-----------------------
Automezclado git_notes.md
CONFLICTO(contenido): conflicto de fusión en git_notes.md
Automatic merge failed; fix conflicts and then commit the result.
--------------------------

We check the differences with

git diff origin/master git_notes.md

And it is also shown in the file!! So that we simply need to go to the file and solve the conflicts manually

## Colaborating

We can allow someone as collaborator on our github repo. But this will allow him to change whatever without a check fom the owener. It is better to make a fork (this give us a repo that we can work with (hosted in our github), with clone, we only have a copy and cannot do anything if the owner of the repo do now allow us to do so.

So, normally, first fork in github, and then git clone to local to work with.

With my copy, I can do all changes I want. Then if I want to add my changes to the original repo, I can add a pull request.
First push to OUR github. Then from github, clik on the green button on top (with the arrows)

When you get a pull request, it appears in the rigth-side tab. We can 
* see the changes made, 
* add a comment 
Before accepting, we can ask to modify something we don't like (this can be used for colaborative papers..). This is like a chat
* accept

If afterwards, there are changes in the original repo, I can get them directly to my local copy, adding a new remote (pointing to the URL of the original githum repo)
git remote add nickname address


**********************
## GUI
**********************
The lecturer uses git-cola (give it a try)
It is used to replace command-line operations..


*******************
## Branching
*******************
Create a branch:

git checkout -b feature/somenewfeature # this is following the "git flow" nomenclature

* NOTE: Normally the master branch only has stable code.

To wiew branches in command line:

git log --oneline --all --decorate --branches

To send it to githum (remote in general)

git push origin feature/somenewfeature

and do the merging in github. Using the green button (the same used to manage pull requests before). This allows merging the new feature into the master through a pull request. This is usefull if we collaborate with others or even for us alone. Ones merged, the feature branch can be deleted










