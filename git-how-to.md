GIT
===

### Init Git Project

[How to Write a Git Commit Message](http://chris.beams.io/posts/git-commit/)

```bash
git init
git config --global user.name "jkmssoft"
git config --global user.email "jkmssoft@users.noreply.github.com"

git add . # or git add file1 folder1
# undo git add before commit:
git reset file1
# or
git reset HEAD --
# or
git reset HEAD file1
git commit -m "first commit"

git remote add origin git@github.com:jkmssoft/yii2-counter.git

git push -u origin master
git push -u origin develop
```

### Generate SSH-Keys

See [generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent]
(https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).

```bash
ssh-keygen -t rsa -b 4096 -C "jkmssoft@users.noreply.github.com"
Find key in /home/you/.ssh/id_rsa.pub
```
Copy it to github: [ssh-keys](https://github.com/settings/keys)

### Branching

See [a-successful-git-branching-model](http://nvie.com/posts/a-successful-git-branching-model/).

Create a new Branch named newFeature from develop:
```bash
git checkout -b newFeature develop
...make some changes in files...
git add modifiedFile.xy
git commit
```

Merge changes from newFeature into develop branch:
```bash
git checkout develop
git merge --no-ff newFeature
git push origin develop
```

Delete branch:
```bash
git branch -d BRANCHTODELETE
git push origin --delete BRANCHTODELETE
```

### Create a release

See [Semantic Versioning](http://semver.org/) for version numbers

[Git-Basics-Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

```bash
git checkout master
git tag -a v0.1.1 -m "new release"
git push origin v0.1.1
git push origin --tags
```

### Update local repo

[Syncing](https://www.atlassian.com/git/tutorials/syncing/)

```bash
git fetch origin
git checkout master
git log origin/master
git merge origin/master
```

With the following command the local branch BRANCHNAME will be updated from origin (corresponding remote branch):
```bash
git pull origin BRANCHNAME
```

### Forked repo

Fork a repository on github. Then you need to add the "original" repository url to fetch updates.
```bash
git clone git@github.com:jkmssoft/yii2-user.git
git remote add upstream git@github.com:dektrium/yii2-user.git
git fetch upstream
```

Get/set remote url
```bash
git config --get remote.origin.url
git config --get remote.upstream.url
git remote -v
git remote set-url origin https://github.com/user/repo2.git
```

#### Update forked repo

```bash
git fetch upstream
git checkout master # if not already in branch master
git rebase upstream/master
```

### Update own branch

First: Update your forket repo

```bash
git checkout <THEBRANCHTOUPDATE>
git rebase master
```

### Merge commits (Rebase)

```bash
# The last two commits:
git reset --soft "HEAD^"
git commit --amend
# or
git rebase -i HEAD~1
# or get base of current branch and merge (all) commits
git merge-base MyBranch master
7dbc...
git rebase -i 7dbc...
# replace pick with s (squash), except the first one!
# attention: then push is only possible with -f! 
```
