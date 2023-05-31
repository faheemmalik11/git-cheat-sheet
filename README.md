# Git

* [I want to show the status of the current branch.](#status)

* [I want to create a new branch that is based on the current branch.](#i-want-to-create-a-new-branch-that-is-based-on-the-current-branch)

* [I want to checkout the previous branch that I was on.](#i-want-to-checkout-the-previous-branch-that-i-was-on)

* [I want to list the files that have been modified in the current working tree.](#i-want-to-list-the-files-that-have-been-modified-in-the-current-working-tree)

### status

The `status` command shows differences between the working tree, the index, and `head` commit.
​
```sh
git status
```



### I want to create a new branch that is based on the current branch.
​
In general, you want to implement new features in short-lived "feature branches" so that changes can be isolated. You can use the `checkout` command to create a new branch based on the current branch:
​
```sh
git checkout master
​
# Creates a new branch, `my-feature`, based on `master`.
git checkout -b my-feature
```

### I want to checkout the previous branch that I was on.
​
In some of the `git` commands, the `-` token refers to the "last branch" that you had checked-out. This makes it very easy to jump back-and-forth between two branches:
​
```sh
git checkout master
git checkout my-feature
​
# At this point, the `-` refers to the `master` branch.
git checkout -
​
# At this point, the `-` refers to the `my-feature` branch.
git checkout -
```
​
The `-` token can also be used to merge-in the last branch that you had checked-out:
​
```sh
git checkout my-feature
# ... changes to the working tree (your file system).
git add .
git commit -m "Awesome updates."
git checkout master
​
# At this point, the `-` refers to the `my-feature` branch.
git merge -
```
​
The `-` token can also be used to `cherry-pick` the most recent commit of the last branch that you had checked-out:
​
```sh
git checkout my-feature
# ... changes to the working tree (your file system).
git add .
git commit -m "Minor tweaks."
​
git checkout master
​
# At this point, the `-` refers to the `my-feature` branch.
git cherry-pick -
```

### I want to list the files that have been modified in the current working tree.
​
By default, when you call `git diff`, you see all of the content that has been modified in the current working tree (and not yet staged). However, you can use the `--stat` modifier to simply list the files that have been modified:
​
```sh
git diff --stat
```
​
