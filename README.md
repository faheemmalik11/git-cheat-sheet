# Git

* [I want to show the status of the current branch.](#status)

* [I want to create a new branch that is based on the current branch.](#i-want-to-create-a-new-branch-that-is-based-on-the-current-branch)

* [I want to checkout the previous branch that I was on.](#i-want-to-checkout-the-previous-branch-that-i-was-on)

* [I want to list the files that have been modified in the current working tree.](#i-want-to-list-the-files-that-have-been-modified-in-the-current-working-tree)

* [I want to view the changes that were made in a given commit.](#i-want-to-view-the-changes-that-were-made-in-a-given-commit)

* [I want to list the files that were changed in a given commit.](#i-want-to-list-the-files-that-were-changed-in-a-given-commit)


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

### I want to view the changes that were made in a given commit.
​
When `show` is given a branch name, it will default to `head` - the last or most-recent commit on the given branch:
​
```sh
git checkout master
​
# Outputs the changes made to the `head` commit of the current (`master`)
# branch.
git show
​
# Outputs the changes made to the `head` commit of the `my-feature` branch.
git show my-feature
```
​
You can also use the `show` command to target a specific commit that is not the `head` commit. This can be done with a specific commit hash; or, a relative commit operator like `~`:
​
```sh
# Outputs the changes made in the commit with the given hash.
git show 19e771
​
# Outputs the changes made in in a previous commit of the current (`master`)
# branch.
git show head~ # Show changes in first parent.
git show head~~ # Show changes in first parent's first parent.
git show head~~~ # Show changes in first parent's first parent's first parent.
​
# Outputs the changes made in a previous commit of the `my-feature` branch.
git show my-feature~
git show my-feature~~
git show my-feature~~~
```

### I want to list the files that were changed in a given commit.
​
Just as with `git diff`, you can limit the output of the `git show` command using the `--stat` modifier. This will list the files that were changed in the given commit:
​
```sh
# Outputs the list of files changed in the commit with the given hash.
git show 19e771 --stat
```
​
