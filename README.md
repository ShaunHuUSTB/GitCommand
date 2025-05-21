# GitCommand

## fork仓同步upstream的新分支
1. fetch上游仓库
```
git fetch upstream
```
2. 创建新分支并关联upstrean
```
git checkout -b new_branch upstream/new_branch
```
3. 推送新分支到fork仓
```
git push fork new_branch
```
4. 关联新分支到fork
 ```
git branch --set-upstream-to=fork/new_branch new_branch
 ```
