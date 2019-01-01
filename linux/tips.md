- kill zombie
```shell
ps -A -o stat, ppid, pid cmd | egrep '^[Zz]';
kill -9 pid
# or do via script
ps -A -o stat,ppid,pid,cmd | grep -e '^[Zz]' | awk '{print $2}' | xargs kill -9
```
