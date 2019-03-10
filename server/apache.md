# 日常操作
## 修改目录
1. 打开文件目录`/etc/apache2/sites-enabled/000-default`
2. 修改路径
```shell
#
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from this directory, but
# symbolic links and aliases may be used to point to other locations.
#
DocumentRoot "/var/www/html"
```
3. 保存文件, 重启Apache
```shell
jason@ghost: systemctl restart apache
jason@ghost: service httpd restart

or

jason@ghost: sudo /etc/init.d/apache2 restart
```

# 配置
## 配置信息
[Apache Options指令详解](http://www.365mini.com/page/apache-options-directive.htm)
## 配置文件
Linux下 Apache的配置文件是 /etc/apache2/apache2.conf，Apache在启动时会自动读取这个文件的配置信息。而其他的一些配置文件，如 httpd.conf等，则是通过Include指令包含进来。

在apache2.conf里有sites-enabled目录，而在 /etc/apache2下还有一个sites-available目录，其实，这里面才是真正的配置文件，而sites-enabled目录存放的只是一些指向这里的文件的符号链接，你可以用ls /etc/apache2/sites-enabled/来证实一下。

所以，如果apache上配置了多个虚拟主机，每个虚拟主机的配置文件都放在 sites-available下，那么对于虚拟主机的停用、启用就非常方便了：当在sites-enabled下建立一个指向某个虚拟主机配置文件的链 接时，就启用了它；如果要关闭某个虚拟主机的话，只需删除相应的链接即可，根本不用去改配置文件。

## 模块Module
### prefork＆worker
Prefork MPM(Multi-Processing Module) uses multiple child processes with one thread each and each process handles one connection at a time.
Worker MPM uses multiple child processes with many threads each. Each thread handles one connection at a time.

# set up apache **Virtual Hosts**
Apache comes with a default virtual host file called **000-default.conf** that we can use as a jumping off point. We are going to copy it over to create a virtual host file for each of our domains.

[set up apache Virtual Hosts](https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-16-04)

## some ERROR encountered:
- the VPS address is your localhost address(see at `ifconfig`), the modify the `hosts` file

- Error: 'You don't have permission to access / on this server. '
modify your site conf file like [this](https://stackoverflow.com/questions/52391440/you-dont-have-permission-to-access-on-this-server)
- Error: 'Bad Request Your browser sent a request that this server could not understand. Additionally, a 400 Bad Request error was encountered while trying to use an ErrorDocument to handle the request.'
you must have included '_' in your DocumentRoot or somewhere in your conf file. [see detail](https://stackoverflow.com/questions/43925672/bad-request-your-browser-sent-a-request-that-this-server-could-not-understand)

:warning: everytime you change the conf file, you need to reload the apache2 (`sudo systemctl reload apache2`)
:warning: remember to read to `error.log`(in `/var/log/`) is important


# 拓展
- [linux环境下Apache配置多个虚拟主机挂载多站点同时运行](https://baijunyao.com/article/9)
