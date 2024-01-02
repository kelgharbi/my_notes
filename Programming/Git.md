* git checkout develop (switch to branch develop)

* git checkout -b vecto (basculement sur la nouvelle branche vecto)

* git push origin develop 
(Toujours faire ça au lieu de "git push", car si t'es pas dans la bonne branche ça risque de foirer dans le serveur)

* git reset --hard HEAD^ (elimine le dernier commit de la branche locale)

* git reset --hard HEAD (Attention : Cette commande va synchroniser l'état, ou le status de ta branche locale avec le HEAD, qui est le dernier commit sur ta branche) HEAD is origin/develop
```
git reset --hard origin/develop (synchronize with remote develop)

git reset --hard HEAD       (going back to HEAD)

$ git reset --hard HEAD^      (going back to the commit before HEAD)
$ git reset --hard HEAD~1     (equivalent to "^")

$ git reset --hard HEAD~2     (going back two commits before HEAD)
```

* $git restore < filename> (Cancel unstaged changes in the local repository, same as previous command)

* $git reset HEAD < filename1 > < filename2 > < filename3 > (untrack file or files, it's the reverse operation of "git add")

- Undo last push in Git and stash changes instead.
```
git reset --soft HEAD~1
git stash save "Saving instead" # or something like that
```

* $git status (Check if the files were indeed untracked)

* $git checkout HEAD -- < filename>
(reset the status of the file in the Git index, and it's working copy, to that of the HEAD)

- $git checkout tags/< tagname> -b develop
checkout the git tag, we specify the tagname and the branch to be checked out.

- $git diff
View unstaged changes comared to your last commit.
- $git diff --staged 
View staged changes compared to your last commit.
- 
* $git rm --cached < filename> (removes file from the git repository, without deleting it from filesystem => add file to .gitignore)

* $git diff < branch1> < branch2> (comparing two branches, such as comparing a local and a remote branch, e.g.: "git diff develop origin/WIP_3099")

- git clean -df  ( remove untracked files and repositories )

## Make a commit
* $git add .
*  $git commit -a
*  $git push origin develop

### Procedure pour rebaser une branche sur master
* $git stash
* $git checkout master
* $git pull
* $git checkout feature
* $git rebase master (OR git rebase -i master, rebase your changes in the current branch to the master branch, OR git merge master)
* $git status (we always use it after conflict resolution)

## How to merge a remote branch into your local branch
* $git fetch --all (OR git fetch remote_branch_name)
* $git branch -a (to see if the remote branch exists, in red if it exists remotely, in white if it exists in local, in green if it exists in local and if it's the current branch)
* $git stash (stash your local changes if any)
* $git checkout <remote_branch_name> (retrieve and switch to remote_branch_name to be your current branch)
* $git checkout <local_branch_name> (switch to local branch)
* $git merge <remote_branch_name>

## How to cherry pick a commit or multiple commits
If we want to cherry pick a commit from another branch :
* $git checkout release (we switch to the branch to which we want the commit to apply)
* $git cherry-pick < commitID> (if we want to cherry pick one commit, the commit could be from another branch)
* $git cherry-pick < commitID1> < commitID2> (cherry pick two commits)
* $git cherry-pick < commitID1> ... < commitIDn> (cherry pick the commits that are between commitID1 and commitIDn both included)

```
commit fca513a1c148a1d04034d4f285f4c691f575f831 (develop)
Author: Khaled <k.elgharbi.ext@pellencst.com>
Date:   Mon Nov 21 14:31:10 2022 +0100

    Resolves SN3-142: TSA2 [4.8 RC18] - 2.10.1 Site client Sietrem TO6 (M+1.4) - Sortie de tri suite erreurs 50000 / 51101 / 51102
    
    Crash dans StatisticsServer lorsqu'on fait un alignement des recettes/familles avec celles dans Fusion à l'initialisation du cache.
    (Contournement : Ne pas faire l'initialisation pour TSA2 on en a pas besoin, car on ne modifie  pas de recettes/familles)
    
    Author: KEI
    Reviewer: XCE
    Number of findings: 0
    Findings:
    Findings resolution:

commit 7d77f2979f26c2538821c9cb9f0cd5a84eca2f57 (origin/develop, origin/HEAD)
Author: xavier.cotte <xavier@pc-xavier.pellencst.com>
Date:   Fri Jul 29 16:23:22 2022 +0200

    Resolves LOG-5138: les stats calculés en surface affichent des pyramides en m²/h (1090%)
    
    Remise aux valeurs par défaut des stats visibles pour le client, après verolage du au passage de surfacique à massique
    
    Author: XCE
    Reviewer: VPY
    Number of findings: 0
    Findings:
    Findings resolution:




_________________________________________________________________________________
commit 5ce5892bfbe09a69ca52f8f8b4b6ae0d001f971c (HEAD, tag: xpert_2.0-4.8.0-rc1, tag: xpert_2.0-4.7.1, tag: mistralqc_2.1-4.6.0-rc13, tag: mistralqc_2.1-4.6.0-rc12, tag: mistralqc_2.1-4.6.0-rc11, tag: mistralqc_2.1-4.6.0-rc10)

Merge: 84db1bf 79c52aa

Author: Jola Greczka <j.boutry@pellencst.com>

Date:   Thu Jan 6 17:07:51 2022 +0100

    Merge branch 'develop' into release

```

___
## Useful commands
- git pull --rebase
-> A method of combining your local unpublished changes with the latest published changes on your remote.

## Git Submodules
- ```git clone git@frpstgit:OPCUA/mware.git``` -> main module, here we get the directories that contain the submodules but not the files within them yet. 
- ```git submodule update --init``` -> initialize local configuration file, and fetch all data from the project and checkout the appropriate commit. There is another way to do it with ```git clone --recurse-submodules git@frpstgit:OPCUA/mware.git 
- We suppose there is a commit made in libPstOpcUAModuleEnumerations ->```cd libPstOpcUAModuleEnumerations && git fetch && git pull --rebase```
- We can go back to the main directory to check -> ```cd .. && git diff --submodule```. If we don't want to write ```--submodule``` everytime we can do ```git config --global diff.submodule log```
- ```git submodule update --remote``` -> git update submodules
- ```git commit -am 'Update Submodule'
- ```git push origin mware
- 
- ```git submodule add git@frpstgit:OPCUA/libPstOpcUAModelEnumerations.git
- ```git status


- git submodule update --init libPstOpcUAModuleEnumerations
- git fetch --recurse-submodules
- git pull --recurse-submodules
- more .gitmodules
## Show the changes of a Stash
- git stash show -p  **(Show changes of the most recent stash)**
- git stash show -p stash@{1}  **(Show changes of the named stash)**
