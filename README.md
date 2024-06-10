# :pencil: Git Commands Summary

#### :notebook: _TODO_
1. merge, rebase
2. merge/pull/rebase conflicts
3. cherrypick
4. detach head
5. remote/upstream
6. pull request
7. pull request conflicts
8. interactive staging
9. before switching to another branch, how to save your work
10. git branch/merge diff seq
11. fast forward
12. force push, when to use
13. Reversing changes/commits/modify, amend
14. Squash/combine commits

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
1. Rebase b1 onto b2: apply b1 commits on top of b2 -> resulting in linear history of commits
:star:  2. Rebase b1 onto b2, now b2 has the work in b1 and b2
```bash
# checkout the branch that is the action branch
$ git checkout b1 # action branch
$ git rebase b2 # base branch
# now, b2 will have additional commits from b1
```
:star:  3. Rebase b2 onto b1, now b1 has the work in b1 and b2
```bash
$ git checkout b2
$ git rebase b1
```

#### :notebook: _Rebase Conflicts_

#### :notebook: _Cherry Pick_
1. Cherry-pick commits from b1 to b2: copy some commits from b1 and apply to b2
```
# checkout the base branch
git checkout b2
gt cherry-pick C2 C4 # apply C2, C4, from b1 (action branch) to b2
# now, c2', c4' will pop upon b1 in that order
```

#### :notebook: _Interactive Staging_
1. Similar to cherry-pick: choose which commands from action branch to copy and apply to base branch
2. Change order, choose/drop
3. Modify, reorder, and drop last x commits (including HEAD)
```bash
$ git rebase -i HEAD~x
# changes with modify, reorder, drop will be shown in the new history
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

