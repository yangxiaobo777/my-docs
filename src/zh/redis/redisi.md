## redis简介
::: info
Remote Dictionary Server(远程字典服务)是完全开源的，使用ANSIC语言编写遵守BSD协议，是一个高性能的Key-Value数据库提供了丰富的数据结构，例如String、Hash、List、Set、SortedSet等等。数据是存在内存中的，同时Redis支持事务、持久化、LUA脚本、发布/订阅、缓存淘汰、流技术等多种功能特性提供了主从模式、Redis Sentinel和Redis Cluster集群架构方案
:::
![作者](/redis/atlz.png)
- [github](https://github.com/antirez)
- [个人博客](http://antirez.com/latest/0)
## redis可以做什么
- **分布式缓存**
 :::info
  与传统数据库关系(mysql)
  Redis是key-value数据库(NoSQL一种)，mysql是关系数据库
  Redis数据操作主要在内存，而mysql主要存储在磁盘
  Redis在某一些场景使用中要明显优于mysql，比如计数器、排行榜等方面
  Redis通常用于一些特定场景，需要与Mysql一起配合使用
  两者并不是相互替换和竞争关系，而是共用和配合使用
  ![](/redis/cache.png)
 :::
- **持久化**
 :::info
  内存存储和持久化(RDB&AOF)
  redis支持异步的将内存中数据写到磁盘，同时不影响服务
 :::
- **高可用架构**
 :::info
  - 单机
  - 主从
  - 哨兵
  - 集群
 :::
- **分布式锁等等。。。**
 :::info 总览
  ![](/redis/todo.png)
 :::

## redis的优势
- 性能极高：redis的读的速度是110000次/秒，写的速度是81000次/秒
- 数据类型丰富(string,list,set,hset,zset,bitmap...)
- 支持数据持久化，可以将内存的数据保存在磁盘中。重启的时候可以再次加载
- 支持数据备份(主从模式)
:::info
![](/redis/allRedis.png)
:::
## redis安装与配制
- **下载**
:::info
- [官网](https://redis.io)
- [中文官网1](https://www.redis.cn/)
- [中文官网2](https://www.redis.com.cn/)
- [源码](https://github.com/redis/redis)
- [在线](https://try.redis.io/)
- [命令手册](http://doc.redisfans.com)
:::
---
:::info
  Redis从发布至今，已经有十余年的时光了，一直遵循着自己的命名规则：
版本号第二位如果是奇数，则为非稳定版本 如2.7、2.9、3.1
版本号第二位如果是偶数，则为稳定版本 如2.6、2.8、3.0、3.2
当前奇数版本就是下一个稳定版本的开发版本，如2.9版本是3.0版本的开发版本
我们可以通过redis.io官网来下载自己感兴趣的版本进行源码阅读：
历史发布版本的源码：https://download.redis.io/releases/
:::
- **安装**
:::info VMWare虚拟机安装
 1. 查看自己的linux是32位还是64位
 ```shell
 getconf LONG_BIT
 ```
 2. 安装gcc
 ```shell
 gcc -v
 yum -y install gcc c++
 ```
 3. 下载好的redis(redis-7.0.0.tar.gz)安装包放置在/opt目录下
 4. 解压安装包
 ```shell
 tar -zxvf redis-7.0.0.tar.gz
 ```
 5. 进入/redis-7.0.0目录，执行如下命令
 ```shell
 make && make install
 ```
 6. 查看默认安装目录/usr/local/bin
 - redis-benchmark: 性能测试工具，服务启动后运行该命令，测试性能
 - redis-check-aof: 修复有问题的aof文件
 - redis-check-dump: 修复有问题的rdb文件
 - redis-cli: 客户端操作入口
 - redis-sentinel: redis哨兵启动
 - redis-server: redis服务器启动命令
 7. 将redis.conf拷贝到自己设置的路径下，比如/myredis
 8. 修改拷贝的redis.conf
 ```text
   默认daemonize no               改为  daemonize yes

   默认protected-mode  yes        改为  protected-mode no

   默认bind 127.0.0.1             改为  直接注释掉(默认bind 127.0.0.1只能本机访问)或改成本机IP地址，否则影响远程IP连接)

   添加redis密码                  改为 requirepass 你自己设置的密码
 ```
 9. 启动服务
 ```shell
 redis-server /myconf/redis.conf
 ```
 10. 连接服务
 ```shell
 redis-cli -a ***** -p 6379 (-h,-c...)
 ```
 11. 关闭
 ```
 单实例关闭
 redis-cli -a **** shutdown
 多实例关闭,指定端口号
 redis-cli -a **** -p 6380 shutdown
 ```
:::
- **卸载**
:::danger redis版本更新
 1. 停止redis服务
 ```shell
 redis-cli -a **** shutdown
 ```
 2. 删除所有/usr/local/bin下的与redis有关的文件
 ```shell
 rm -rf redis-*
 ```
:::
