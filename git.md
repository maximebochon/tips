# Git basics

Commit routine:
```sh
git status
git add ...
git status
git commit -m "<commit_description>"
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
