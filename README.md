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

* [I want to copy a file from a given commit into my current working tree.](#i-want-to-copy-a-file-from-a-given-commit-into-my-current-working-tree)

* [I want to copy the last commit from another branch into my branch.](#i-want-to-copy-the-last-commit-from-another-branch-into-my-branch)

* [I want to copy an earlier commit from the current branch to the `head`.](#i-want-to-copy-an-earlier-commit-from-the-current-branch-to-the-head)

* [I want to update the files in the current commit.](#i-want-to-update-the-files-in-the-current-commit)

* [I want to edit the current commit message.](#i-want-to-edit-the-current-commit-message)

* [I want to copy `master` into my feature branch.](#i-want-to-copy-master-into-my-feature-branch)

* [I want to revert the merge of my feature branch into `master`.](#i-want-to-revert-the-merge-of-my-feature-branch-into-master)

* [I want to extract changes that I accidentally made to `master`.](#i-want-to-extract-changes-that-i-accidentally-made-to-master)

* [I want to undo the changes that I've made to my branch.](#i-want-to-undo-the-changes-that-ive-made-to-my-branch)

* [I want to configure my username and email.](#i-want-to-configure-my-username-and-email)

* [I want to create new git branch.](#i-want-to-create-new-git-branch)

* [I want to clone an existing repository.](#i-want-to-clone-an-existing-repository)

* [I want to link an existing local repository to a remote repository.](#i-want-to-link-an-existing-local-repository-to-a-remote-repository)


* [I want to add local project on github repository.](#i-want-to-add-local-project-on-github-repository)


## status

The `status` command shows differences between the working tree, the index, and `head` commit.
​
```sh
git status
```
<hr>


## I want to create a new branch that is based on the current branch.
​
In general, you want to implement new features in short-lived "feature branches" so that changes can be isolated. You can use the `checkout` command to create a new branch based on the current branch:
​
```sh
git checkout master
​
# Creates a new branch, `my-feature`, based on `master`.
git checkout -b my-feature
```
<hr>

## I want to checkout the previous branch that I was on.
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
<hr>

## I want to list the files that have been modified in the current working tree.
​
By default, when you call `git diff`, you see all of the content that has been modified in the current working tree (and not yet staged). However, you can use the `--stat` modifier to simply list the files that have been modified:
​
```sh
git diff --stat
```
<hr>

## I want to view the changes that were made in a given commit.
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
<hr>

## I want to list the files that were changed in a given commit.
​
Just as with `git diff`, you can limit the output of the `git show` command using the `--stat` modifier. This will list the files that were changed in the given commit:
​
```sh
# Outputs the list of files changed in the commit with the given hash.
git show 19e771 --stat
```
<hr>

## I want to view the changes that were made across multiple commits.
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
<hr>

## I want to view the changes that were made in a given file.
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
<hr>

## I want to view the contents of a file in a given commit.
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
<hr>

## I want to open the contents of a file in a given commit in my editor.
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
​<hr>
​
## I want to copy a file from a given commit into my current working tree.
​
Normally, the `checkout` command will update the entire working tree to point to a given commit. However, you can use the `--` modifier to copy (or checkout) a single file from the given commit into your working tree:
​
```sh
git checkout my-feature
​
# While staying on the `my-feature` branch, copy the `README.md` file from
# the `master` branch into the current working tree. This will overwrite the
# current version of `README.md` in your working tree.
git checkout master -- README.md
```
​<hr>

## I want to copy the last commit from another branch into my branch.
​
When you don't want to merge a branch into your current working tree, you can use the `cherry-pick` command to copy specific commit-changes into your working tree. Doing so creates a new commit on top of the current branch:
​
```sh
git checkout master
​
# Copy the `head` commit-changes of the `my-feature` branch onto the `master`
# branch. This will create a new `head` commit on `master`.
git cherry-pick my-feature
```
<hr>

## I want to copy an earlier commit from the current branch to the `head`.
​
Sometimes, after you understand why reverted code was breaking, you want to bring the reverted code back into play and then fix it. You _could_ use the `revert` command in order to "revert the revert"; but, such terminology is unattractive. As such, you can `cherry-pick` the reverted commit to bring it back into the `head` where you can then fix it and commit it:
​
```sh
git checkout master
​
# Assuming that `head~~~` and `19e771` are the same commit, the following are
# equivalent and will copy the changes in `19e771` to the `head` of the 
# current branch (as a new commit).
git cherry-pick head~~~
git cherry-pick 19e771
```
<hr>

## I want to update the files in the current commit.

If you want to make changes to a commit after you've already committed the changes in your current working tree, you can use the `--amend` modifier. This will add any staged changes to the existing commit.

```sh
git commit -m "Woot, finally finished!"

# Oops, you forgot a change. Edit the file and stage it.
# ... changes to the working tree (your file system).
git add oops.txt

# Adds the currently-staged changes (oops.txt) to the current commit, giving
# you a chance to update the commit message.
git commit --amend
```
<hr>

## I want to edit the current commit message.

In addition to adding files to the current commit, the `--amend` modifier can also be used to change the current commit message:

```sh
git add .
git commit -m "This is greet."

# Oh noes! You misspelled "great". You can edit the current commit message:
git commit --amend -m "This is great."
```

Note that if you omit the `-m message` portion of this command, you will be able to edit the commit message in your configured editor.

<hr>

## I want to copy `master` into my feature branch.

At first, you may be tempted to simply `merge` your `master` branch into your feature branch, but doing so will create an unattactive, non-intuitive, Frankensteinian commit tree. Instead, you should `rebase` your feature branch on `master`. This will ensure that your feature commits are cleanly colocated in the commit tree and align more closely with a human mental model:

```sh
git checkout my-feature

# This will unwind the commits specific to the `my-feature` branch, pull in
# the missing `master` commits, and then replay your `my-feature` commits.
git rebase master
```

Once your `my-feature` branch has been rebased on `master`, you could then, if you wanted to, perform a `--ff-only` merge ("fast forward only") of your feature branch back into `master`:

```sh
git checkout my-feature
git rebase master

# Fast-forward merge of `my-feature` changes into `master`, which means there
# is no creation of a "merge commit" - your `my-features` changes are simply
# added to the top of `master`.
git checkout master
git merge --ff-only my-feature
```

That said, when you're working on a team where everyone uses a different git workflow, you will definitely _want_ a "merge commit". This way, multi-commit merges can be easily reverted. To force a "merge commit", you can use the `--no-ff` modifier ("no fast forward"):

```sh
# Get the `my-feature` branch ready for merge.
git checkout my-feature
git rebase master

# Merge the `my-feature` branch into `master` creating a merge-commit.
git checkout master
git merge --no-ff my-feature
```

Now, if the merge needs to be reverted, you can simply revert the "merge commit" and all commits associated with the merge will be reverted.

<hr>

## I want to revert the merge of my feature branch into `master`.

If you performed a `--ff-only` merge of your feature branch into `master`, there's no "easy" solution. You either have to reset the branch to an earlier commit (rewriting history); or, you have to revert the individual commits in the merge.

If, however, you performed a `--no-ff` merge ("no fast forward") that created a "merge commit", all you have to do is revert the merge commit:

```sh
git checkout master

# Merge the feature branch in, creating a "merge commit".
git merge --no-ff my-feature

# On noes! You didn't mean to merge that in. Assuming that the "merge commit"
# is now the `head` of `master`, you can revert back to the commit's fist
# parent, the `master` branch: -m 1. And, since `head` and `master` are the
# same commit, the following are equivalent:
git revert -m 1 head
git revert -m 1 master
```
<hr>

## I want to extract changes that I accidentally made to `master`.

Sometimes, after you've finished working on your feature branch, you execute `git checkout master`, only find that you've been accidentally working on `master` the whole time (error: "Already on 'master'"). To fix this, you can `checkout` a new branch and `reset` your `master` branch:

```sh
git checkout master
# > error: Already on 'master'

# While on the `master` branch, create the `my-feature` branch as a copy of
# the `master` branch. This way, your `my-feature` branch will contain all of # your recent changes.
git checkout -b my-feature

# Now that your changes are safely isolated, get back into your `master`
# branch and `reset` it with the `--hard` modifier so that your local index
# and file system will match the remote copy.
git checkout master
git reset --hard origin/master
```
<hr>

## I want to undo the changes that I've made to my branch.

If you've edited some files and then change your mind about keeping those edits, you can reset the branch using the `--hard` modifier. This will update the working tree - your file structure - to match the structure of the last commit on the branch (`head`).

**Caution**: You will lose data when using the `--hard` option.

```sh
git checkout my-feature
# ... changes to the working tree (your file system).
git add .

# Remove the file from staging AND remove the changes from the file system.
git reset --hard
```

If you call `git reset` without the `--hard` option, it will reset the staging to match the `head` of the branch, but it will leave your file system in place. As such, you will be left with "unstaged changes" that can be modified and re-committed.

<hr>

## I want to configure my username and email.

If you want to configure the username and email of you git. Then simply do:

```sh
git config --global user.name "FIRST_NAME LAST_NAME"
git config --global user.email "MY_NAME@example.com"
```
<hr>

## I want to create new git branch.

If you want to create a new git branch without switching. You can use :

```sh
git branch <branch_name>
```

But if you want to create a new branch and switch to the created branch. You can use:
```sh
git checkout -b <branch_name>
```
<hr>

## I want to clone an existing repository.

`git clone` is primarily used to point to an existing repo and make a clone or copy of that repo at in a new directory, at another location.

```sh
git clone ssh://john@example.com/path/to/my-project.git 
```
<hr>

## I want to link an existing local repository to a remote repository.

When you clone a repository, Git automatically sets up a remote named "origin" that points to the repository you cloned from. However, if you create a new local repository or want to link an existing local repository to a remote repository, you need to use the `git remote add origin command`.

```sh
git remote add origin https://github.com/username/repository.git
```

<hr>

## I want to add local project on github repository.


To add your local project to a GitHub repository, you can follow these general steps:

1- Initialize Git in your local project:

Open a terminal or command prompt.
Navigate to the root directory of your local project.
Run the following command to initialize a Git repository:

```sh
git init
```

2- Add your project files to the Git repository:

Use the following command to add all files in the current directory and its subdirectories to the repository:
```sh
git add .
```

3- Commit your changes:

After adding the files, create a commit to save the current state of your project using the following command:
```sh
git commit -m "initial commit"
```

4- Link your local repository to the GitHub repository:

On the GitHub repository page, copy the remote repository URL. You can find it by clicking on the "Code" button and selecting the appropriate URL (HTTPS or SSH).
In your terminal or command prompt, run the following command to add the remote repository:

```sh
git remote add origin <remote_repository_URL>
```

5- Push your local repository to GitHub:

Use the following command to push your local commits to the remote repository on GitHub:
```sh
git push origin <branch_name>'i.e main'
```

<hr>