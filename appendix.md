<!-- $theme: gaia -->
<!-- $width: 1440-->
<!-- $height: 900 -->

# ![center 150%](images/logo.svg)

---

# Appendix

---

<!-- page_number: true -->---

# Appendix

1. Writing commit messages
2. Git workflow

---

# Writing commit messages

1. Describe the intent not the code.
2. Write imperative.
3. Write in present tense.

---

# Writing commit messages

* One header line, 50 chars.
* Start with a verb.
* Empty line.
* Then multiple paragraphs, 72 chars.

---

# Writing commit messages

```git
Explain the commit in the header with 50 chars max

Body of commit message is a few lines of text, explaining things
in more detail, possibly giving some background about the issue
being fixed, etc etc.

The body of the commit message can be several paragraphs, and
please do proper word-wrap and keep columns shorter than about
72 characters or so. That way "git log" will show things
nicely even when it's indented.

Reported-by: whoever-reported-it
Signed-off-by: Your Name <youremail@yourhost.com>

Fixes #32145
```

---

# Workflow

1. Commit early.
2. Commit often.
3. Commit related changes.
4. Use your tools to make a good commit.

---

# Workflow

```
$ git add --patch
$ git checkout --patch
$ git diff --cached
```

!!! think of a good demo, current project?

---

# Nuggets

!!! examples

```
git checkout -
git diff --word-diff
git diff --name-only --diff-filter=U
git status --short
git log --oneline
```

Config

```
git config --global push.default current # prevent accidental pushes
git config --global commit.verbose true  # see diff on commit
git config --global merge.summary true   # see diff on merge
```
---

# git reset

explain soft vs hard

---

# git status

Initial commit

```
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

---

# git status

Clean

```
$ git status
On branch master
nothing to commit, working tree clean
```

Untracked

```
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        index.html

nothing added to commit but untracked files present (use "git add" to track)
```

---

# git status

Modified

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")

```

---

# Installation

```sh
$ brew install git     # macOS
$ apt-get install git  # Debian/Ubuntu
$ yum install git      # Fedora < 22
$ dnf install git      # Fedora >= 22
```

Configuration

```sh
$ git config --global user.name <name>   # define author for user
$ git config --global user.email <email> # define mail for user
```

---

# Commands

```sh
git init [<directory>]      # create repository
git clone [<repo>]          # clone repo

git add <dir|file>          # stage changes
git commit -m "<message>"   # commit stage with message

git status                  # list (un)staged & untracked files
git log                     # show commit history
git diff                    # show unstaged changes

git checkout                # switch to a branch
git branch                  # create a branch
```

---


---

# Ignoring whitespace

!!! -Xignore-all-space or -Xignore-space-change

```shell
$ git merge -Xignore-space-change whitespace
Auto-merging hello.rb
Merge made by the 'recursive' strategy.
 hello.rb | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

!!! look at bodged whitespace in terminal


---

# Conflict before a Merge

<div style="float: left">

```sh
$ git config --global \
    alias.stsh 'stash --keep-index'
$ git config --global \
    alias.staash 'stash --include-untracked'

git stsh    # only unstaged changes to tracked files
git stash   # any changes to tracked files
git staash  # untracked and tracked files
```

!!! makes this easier

</div>

---

# `git config merge.conflictstyle diff3`

---

I find merge tools rarely help me understand the conflict or the resolution. I'm usually more successful looking at the conflict markers in a text editor and using git log as a supplement.

Here are a few tips:

Tip One

The best thing I have found is to use the "diff3" merge conflict style:

git config merge.conflictstyle diff3

This produces conflict markers like this:

```
<<<<<<<
Changes made on the branch that is being merged into. In most cases,
this is the branch that I have currently checked out (i.e. HEAD).
|||||||
The common ancestor version.
=======
Changes made on the branch that is being merged in. This is often a
feature/topic branch.
>>>>>>>
```

---


# Merge strategies - `-Xours|theirs`

`recursive` options

* pick side in case of conflict
* still merge non conflicting changes

```sh
$ git merge -Xours mundo
Auto-merging hello.rb
Merge made by the 'recursive' strategy.
 hello.rb | 2 +-
 test.sh  | 2 ++
 2 files changed, 3 insertions(+), 1 deletion(-)
 create mode 100644 test.sh
```

!!! `git merge-file --ours` example

---


# Merge strategies - `-s ours|theirs`

different strategy

* picks side
* fake merge
* useful to keep history

!!! good example

```sh
$ git merge -s ours mundo
Merge made by the 'ours' strategy.
$ git diff HEAD HEAD~
$
```
