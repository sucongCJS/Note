## kill zombie
```shell
ps -A -o stat, ppid, pid cmd | egrep '^[Zz]';
kill -9 pid
# or do via script
ps -A -o stat,ppid,pid,cmd | grep -e '^[Zz]' | awk '{print $2}' | xargs kill -9

```
## top
```shell
# see the specific pid
top -d 1 -p 29907
```

- [more kill skills](https://www.jianshu.com/p/5ab557f8a6bf)
