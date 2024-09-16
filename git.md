# Cherry-pick multiple commits
To cherry-pick all the commits from A to B, __where A is older than B__, run:
```
git cherry-pick A^..B
```
If you want to ignore A itself, run:
```
git cherry-pick A..B
```
