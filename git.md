# Git basics

Commit routine:
```sh
git status
git add ...
git status
git commit -m "${commit message}" -m "${commit description}"
```

&nbsp;

Show changes on staged files only:
```
git diff --cached
```

&nbsp;

Fix last commit message:
```sh
git commit --amend -m "${new commit message}"
```

&nbsp;

Undo last commit:
```sh
git reset HEAD~1
```

&nbsp;

List branches by date:
```sh
git branch --sort=committerdate
```

&nbsp;

Switch branches:
```sh
git checkout ${existing branch}
```

&nbsp;

Create a new branch and switch to it:
```sh
git checkout -b ${new branch}
```

&nbsp;

Rename current local branch:
```sh
git branch -m ${new branch name}
```

&nbsp;

Delete a local branch:
```sh
git branch -D ${existing local branch}
```

&nbsp;

Push new branch to remote repository:
```sh
git push -u origin ${local branch}
```

&nbsp;

List files modified between two commits:
```sh
git diff --name-only ${commit A} ${commit B}
```

&nbsp;

Create a patch, check it, apply it:
```sh
git diff ${commit A} ${commit B} > diff_fromA_toB.patch
git apply --check diff_fromA_toB.patch
git apply diff_fromA_toB.patch
```

&nbsp;

Apply version of a file from another branch:
```sh
git checkout ${reference branch} -- ${file}
```

&nbsp;

Apply existing commit without commiting:
```sh
git cherry-pick -n ${commit}
```

&nbsp;

Reset the state of a file:
```sh
git checkout -- ${file}
```

&nbsp;

Reset the state of a branch:
```sh
git checkout ${branch}
git reset --hard origin/${branch}
```

&nbsp;

Put aside current changes for later use (called _stash_):
```sh
git stash push -m "${description}"
```

&nbsp;

List stash entries:
```sh
git stash list
```

&nbsp;

Show a stash as a patch:
```sh
git stash show -p ${stash index}
```

&nbsp;

Apply a stash:
```sh
git stash apply ${stash index}
```

&nbsp;

Remove a stash:
```sh
git stash drop ${stash index}
```

&nbsp;

Apply and remove a stash at the same time:
```sh
git stash pop ${stash index}
```

&nbsp;

Put aside changes for unstaged files only:
```sh
git stash --keep-index
```

&nbsp;

Put aside changes for some files only:
```sh
git stash push -m "${description}" -p ${file 1} ${file 2} ... ${file N}
```

&nbsp;

Revert up to some specific commit and loose intermediate history (does not work on a protected branch):
```sh
git reset --hard ${commit}
git push origin HEAD --force
```

&nbsp;

Add up-stream project and rebase on it:
```sh
# from the fork repository:
git remote add upstream ${Git project URL, either SSH or HTTP}
git fetch upstream
git rebase upstream/${branch}
```

&nbsp;

Display the first commit of some user in current branch:
```sh
git log --author="${user}" --reverse | head -4
```

&nbsp;

Display ignored files:
```sh
git status --ignored
```
