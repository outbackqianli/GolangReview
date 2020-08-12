## 常用Linux命令

如果熟悉Linux，下面这些命令很简单。如果你不熟悉，那么下面这些是用到的比较频繁的命令，可以帮助你快速上手服务器操作。

* **top/htop**
> 查看当前服务器负载

* **free -m**
> 查看服务器内存使用情况

* **lsof -i :xxx** (lsof -i :11300)
> 查看xxx端口被什么进程占用

* **ps -ef | grep "xxx"** (grep "loyocloud-oa")
> 搜索"xxx"关键字的进程

* **nohup xxx &**  (nohup ./loyocloud-oa &)
> 后台执行xxx命令，输出保存在当前目录的nohup.log文件中 

* **less xxx**
> 查看log文件，打开后按F切换到实时更新模式（如同tail -f），Ctrl+C退出实时更新模式

* **tail -f xxx** (tail -f loyocloud-oa.log)
> 实时查看xxx文件

* **tail -xxx yyy** (tail -1000 loyocloud-oa.log)
> 查看yyy文件的最后xxx行(当文件比较大时)

* **cat xxx | grep "yyy"** (cat loyocloud-oa.log | grep "2017-07-18")
> 搜索xxx文件中包含yyy字符的行(可以连续使用grep)

* **which xxx** (which redis-server)
> 再PATH中寻找xxx命令的路径

* **kill -9 xxx** (kill -9 2121)
> 强制终止xxx进程(进程号可通过上面的ps或lsof命令得到)

* **tar -czvf xxx yyy** (tar -czvf test.tar.gz ./*)
> 打包yyy文件为xxx压缩文件

* **tar -zxvf xxx** (tar -zxvf test.tar.gz)
> 解压xxx压缩文件到当前目录

* **df -h xxx** (df -h /)
> 查看磁盘使用情况,xxx指定挂载点,不跟显示所以挂载点

* **scp xxx:yyy zzz** (scp -P 22022 root@staging.ukuaiqi.com:~/test .) 
> 拷贝xxx服务器上的xxx文件到本地的zzz中

* **scp xxx yyy:zzz** (scp -P 22022 test root@staging.ukuaiqi.com:~/test) 

> 拷贝本地的xxx文件到yyy服务器上的zzz中