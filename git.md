## git push origin master
- master can be changed to other dev

---

## git add .
- add all files

---
# reset
## git reset --soft HEAD^
- reset commit
- HEAD^的意思是上一个版本,也可以写成HEAD~1,如果你进行了2次commit,想都撤回,可以使用HEAD~2

## git reset --hard <SOME-COMMIT>
- <SOME-COMMIT> can be commit id or HEAD or sth. else
- things that happens
    + make your current branch (typicallly master) back to point at <SOME-COMMIT>
    + make the files in your working tree the same as the version committed in <SOME-COMMIT>
    + make the files in the index the same as the version committed in <SOME-COMMIT>
    + all uncommitted changes will be throwed away
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  - this is a potentially dangerous command, since all the uncommitted changes will be discarded.
- you should always check that the ouput of `git status` is clean before using it.

## reset the `git init`
- find . -name ".git" | xargs rm -rf

---
# commit
## change the commit message
- `git commit --amend`
- `git commit --amend -m "some message"`

## 取消git初始化
`rm -rf .git`

# 初始化

### …or create a new repository on the command line

```
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:sucongCJS/test.git
git push -u origin main
                
```

### …or push an existing repository from the command line

```
git remote add origin git@github.com:sucongCJS/test.git
git branch -M main
git push -u origin main
```