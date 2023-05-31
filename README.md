# Git

* [I want to show the status of the current branch.](#status)

### status

The `status` command shows differences between the working tree, the index, and `head` commit.
​
```sh
git status
```

* [I want to create a new branch that is based on the current branch.](#i-want-to-create-a-new-branch-that-is-based-on-the-current-branch)

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
