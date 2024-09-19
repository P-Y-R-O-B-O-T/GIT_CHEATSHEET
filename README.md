# GIT CHEATSHEET
![](ZZZ/ZZZ.jpg) 

## CONFIG NAME AND EMAIL
| Command | Description |
|---------|-------------|
| `git config user.name "NAME"` | Config name |
| `git config eser.email "EMAIL"` | Config email |

## BASIC
| Command | Description |
|---------|-------------|
| `git help SUBCOMMAND` | Get help for git commands |
| `git init` | Init a local repo |
| `git status` | Gets status of changes on current branch |
| `git add FILES_DIRECTORY` | Add items to staging area |
| `git add .` | Add everything to staging area |
| `git commit -m "MESSAGE"` | Commit changes |

## WHEN FILE IS STAGED and CHANGED AFTER STAGING
| Command | Description |
|---------|-------------|
| `git restore FILE` | Restore the file to the state when it was staged or committed |
| `git restore --staged FILE` | Unstage the file |
| `git rm --cached FILE` | Prevent a file from being tracked |
| `git rm -f FILE` | Prevent a file from being tracked and delete it |

## BRANCHING
| Command | Description |
|---------|-------------|
| `git checkout -b BRANCH_NAME` | Create a new branch and switch to it |
| `git checkout BRANCH_NAME` | Switch to existing branch |
| `git branch` | Show all and current branch |
| `git branch -d BRANCH_NAME` | Delete a branch |
| `git merge BRANCH_NAME` | Merge a branch into current branch: `fast-forward` `non-fast-forward` |

## REMOTE_REPO
| Command | Description |
|---------|-------------|
| `git remote add REMOTE_ALIAS ACCESS_STRING` | Connect to remote repo, generally `REMOTE_ALIAS=origin` |
| `git remote -v` | List all remote repos |
| `git push REMOTE_ALIAS BRANCH_NAME` | Push to remote repo's particular branch, generally `BRANCH_NAME=main` for single handed project |
| `git push REMOTE_ALIAS BRANCH_NAME --force` | Force push to remote repository |
| `git clone ACCESS_STRING` | Clone a repo |
| `git pull REMOTE_ALIAS BRANCH_NAME` | Pull updates from remote repo |

## REBASE and CHERRYPICK
| Command | Description |
|---------|-------------|
| `git rebase BRANCH_NAME` | Pull another branch's update in current branch |
| `git cherry-pick COMMIT_ID` | Replicate a particular commit of a branch on another branch |

## RESET REVERT
| Command | Description |
|---------|-------------|
| `git revert COMMIT_ID` | Creates a new commit by reversing all changes made by the COMMIT_ID |
| `git reset --soft HEAD~N` | Go back N commits but keep the files intact |
| `git reset --hard HEAD~N` | Go back N commits and delete the changes made after that commit |
| `git reset --soft COMMIT_ID` | Go to specific commit and keep the current changes |
| `git reset --hard COMMIT_ID` | Go to specific commit and delete the changes made after that commit |

## STASH
| Command | Description |
|---------|-------------|
| `git stash list` | List all stashes |
| `git stash show STASH_ID` | List contents of a stash |
| `git stash pop STASH_ID` | Get contents of stach to working area |
| `git stash` | Push changes to stash |

## LOGS
| Command | Description |
|---------|-------------|
| `git reflog` | Tells state of repo. List all actions taken so far. Helps in resetting changes that we did. |
| `git log` | Gets all data regarding commits and hashes. |

## SYNCING REMOTE REPO MANUALLY
* Alternative to `git pull REMOTE_ALIAS BRANCH_NAME`

> [!NOTE]
> ### STEPS
> * `git fetch BRANCH_NAME --all`
> * `git checkout BRANCH_NAME`
> * `git merge REMOTE_ALIAS/BRANCH_NAME`

## TO NOTE
* **Working Area**: All active changes
* **Staging Area**: Contains the changes
* **Stash Area**:
    - If needed to work on multiple branches at the same time, before working on the different branch, we put current changes to stash area
* **Commited Area**: Stores all the commited changes
* **HEAD**: Pointer to last commit in the current branch
* **.gitignore**: files to ignore
* **Branch**: Pointer to a specific commit in the codebase
* **Rebasing**:
    - Rebasing is putting one branch on top of another one
    - When we rebase, we copy all the commits from one to another branch
    - We change the history of branch when we rebase

* Files are first added from working area to staging area and then commited to the commited area

* Each git commit should be atomic, which means it should be independent, which means it must solve bug or a completely added feature etc

* Never use rebasing in public repo

## SENARIOS

> [!TIP]
> ### SENARIO_1
> * `ana` on `BRANCH1`
> * `ana` created a file `F1`
> * `ana` wants to work on another idea which need `F2`
>
> ### SOLUTION
> * Create a new branch `BRANCH2`, switch to it and work on it


> [!TIP]
> ### SENARIO_2 = SENARIO_1+
> * `ana` finds a typo in `F1` on `BRANCH1` but havent completed work on `BRANCH2`
> * `ana` wants to fix the error asap
>
> ### SOLUTION
> * Add and commit `F2` on `BRANCH2`
> * Switch to `BRANCH1`, rectify the error, commit `F1` on `BRANCH1`
> * After that, complete work on `F2` on `BRANCH2`
> * Switch to `BRANCH1`
> * Merge `BRANCH2` into `BRANCH1` using `git merge BRANCH2`


> [!TIP]
> ### SENARIO_3
> * There is need to see which branch is the parent of current branch
>
> ### SOLUTION
> * Get onto current branch, run `git log --graph --decorate`


> [!TIP]
> ### SENARIO_4
> * `sam` wants to work on a feature and he have cloned a repository
>
> ### SOLUTION
> * Create a new branch, commit changes to it
> * Push the branch to the remote repository `git push REMOTE_ALIAS BRANCH_NAME`


> [!TIP]
> ### SENARIO_5
> * `ana` want to work on a feature on file `F1`
> * The repository clone is a bit older and new changes are not in `ana`'s local repo
>
> ### SOLUTION_1
> * Switch to branch `git checkout BRANCH_NAME`
> * Fetch changes `git fetch REMOTE_ALIAS BRANCH_NAME`
> * View all branches (local and remote) `git branch -a`
> * Update local branch name by merging remote branch `git merge REMOTE_BRANCH_NAME`
>
> ### SOLUTION_2
> * `git pull REMOTE_ALIAS BRANCH_NAME`


> [!TIP]
> ### SENARIO_6
> * `max` have local repo for the project and other developers are commiting changes to the remote repo, `max` is out of sync
> * `max` also have commited changes to his local repository
> * `max` changed a file and other developer changed the same file too, pulling changes creates merge conflicts
>
> ### SOLUTION
> * Commit the changees `git commit -am "MESSAGE"`
> * Running `git push REMOTE_ALIAS BRANCH_NAME` will result in rejection due to out of sync of out local repository
> * Pull the changes `git pull REMOTE_ALIAS BRANCH_NAME` (creates merge conflicts and also lists files which led to it)
> * See logs to see who commited the file `git log REMOTE_ALIAS/BRANCH_NAME`
> * Solve the merge conflict manually
>     - < HEAD shows our commited data
>     - > HASH shows remote commited data
> * Rectifi everything and try to edit those files (vary carefully)
> * Now commit the new changes `git commit -am "MESSAGE"`
> * Push changes to remote `git push REMOTE_ALIAS BRANCH_NAME`


> [!TIP]
> ### SENARIO_7
> * `ana` is working on a file `F1` in `BRANCH2`
> * Other developers have pushed changes on remote repository in `BRANCH1` (parent branch of `BRANCH1`)
> * We need to pull the changes on parent branch and solve the conflict in merging
> * Update our current working branch `BRANCH2` according to new data in parent branch `BRANCH1`
> * After she complete, she do not want to make multiple commits to the branch, require only one commit
> ### SOLUTION
> * Checkout the parent branch `BRANCH1`
> * Pull the changes `git pull REMOTE_ALIAS BRANCH1`
> * Checkout child branch `BRANCH2`
> * Rebase the current branch on parent branch `git rebase BRANCH1`
> * Complete the working on the file
> * Squash all commits in single commit while being on child branch `BRANCH2` `git rebase -i HEAD~N`, here N commits will be squashed, enter the message in the opening editor as new commit (also change the lines having pick to squash except the first one)


> [!TIP]
> ### SENARIO_8
> * `max` is working on a branch `BRANCH2`
> * Other developers are working on parent branch `BRANCH1` and making commits
> * `max` wanto replicate a commit on his branch that a developer made on another branch
>
> ### SOLUTION
> * `git checkout BRANCH2`
> * `git cherry COMMIT_ID`


> [!TIP]
> ### SENARIO_9
> * `ana` is working on a task, but she got another task in mind and completed it too and by mistake she comitted both tasks in single commit
>
> ### SOLUTION
> * `git rev --soft HEAD~1`
> * Then complete the work in sequential manner and commit one by one


> [!TIP]
> ### SENARIO_10
> * `max` are working on a branch `BRANCH1` and parallely on `BRANCH2`
> * Need to make change on `BRANCH2` while currently on `BRANCH1` or maybe on the same branch due to need of rectification of error
> * `max` first needs to rectify the error and then resume his work
>
> ### SOLUTION
> * Put changes to stash `git stash`
> * Rectify the error
> * Commit error rectification
> * Pop stash `git stash pop STASH_ID`
> * Continue working

> [!TIP]
> ### SENARIO_11
> * `max` is working on a project and he realizes he needs to update a major change (a big file in the project an image or something)
> * This if he commits the large file the log files get larger
> * We need to push this change to remote repository too
>
> ### SOLUTION
> * Clone the repository
> * Do a soft reset till the point where we introduced the large file for the first time `git reset --soft HEAD~N`
> * Edit the large file
> * Commit the changes `git add . && git commit -m "MESSAGE"`
> * Force push the changes to remote repository `git push REMOTE_ALIAS BRANCH_NAME --force`
