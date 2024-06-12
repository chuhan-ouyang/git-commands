# :pencil: Git Commands Summary

#### :notebook: _TODO_
1. merge conflict
2. pull conflict
3. rebase conflict
5. cherrypick test again
6. detach head and force head again
7. remote/upstream
8. pull request
9. pull request conflicts
10. interactive staging, more usages
11. before switching to another branch, how to save your work
13. fast forward
14. force push, when to use
15. Reversing changes/commits/modify, amend practice
16. Squash/combine commits

#### :notebook: _Creating Branches_
1. git branch is for creating new branch, git checkout is to switched to a created branch
2. Create a new local branch called newImage
```bash
$ git branch newImage
```
3. Checkout a created branch (switch), either a local created branch or remote branch
```bash
$ git checkout newImage
```
4. Create a new branch and switch to it at the same time
```bash
$ git checkout -b newImage
```

#### :notebook: _Merging Branches_
1. Merge b1 into b2: create a new commit in b2 that has parents in both b1 and b2
:star:  2. Merge b1 into b2, now b2 has work in b1 and b2
```bash
# checkout the branch that is being merged into
$ git checkout b2 # into branch
$ git merge b1 # action branch
```
:star:  3. Merge b2 into b1, now b1 has work in b1 and b2
```bash
$ git checkout b1
$ git merge b2
```

#### :notebook: _Merging Branches Conflicts_

#### :notebook: _Pull Conflicts_

#### :notebook: _Rebase_
:star: 1. Rebase topic branch onto base branch: move topic branch's head along by applying the topic branch's commits on top of (after) base branch commits in a linear history
Note: later, can rebase base branch on top of topic branch so base branch can move along to the same "combined" head as the topic branch
```bash
$ git rebase [basebranch] [topicbranch]
# now topic branch's commits will be applied on top of base, and topic branch's head will be updated
```

#### :notebook: _Rebase Conflicts_

#### :notebook: _Cherry Pick_
1. Cherry-pick commits from b1 to head: copy some commits from b1 and apply to current head
```
# checkout the base branch
git checkout b2 # target is b2's head
gt cherry-pick C2 C4 # apply C2, C4, from b1 (action branch) to b2's head
# now, c2', c4' will pop upon after b2's previous head, in that order
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

#### :notebook: _Upstream_

#### :notebook: _Pull Request_

#### :notebook: _Pull Request Conflicts_

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

