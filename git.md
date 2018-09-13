# Git basics

Commit routine:
```sh
git status
git add ...
git status
git commit -m "<commit_message>"
```

Fix last commit message:
```sh
git commit --amend -m "<new_commit_message>"
```

List branches:
```sh
git branch
```

Switch branches:
```sh
git checkout <existing_branch>
```

Create a new branch and switch to it:
```sh
git checkout -b <new_branch>
```

Rename current local branch:
```sh
git branch -m <new_branch_name>
```

Delete a local branch:
```sh
git branch -D <existing_local_branch>
```

Push new branch to remote repository:
```sh
git push -u origin <local_branch>
```

Create a patch, check it, apply it:
```sh
git diff <commit_A> <commit_B> > diff_fromA_toB.patch
git apply --check diff_fromA_toB.patch
git apply diff_fromA_toB.patch
```

Apply version of a file from another branch:
```sh
git checkout <reference_branch> -- <file>
```

Reset the state of a file:
```sh
git checkout -- <file>
```

Reset the state of a branch:
```sh
git checkout <branch>
git reset --hard origin/<branch>
```

Put aside current changes for later use (called _stash_):
```
git stash push -m "<description>"
```

List stash entries:
```
git stash list
```

Show a stash as a patch:
```
git stash show -p <stash index>
```

Apply a stash:
```
git stash apply <stash index>
```

Remove a stash:
```
git stash drop <stash index>
```

Apply and remove a stash at the same time:
```
git stash pop <stash index>
```

Put aside changes for some files only:
```
git stash push -m "<description>" -p <file 1> <file 2> ... <file N>
```

Revert up to some specific commit and loose intermediate history (does not work on a protected branch):
```
git reset --hard <commit>
git push origin HEAD --force
```
