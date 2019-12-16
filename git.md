# Git basics

Commit routine:
```sh
git status
git add ...
git status
git commit -m "${commit message}" -m "${commit description}"
```

Fix last commit message:
```sh
git commit --amend -m "${new commit message}"
```

Undo last commit:
```sh
git reset HEAD~1
```

List branches by date:
```sh
git branch --sort=committerdate
```

Switch branches:
```sh
git checkout ${existing branch}
```

Create a new branch and switch to it:
```sh
git checkout -b ${new branch}
```

Rename current local branch:
```sh
git branch -m ${new branch name}
```

Delete a local branch:
```sh
git branch -D ${existing local branch}
```

Push new branch to remote repository:
```sh
git push -u origin ${local branch}
```

Create a patch, check it, apply it:
```sh
git diff ${commit A} ${commit B} > diff_fromA_toB.patch
git apply --check diff_fromA_toB.patch
git apply diff_fromA_toB.patch
```

Apply version of a file from another branch:
```sh
git checkout ${reference branch} -- ${file}
```

Apply existing commit without commiting:
```sh
git cherry-pick -n ${commit}
```

Reset the state of a file:
```sh
git checkout -- ${file}
```

Reset the state of a branch:
```sh
git checkout ${branch}
git reset --hard origin/${branch}
```

Put aside current changes for later use (called _stash_):
```sh
git stash push -m "${description}"
```

List stash entries:
```sh
git stash list
```

Show a stash as a patch:
```sh
git stash show -p ${stash index}
```

Apply a stash:
```sh
git stash apply ${stash index}
```

Remove a stash:
```sh
git stash drop ${stash index}
```

Apply and remove a stash at the same time:
```sh
git stash pop ${stash index}
```

Put aside changes for some files only:
```sh
git stash push -m "${description}" -p ${file 1} ${file 2} ... ${file N}
```

Revert up to some specific commit and loose intermediate history (does not work on a protected branch):
```sh
git reset --hard ${commit}
git push origin HEAD --force
```

Add up-stream project and rebase on it:
```sh
# from the fork repository:
git remote add upstream ${Git project URL, either SSH or HTTP}
git fetch upstream
git rebase upstream/${branch}
```

Display the first commit of some user in current branch:
```sh
git log --author="${user}" --reverse --max-count=1
```
