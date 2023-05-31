# Git

* [I want to show the status of the current branch.](#status)

* [I want to create a new branch that is based on the current branch.](#i-want-to-create-a-new-branch-that-is-based-on-the-current-branch)

* [I want to checkout the previous branch that I was on.](#i-want-to-checkout-the-previous-branch-that-i-was-on)

* [I want to list the files that have been modified in the current working tree.](#i-want-to-list-the-files-that-have-been-modified-in-the-current-working-tree)

* [I want to view the changes that were made in a given commit.](#i-want-to-view-the-changes-that-were-made-in-a-given-commit)

* [I want to list the files that were changed in a given commit.](#i-want-to-list-the-files-that-were-changed-in-a-given-commit)

* [I want to view the changes that were made across multiple commits.](#i-want-to-view-the-changes-that-were-made-across-multiple-commits)

* [I want to view the changes that were made in a given file.](#i-want-to-view-the-changes-that-were-made-in-a-given-file)

* [I want to view the contents of a file in a given commit.](#i-want-to-view-the-contents-of-a-file-in-a-given-commit)

* [I want to open the contents of a file in a given commit in my editor.](#i-want-to-open-the-contents-of-a-file-in-a-given-commit-in-my-editor)

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

### I want to view the changes that were made across multiple commits.
​
While the `show` command can show you changes in a given commit, you can use the `diff` command to show changes across multiple commits:
​
```sh
git checkout master
​
# Outputs the changes between `head~` and `head` of the current branch. If
# only one commit is provided, other commit is assumed to be `head`.
git diff head~
​
# Outputs the changes between the first commit and the second commit.
git diff head~~~..head~~
```
​
And, since branch names are really just aliases for commits, you can use a branch name in order to show the changes between one branch and your branch:
​
```sh
git checkout my-feature
​
# At this point, the following are equivalent and output the changes between
# the `head` commit of the `master` branch and the `head` commit of the
# `my-feature` branch.
git diff master
git diff master..head
git diff master..my-feature
```

### I want to view the changes that were made in a given file.
​
By default, the `show` command shows all of the changes in a given commit. You can limit the scope of the output by using the `--` modifier and identifying a filepath:
​
```sh
# Outputs the changes made to the `README.md` file in the `head` commit of the
# `my-feature` branch.
git show my-feature -- README.md
​
# Outputs the changes made to the `README.md` file in the `19e771` commit.
git show 19e771 -- README.md
```

### I want to view the contents of a file in a given commit.
​
By default, the `show` command shows you the changes made to a file in a given commit. However, if you want to view the entire contents of a file as defined at that time of a given commit, regardless of the changes made in that particular commit, you can use the `:` modifier to identify a filepath:
​
```sh
# Outputs the contents of the `README.md` file as defined in the `head` commit
# of the `my-feature` branch.
git show my-feature:README.md
​
# Outputs the contents of the `README.md` file as defined in the `19e771`
# commit.
git show 19e771:README.md
```

### I want to open the contents of a file in a given commit in my editor.
​
Since you're working on the command-line, the output of any git-command can be piped into another command. As such, you can use the `show` command to open a previous commit's file-content in your editor or viewer of choice:
​
```sh
# Opens the `README.md` file from the `head` commit of the `my-feature` branch
# in the Sublime Text editor.
git show my-feature:README.md | subl
​
# Opens the `README.md` file from the `19e771` commit in the `less` viewer.
git show 19e771:README.md | less
```
​
​
