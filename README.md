# git-commands

#### TODO
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

#### Creating Branches
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

#### Merging Branches
1. Merge b1 into b2: create a new commit in b2 that has parents in both b1 and b2
2. Merge b1 into b2, now b2 has work in b1 and b2
```bash
# checkout the branch that is being merged into
$ git checkout b2 # into branch
$ git merge b1 # action branch
```
3. Merge b2 into b1, now b1 has work in b1 and b2
```bash
$ git checkout b1
$ git merge b2
```

#### Merging Branches Conflicts

#### Pull Conflicts

#### Rebase
1. Rebase b1 onto b2: apply b1 commits on top of b2 -> resulting in linear history of commits
2. Rebase b1 onto b2, now b2 has the work in b1 and b2
```bash
# checkout the branch that is the action branch
$ git checkout b1 # action branch
$ git rebase b2 # base branch
# now, b2 will have additional commits from b1
```
3. Rebase b2 onto b1, now b1 has the work in b1 and b2
```bash
$ git checkout b2
$ git rebase b1
```

#### Rebase Conflicts

#### Cherry Pick

#### Detach Head

#### Remote

#### Upstream

#### Pull Request 

#### Pull Request Conflicts

#### Interactive Staging

