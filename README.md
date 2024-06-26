# :pencil: Git Commands Summary

#### :notebook: _TODO_
3. merge conflict
4. rebase conflict
5. 10. pull request conflicts
6. cherrypick test again
7. detach head and force head again
8. reset hard
9. remote(orgin)/upstream
12. before switching to another branch, how to save your work
13. fast forward
14. force push, when to use
17. git stash, pop, apply
18. reset hard

#### :notebook: _Creating Branches_
1. git branch is for creating new branch, git checkout is to switched to a created branch
2. Create a new local branch called newImage
```bash
$ git branch newImage
```
3. Checkout a created branch (switch), either a local created branch or remote branch. If newImage is remote, then you will have a local newImage that is set to track remote newImage branch.
```bash
$ git checkout newImage
```
4. Create a new branch and switch to it at the same time
```bash
$ git checkout -b newImage
```
5. Create a new branch, switch to it, and track some remote branch
```bash
$ git checkout -b totallyNotMain o/main
```

#### :notebook: _Merging Branches_
1. Merge b1 into b2: create a new commit in b2 that has parents in both b1 and b2
:star:  2. Merge b1 into b2, now b2 has work in b1 and b2
```bash
# checkout the branch that is being merged into
$ git checkout b2 # base branch
$ git merge b1 # topic branch
```
:star:  3. Merge b2 into b1, now b1 has work in b1 and b2
```bash
$ git checkout b1
$ git merge b2
```

#### :notebook: _Merging Branches Conflicts_

#### :notebook: _Pull Conflicts_
* After you have a local commit, and then try pulling in new commits from remote, remote conflicts with local commit
* Occurs when pulling after a local commit, which happens when pushing a local commit (notified with need to pull first)
* The local commit to push needs to be based off of the most recent remote commit

#### :notebook: _Resolving Pull Conflicts Using Rebasing_
```bash
$ git checkout main
$ git fetch # origin/main will now have remote commits
$ git rebase origin/main # rebase main onto origin/main
# now, main commits will be applied on top of origin/main
# main commits are now based off the most recent remote commits
$ git push
```
* Equivalently: Think applying main commits on top of all remote commits
```bash
$ git checkout main
$ git pull --rebase
$ git push
```

#### :notebook: _Resolving Pull Conflicts Using Merging_
```bash
$ git checkout main
$ git fetch # origin/main will now have remote commits
$ git merge origin/main # create new commit in main to incorporate both main commits and remote new commits
$ git push # latest commit is based on the most recent remote commits
```
* Equivalently: Think creating new commit with both main and remote commits
```bash
$ git checkout main
$ git pull
$ git push
```

#### :notebook: _Rebase_
:star: 1. Rebase topic branch onto base branch: move topic branch's head along by applying the topic branch's commits on top of (after) base branch commits in a linear history
Note: later, can rebase base branch on top of topic branch so base branch can move along to the same "combined" head as the topic branch
```bash
$ git rebase [basebranch] [topicbranch]
# now topic branch's commits will be applied on top of base, and topic branch's head will be updated
```
![image](https://github.com/chuhan-ouyang/git-commands/assets/112202738/e646a623-639b-42e8-920c-7e16926325ff)


#### :notebook: _Rebase Conflicts_

#### :notebook: _Cherry Pick_
1. Cherry-pick commits from b1 to head: copy some commits from b1 and apply to current head
```
# checkout the base branch
git checkout b2 # target is b2's head
gt cherry-pick C2 C4 # apply C2, C4, from b1 (action branch) to b2's head
# now, c2', c4' will pop upon after b2's previous head, in that order
```


#### :notebook: _Modifying the Latest Commit_
```bash
# make changes to files, like git add new.cpp, git rm old.cpp
git commit --amend # modify commit message (locally)
git push --force
```

#### :notebook: _Modifying Multiple Past Commits_
* Use interactive rebase to edit each command, preserve original order and structure
```bash
git rebase -i HEAD~n # modify last n commit
# change pick to edit for the commit to edit
# one by one ...
git add .... # new changes
git commit --amend # solidified amend
git rebase --continue
git push --force 
```
#### :notebook: _Reordring Multiple Past Commits_
* Use interactive rebase to reorder commits
* In interactive staging, commits will be listed/applied from oldest - latest
```bash
git rebase -i HEAD~n # modify last n commit
# use vim to reorder, from old to latest
```
#### :notebook: _Squashing Multiple Past Commits_
* Use interactive rebase to squash commit
* pick c1, squash c2 will squash c2 into the older commit c1 -> appear as 1 commit
```bash
git rebase -i HEAD~n # modify last n commit
# use vim to change pick to squash if you want to squash this into prev
```
#### :notebook: _Splitting Past Commits_
```bash
git rebase -i HEAD~n
# change pick to edit for the commit to split
git reset HEAD~1 # unstage all files
git add c1
git commit -m "c1" # first part of split
git add c2
git commit -m "c2" # second part of split
git rebase --continue # now, will be splitted to c1, c2
```

#### :notebook: _Deleting Past Commits_
```bash
git rebase -i HEAD~n
# change edit to drop for the commit to drop
```

#### :notebook: _Interactive Staging_
1. Similar to cherry-pick: choose which commands from action branch to copy and apply to base branch
2. Change order, choose/drop
3. Modify, reorder, and drop last x commits (including HEAD)
```bash
$ git rebase -i HEAD~x
# changes with modify, reorder, drop will be shown in the new history
```
4. Can be used to just use some, but not all, commits in the history

#### :notebook: _Modifying Commit Early in History Using Rebase & Amend_
1. Case: modify commit the previous commit (C2) in current history (C2, C1)
```bash
# use staging to move previous commit to top
$ git rebase -i HEAD~2

# move order to C1, C2

# amend modify latest commit
$ git commit --amend

# re-order commits back to how they were
$ git rebase -i HEAD~2

#move order to C2, C1
```

#### :notebook: _Modifying Commit Early in History Using Amend & Cherry-Pick_
1. Case: modify c2 commit in b2, and then get c3, c2' onto b1
```bash
git checkout b2
git commit --amend

git checkout b1
git cherry-pick c3
git cherry-pick c2' # modified c2 version
```


#### :notebook: _Detach Head_
:star: 1. HEAD = most recent commit in the working tree, usually points to a branch (each branch pts to its most recent commit)
```bash
$ git log -1 HEAD # show info about head
```
2. Detach head = attaching head to a commit instead of a branch
:star: 3. Move head around: detach head from branch b1 and attach head to commit C1
```bash
git checkout C1 # commit hash
```
4. Move head around: checkout commit right before curr commit of branch b1, also detach head
```bash
git checkout b1^ # head is now at the parent of b1
```
:star: 5. Force reassign branch to another commit
```bash
git branch -f main HEAD~3 # Reassign main to 3 commits before HEAD
```

#### :notebook: _Remote_
:star: remote repo = server copy of repo
:star: each remote as a name. Typically, remote is named origin
:star: after adding a remote repo, there are remote branches, reflecting the state of the branches when we last talked to the servers
* ex. origin(<remote name>)<branch name>

#### :notebook: _Fetch_
:star: fetch data from remote repo, updating remote branches states in local repo
:star: fetch latest commits from remote repo to local remote branches, and update the head of local remote branches to latest commit
```bash
$ git fetch
```
:star: does not update the local non-remote branches

#### :notebook: _Pull_
* Fetch remote branch and merge remote branch into local branch
* Equivalent commands
```bash
git checkout main
git pull 

# same as
git checkout main
git fetch
git merge origin/main
```

#### :notebook: _Push_
* Push new commit to remote and local remote branches
```bash
$ git checkout main
$ git push origin <source>:<destination>
```
* When pushing, the head should be checked out (not detached) on the tip of a remote tracking local branch

#### :notebook: _Pull Request_
* Have a feature branch and set remote to track that
* Send pull request from feature to main (protected branch)

#### :notebook: _Pull Request Conflicts_

#### :notebook: _Upstream_

#### :notebook: _Forks_

#### :notebook: _Git Reset, Revert_
1. Git reset: move local branch reference backward
```bash
git reset HEAD~1 # reset the head of main back by 1
```
2. Git revert: move remote branch reference backward
```bash
git revert HEAD # reset the head of remote branch back by 1
```

#### :notebook: _Interactive Staging_

