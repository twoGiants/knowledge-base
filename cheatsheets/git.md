# Git

Resource: [Pro Git 2nd Edition](https://git-scm.com/book/en/v2).

## Gitignore

Exclude everything except directory `foo/bar`:

```sh
# .gitignore
/*
!/foo
/foo/*
!/foo/bar
```

Now an example from the Obsidian vault. Exclude everything except plans (`2. Areas/Time Management/Plans`) and archived plans from 2025 (`4. Archive/Time Management/Weekly/2025`):

```sh
# .gitignore
# exclude everything
/*

# except gitignore
!.gitignore

# except plans
!2. Areas
2. Areas/*
!2. Areas/Time Management
2. Areas/Time Management/*
!2. Areas/Time Management/Plans

# except plan archive
!4. Archive
4. Archive/*
!4. Archive/Time Management
4. Archive/Time Management/*
!4. Archive/Time Management/Weekly
4. Archive/Time Management/Weekly/*
!4. Archive/Time Management/Weekly/2025
```

## Workflows

### Amend old Commit

Add your staged changes to a commit which is `n` commits in the past:

```sh
# stash your staged files
git stash

# interactively rebase and go to the commit in the past you want to add the change
git rebase -i HEAD^4

# in interactive rebase change "pick" to "edit" on your target commit
# then pop or apply the stash
git stash pop

# resolve conflicts if any
```

### Checkout Fork

Checkout PR branch from a fork:

```sh
# tektoncd/pipeline PR 8677 example
git fetch upstream pull/8677/head:aThorp96-git-resolver-memory-leak

git checkout aThorp96-git-resolver-memory-leak
```

### Change Commit Date

## Change Last Git Commit Date to Yesterday

1. Set yesterday’s date:

   ```bash
   export GIT_COMMITTER_DATE="$(date -d 'yesterday' '+%Y-%m-%d %H:%M:%S')"
   export GIT_AUTHOR_DATE="$GIT_COMMITTER_DATE"
   ```

2. Amend the latest commit:

   ```bash
   git commit --amend --no-edit --date "$GIT_AUTHOR_DATE"
   ```

3. Force-push:

   ```bash
   git push --force
   ```

4. Reset:

   ```bash
   unset GIT_COMMITTER_DATE
   unset GIT_AUTHOR_DATE
   ```

## Change to Day Before Yesterday

1. Set day before yesterday’s date:

   ```bash
   export GIT_COMMITTER_DATE="$(date -d '2 days ago' '+%Y-%m-%d %H:%M:%S')"
   export GIT_AUTHOR_DATE="$GIT_COMMITTER_DATE"
   ```

For the other steps see above.

## Commands

Restore to commit before merge:

```sh
# one commit before
git reset --merge HEAD~1

# to commit with sha
git reset --merge <commit-sha>
```

### Configuration

Store username and password:

```sh
git config --global credential.helper store
```

Cache username and password for a session:

```sh
git config --global credential.helper cache
```

Show configurations:

```sh
git config —-list
git config user.name
git config —-show-origin user.name
```

Intro

```sh
git status -s

# diff of staged to last commit
git diff —-staged

# öffnet konfigurierten Editor
git commit

# zeig nur die Änderungen im Log von den letzten 2 commits
git log -p -2

git log —-pretty=oneline|short|full|fuller

# find the last commit that added or removed a reference to a specific function (a string)
git log -S funcName

# zeig die History von einem File oder Files in einem Ordner
git log —- path/to/file

# show branch pointers with log
git log —-decorate

# !!! merge commits ausblenden
git log —-oneline --no-merges

# complex example: commits modifying test files by Junio Hamano in October 2008 which are not merge commits
git log —-pretty=„%h - %s“ —-author=„Junio Hamano“ —-since=„2008-10-01“ —-before=„2008-11-01“ —-no-merges —- /tests

# show history of a specific branch
git log testing

# show history of all branches
git log —-all

# showing where your branch pointers are and how your history has diverg
git log —-decorate —-oneline —-all —-graph
```

Git log pretty format options p.43

Unstage file

```sh
git reset HEAD <file>

# OR the new command
git restore —-staged <file>
```

Unmodify modified file

```sh
git checkout —- <file>

# OR
git restore <file>
```

If you use other remotes name them by the owner names

```sh
git remote add tg https://github.com/twogiants/example-repo.git
```

If you want to rebase when pulling:

```sh
git config --global pull.rebase "true"
```

Tags p56

* annotated recommended
* lightweight tags are not shown in the log
* push single or all of them

```sh
git push origin v1.5
git push origin —-tags
git push origin <branch> —-follow-tags
```

Deleting Tags

```sh
git tag -d v1.5
git push origin —-delete v1.5
# OR
git push origin :ref/tags/v1.5
```

You can use switch instead of checkout:

```sh
# switch
git switch testing-branch

# create and switch
git switch -c new-branch

# switch to prev branch
git switch -
```

Branches and Merges

* p73, Fast forward merge: when you try to merge one commit with a commit that can be reached by following the first commit’s history, Git simplifies things by moving the pointer forward because there is no divergent work to merge together
* If the history has diverged git uses a three-way-merge: last commits of the two branches and a common ancestor. It creates a merge commit which points to the two last commits of the branches
* If you have conflicts, resolve them, remove the markers and use git add to stage, staged files are seen as resolved. When you commit you get a standard commit message, chnage it if the commit was complex and needed some special changes

The branch cmd

```sh
# show branches
git branch

# show with last commit
git branch -v

# show merged branches into the current branch
git branch —-merged

# show not merged
git branch —-no-merged

# show not merged in master when you are in testing
git branch —-no-merged master
```

Rename and update on the remote p81

```sh
git branch —-move bad-name corrected-name
git push —-set-upstream origin corrected-name
git branch —-all
git push origin —-delete bad-name
git branch —-all
```

Working with remotes p85

* remote branches are pointers you can’t move -> origin/master does not move
* If you want its state in your branch you need to merge( or rebase) git merge origin/master (git rebase origin/master) while being in master
* If you want a local branch which is based on some remote: git checkout -b serverfix origin/serverfix
* If you are on a branch and want it to track some remote branch: git checkout —-track origin/somebranch
* When a local branch tracks a remote, pushes pulls go there
* When you clone a repo git sets, origin as a remote, master as the first branch which tracks origin/master
* To setup a local branch with a different name than the remote branch: git checkout -b sf origin/serverfix
* If you already have a local branch and you want it to track a remote branch: git branch -u origin/serverfix
* See what tracking branches you have set up:

```sh
git fetch —-all
git branch -vv
    iss53    7e424c3 [origin/iss53: ahead 2] Add forgotten brackets
    master    1ae2a45 [origin/master] Deploy index fix
  * serverfix f8674d9 [teamone/server-fix-good: ahead 3, behind 1] This should do it
    testing  5ea463a Try something new
```

* delete a remote branch: git push origin ——delete serverfix

Pulling

* prefer git fetch and git merge over git pull

Rebase p95

* Take all the changes you did in one branch and replay them on another branch and then fast forward merge

```sh
git checkout experiment
git rebase master
git checkout master
git merge experiment
```

* No difference to merge but a cleaner history
* If you examine the log of a rebased branch, it looks like a linear history: it appears that all the work happened in series, even when it originally happened in parallel.
* best of both worlds: rebase local changes before pushing to clean up your work, but never rebase anything that you’ve pushed somewhere.

Distributed Git

* all the different workflows and when to use them <https://martinfowler.com/articles/branching-patterns.htm>

Git commits p131

* checkout git history: git log —no-merges
* documentation/submittingpatches in git project
* Check whitespace

```sh
git diff —check
```

Git Workflows p139

* Get remote and see only the new changes to you local branch

```sh
git fetch origin
git log featureA..origin/featureA
```

* set your upstream to a remote branch with a different name

```sh
git push -u origin featureB:featureBee
```

* if your contributor sends you two patches and you create a branch called contrib and applied those patches there, you can run this

```sh
git log contrib —-not master
```

* shows you only the work your current topic branch has introduced since its common ancestor with master

```sh
git diff contrib...master
```

Rerere p162

* use rerere when maintaining a long lived branch which will memorize conflict resolutions and apply them on future conflicts

```sh
git config --global rerere.enabled true
```

Generate a build number p163

* latest tag will used and number of commits since then with the sha of the last commit and g as prefix

```sh
git describe master
v1.6.2-rc1-20-g8c5b85c
```

Release p164

* creates the latest snapshot of your code in an archive

```sh
git archive master —-prefix=“project/“ | gzip > $(git describe master).tar.gz
ls *.tar.gz
v1.6.2-rc1-20-g8c5b85c.tar.gz
```

Shortlog/Changelog p164

* everything that was added since last release v1.0.1

```sh
git shortlog —-no-merges master —-not v1.0.1
```

Git Tools

* The sha-1 value of at least 4 characters can be used instead of the full sha

```sh
git show 0f9i
```

* show the short sha on each commit

```sh
git log —-abbrev-commit —-pretty=oneline
```

* get sha of branch tip

```sh
git rev-parse topic1
ca82a6dff817ec66f44342007202690a93763949
```

* reflog is a log of where the head and branches were in the last months

```sh
git reflog
```

* show ancestor or parent
* show parent of parent etc

```sh
git show HEAD^
git show HEAD~3
```

* what is in your experiment branch that hasn’t yet been merged into your master

```sh
git log master..experiment
```

* what are rhe commits you are going to push

```sh
git log origin/featureA..HEAD
# OR
git log origin/featureA..
```

* see all commits that are reachable from refA or refB but not from refC

```sh
git log refA refB —-not refC
```

* all the commits that are reachable by either of two references but not by both of them

```sh
git log experiment...master —-left-right
```

* interactive staging

```sh
git add -i
```

* staging patches

```sh
git add -p
```

Git Stash

* stash and restore the staged files

```sh
git stash apply —-index
```

* stash but keep stuff in the index in case you want to apply it somewhere else

```sh
git stash —-keep-index
```

* stash with untracked files, otherwise only the staged ones will be stahsed

```sh
git stash -u # —-include-untracked
```

* stash with untracked files and message

```sh
git stash -um "your message"
```

* and to add ignored files also add

```sh
git stash -a # —-all
```

* stash interactively and decide what to stash and what not

```sh
git stash —-patch
```

* create a branch from stash -> useful when you continued working after stashing and don’t want to apply in the current branch

```sh
git stash branch <new-branch-name>
```

Create patch from 1 commit and apply somewhere

```sh
# create
git format-patch -1 e314b68 

# apply
git am *.patch
```
