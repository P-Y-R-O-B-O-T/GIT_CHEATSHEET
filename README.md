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
| `git push REMOTE_ALIAS BRANCH_NAME` | Push to remote repo's particular branch, generally `BRANCH_NAME=main` |
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
* Alternative to `git pull origin BRANCH_NAME`
* `git fetch BRANCH_NAME --all`
* `git checkout BRANCH_NAME`
* `git merge REMOTE_ALIAS/BRANCH_NAME`

## TO NOTE
* **Working Area**: All active changes
* **Staging Area**: Contains the changes
* **Commited Area**: Stores all the commited changes
* **HEAD**: Pointer to last commit in the current branch
* **.gitignore**: files to ignore

* Files are first added from working area to staging area and then commited to the commited area

* Each git commit should be atomic, which means it should be independent, which means it must solve bug or a completely added feature etc

* Never use rebasing in public repo
