# Docker概述

## 	Docker为什么出现

传统:开发jar,运维来部署!

现在:开发打包部署上线,一套流程做完!

![image-20220112142940644](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220112142940644.png)

隔离:Docker核心思想!打包装箱!每个箱子是相互隔离的。

Docker通过隔离机制，可以将服务器利用到极致！

本质：所欲的技术都是因为出现了一些问题，我们需要去解决，才去学习！

## Docker的历史

2010年，几个搞IT的年轻人，就在美国成立了一家公司`dotCloud`

做一些 pass的云计算服务!LXC有关的容器技术!

他们将自己的技术(容器化技术)命名就是Docker!

Docker刚刚诞生的时候,没有引起行业的注意！

`开源`

2013年Docker开源了!

Docker越来越多的人发现了Docker 的优点!火了,Docker每个月都会更细哪一个版本!

2014年4月9日,Docker1.0发布!

Docker为什么这么火?相对虚拟机十分轻巧!

在容器技术出来之前,我们都是使用的虚拟机技术!

`虚拟机`在Windows中装一个Vmware，通过这个软件我们可以虚拟出来一台或者多台电脑！缺点是笨重！

虚拟机也是属于虚拟化技术，Docker容器技术，也是一中虚拟化技术！

```shell
vm:liunx centos原生镜像(一个电脑!)隔离,需要开启多个虚拟机! 几个G 几分钟

docker,隔离,镜像(最核心的环境4m+jdk+mysql)十分小巧,运行镜像就可以了! 小巧! 几个M KB 秒级启动
```

到现在所有开发人员都必须要会Docker！





>聊聊Docker

Docker是基于Go语言开发的！`开源项目`

官网：https://www.docker.com/

文档地址:https://docs.docker.com/ Docker的文档是超级详细的！

仓库地址:https://hub.docker.com/  



## Docker能干嘛

> 之前的虚拟机技术！

![image-20220112145148064](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220112145148064.png)

`虚拟机的缺点：`

1、资源占用十分多

2、冗余步骤多

3、启动很慢

> 容器化技术

虚拟化技术不是模拟的一个完整的操作系统

![image-20220112145948761](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220112145948761.png)

  比较Docker和虚拟机的技术不同

- 传统虚拟机，虚拟出一条硬件，运行一个完整的系统，然后在这个系统上安装运行软件
- 容器内的应用直接运行在宿主机的内容，容器是没有自己的内核的，也没有虚拟我们的硬件，所有就轻便了
- 每个容器是相互隔离的，每个容器都有属于自己的文件系统，互不影响

 >DevOps(开发、运维)

**应用更快速的交付和部署**

传统：一堆帮助文档，安装程序

Docker：打包镜像发布测试，一件运行

**更便捷的升级和扩缩容**

使用Docker之后，我们部署应用就和搭积木一样！

项目打宝为一个镜像，扩展 服务器A！ 服务器B

**更简单的系统运维**

在容器化之后，我们的开发，测试环境都是高度一致。

**更高效的计算资源利用**

Docker是内核级别的虚拟化，可以再一个物理机上可以运行很多的容器实例！服务器的性能可以被压榨到极致。

# Docker安装

## Docker的基本组成

![image-20220112151455878](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220112151455878.png)

**镜像（images）：**

Docker镜像就好比是一个模板，看他通过这个模板来在创建容器服务，tomcat镜像===>run ===> tomcat01容器（提供服务），通过这个镜像可以创建多个容器（最终服务运行或者项目运行就是在容器中的）。

**容器（container）：**

Docker利用容器技术，独立运行一个或者一组应用，通关镜像来创建的。

启动，停告知删除，基本命令

目前就可以把这个容器理解为就是一个建议的liunx系统

**仓库（repository）：**

仓库就是存放镜像的地方！

仓库分为公有仓库和私有仓库！

Docker Hub（默认是国外的）

阿里云...都有容器服务（配置镜像加速）

## 安装Docker

> 环境准备

1、需要会一点点的liunx的基础

2、CentOS 7

3、使用远程连接软件Xsheel

> 环境查看

```shell
#查看系统内核
uname -r
#查看系统版本
cat /etc/os-release
```

> 安装

帮助文档：文档地址:https://docs.docker.com/ 

```shell
# 1、卸载旧的版本
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
                  
# 2、需要的安装包
yum install -y yum-utils


# 报错了： 错误：rpmdb: BDB0113 Thread/process 136661/140660029847360 failed: BDB1507 Thread died in Berkeley DB library
# 解决地址：https://www.cnblogs.com/ltlinux/p/12963725.html
# 解决方式：重新构建rpm数据库
[root@localhost ~]# cd /var/lib/rpm
[root@localhost rpm]# ls
Basenames     __db.001  __db.003  Group       Name          Packages     Requirename  Sigmd5
Conflictname  __db.002  Dirnames  Installtid  Obsoletename  Providename  Sha1header   Triggername
[root@localhost rpm]# rm -rf __db*
[root@localhost rpm]# rpm --rebuilddb

# 3、设置镜像的仓库
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo  #官网是国外的
    
yum-config-manager \
    --add-repo \
http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo #推荐使用阿里云的

# 更新yum软件包索引
yum makecache fast

# 4、安装docker相关的内容 docker-ce 社区版 ee企业版
yum install docker-ce docker-ce-cli containerd.io

# 5、启动docker
systemctl start docker

# 6、判断docker是否安装成功
docker version

# 7、hello-world
docker run hello-world

# 8、查看一下下载的这个hello-world镜像
docker images
```

了解：卸载docker

```shell
# 1、卸载依赖
yum remove docker-ce docker-ce-cli containerd.io

# 2、删除资源
rm -rf /var/lib/docker

# /var/lib/docker	docker的默认工作路径
```

## 阿里云镜像加速

1、登录阿里云找到容器服务

2、找到镜像加速地址

3、配置使用

## 回顾HelloWord流程

![image-20220112194444649](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220112194444649.png)

## 底层原理

**Docker是怎么工作的？**

Docker是一个Client-Server结构的系统，Docker的守护进程运行在主机上。通过Socket从客户端访问！

DockerServer接收到Docker-Client的指令，就会执行这个命令！

![image-20220112195625306](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220112195625306.png)

**Docker为什么比VM快？**

1、Docker有着比虚拟机更少的抽象层。

2、Docker利用的是宿主机的内核，vm需要是GuestOS。

![image-20220112195739590](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220112195739590.png)

所以说，新建一个容器的时候，Docker不需要像虚拟机一样出现加载一个操作系统，避免引导。虚拟机加载GuestOS，分钟级别的，而Docker是利用宿主机的操作系统，省略了这个复杂的过程，秒级的！

![image-20220112200147317](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220112200147317.png)

之后学习完毕所有的命令，在回过头来看这段理论，就会很清晰！

# Docker的常用命令

## 帮助命令

```shell
docker version		#显示docker版本信息
docker info			#显示docker的系统信息，包括镜像和容器的数量
docker 命令 --help		#帮助命令
```

官方文档：https://docs.docker.com/reference/

## 镜像命令

```shell
docker images	# 查看所有本地主机上的镜像

# 解释
REPOSITORY  镜像的仓库源
TAG			镜像的标签
IMAGE ID	镜像的id
CREATED		镜像的创建时间
SIZE		镜像的的大小

# 可选项
-a	#列出所有镜像
-q	#值显示镜像的ID 


```

**docker search #搜索镜像**

```shell
#可选项，通过收藏来过滤
--filter=STARS=3000	#搜索出来的镜像就是STARS大于3000

docker search mysql --filter=STARS=3000 #搜索mysql
```

**docker pull 下载镜像**

```shell
# 下载镜像docker pull 镜像名 [:tag]
docker pull mysql	#如果不写tag，默认就是latest
#docker pull的原理：分层下载，docker iamge的核心 联合文件系统
#Digest 签名
#docker.io 真实地址

# 等价于它
docker pull mysql
docker pull docker.io/library/mysql:latest

#指定版本
docker pull mysql:5.7 

```

**docker rmi删除镜像**

```shell
docker rmi -f 镜像ID	#根据ID删除指定镜像
docker rmi -f 镜像ID 镜像ID 镜像ID	#删除多个镜像
docker rmi -f $(docker images -aq)	#删除所有镜像
```

## 容器命令

**说明：我们有了镜像才可以创建容器，liunx，下载一个centOS镜像来测试学习**

```shell
docker pull centos
```

**新建容器并启动**

```shell
docker run [可选参数] image

# 参数说明
--name="Name"	# 容器名字 tomcat01 tomcat02 ，用来区分容器
-d	# 后台方式运行
-it	# 使用交互方式运行，进入容器查看内容
-p	# 指定容器的端口 -p 8080:8080
	-p ip：主机端口容器端口
	-p 主机端口：容器端口（常用）
	-p 容器端口
-P	# 随机指定端口

#测试,启动并进入容器
dockeer run -it centos /bin/bash
```

**列出所有的运行的容器**

```shell
# docker ps 命令
	# 列出所有的运行的容器
-a	# 列出所有的运行的容器+带出历史运行过的容器
-n=?	# 系那是最创建的容器
-q	# 只显示容器的编号
```

**退出容器**

```shell
exit	# 直接容器停止并退出到主机
Ctrl+p+q	# 容器不停止退出
```

**删除容器**

```shell
docker rm 容器ID	# 删除指定的容器，不能删除正在运行的容器，如果要强制删除rm -f
docker rm -f $(docker ps -aq)	# 删除所有的容器
docker ps -a -q|xargs  docker rm	# 删除所有的容器
```

**启动和停止容器的操作**

```shell
docker start 容器ID	# 启动容器
docker restart 容器ID	# 重启容器
docker stop 容器ID	#停止当前正在运行的容器
docker kill	容器ID	#强制停止当前容器
```

## 常用的其他命令

**后台启动容器**

```shell
# 命令 docker run -d 镜像名：
docker run -d centos
# 问题docker ps 发现centos停止了

# 常见的坑，docker容器使用后台运行，就必须要有一个前台进程，docker发现没有应用，就会自动停止
# nainx，容器启动后，发现自己没有提供服务，就会立刻停止，就是没有程序了
```

**查看日志**

```shell
docker logs -tf --tail 10 容器ID # 容器，没有日志

# 自己编写一个脚本
docker run -d centos /bin/sh -c "while true:do echo kuangshen;sleep 1;done"

docker ps	# 查看运行的容器

#显示日志
-rf	# 显示日志 f是带上时间戳
--tail number	# 要显示日志条数
docker logs -tf --tail 10 容器ID
```

**查看容器中进程信息ps**

```shell
docker top 容器ID
```

**查看镜像的元数据**

```shell
# docker inspect 容器ID	#查看镜像的元数据
```

**进入当前正在运行的容器**

```shell
# 我们通常容器都是使用后台方式运行的，需要进入容器，修改一些配置

# 命令
docker exec -it 容器id bashshell

# 测试
docker exec -it 容器id /bin/bash

# 方式二:正在执行当前的代码...
docker attach 容器id

# docker exec	# 进入容器后开启一个新的终端，可以在里面操作（常用）
# docker attach	#进入容器正在执行的终端，不会启动心的进程
```

**从容器内拷贝文件到主机上**

```shell
docker cp 容器id:复制路径文件 目标路径

# 将这个文件拷贝出来到主机上
docker cp 容器id:/home/kuangshen.java /home

#拷贝是一种手动过程，未来我们使用 -v 卷的技术，可以实现，自动同步
```



## 小节

![image-20220122125749709](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220122125749709.png)

## 作业练习

> Docker安装Nainx

```shell
# 1、搜索镜像 search 建议大家去docker搜索，可以看到帮助文档
# 2、下载镜像 pull
# 3、运行测试
# 	docker images 查看当前镜像

#	docker run -d --name nainx01 -p 3344:80 nginx
#  		-d 后台运行
#  		--name 给容器名
#  		-p 宿主机端口，容器内部端口

#	docker ps	查看运行中的镜像

#	docker exec -it nainx01 /bin/bash	进入容器
#	whereis nainx	查看nainx的目录

#	docker stop NAMES	#停止服务


curl localhost:3344	#liunx访问网页
```

端口暴露的概念

![image-20220122130850055](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220122130850055.png)

思考问题：我们每次改动nginx配置文件，都需要进入容器内部?十分的麻烦，我要是可以在容器外部提供一个映射路径，达到在容器修改文件名，容器内部就可以自动修改？-v 数据卷！

> 作业：docker 来装一个tomcat 

```shell
# 官网的使用
docker run -it --rm tomccat:9.0	#一搬用来测试，用完就删除

# 我们之前的启动都是后台，停止了容器之后，容器还是可以查到
docker run -it tomcat:8	#doerhub上搜索版本号

# 下载在启动
docker pull tomcat:9.0

# 启动运行
docker images	#查看镜像包

# 启动容器
docker run -d -p 3355:8080 tomcat01 tomcat	

# 进入容器
docker exec -it tomcat01 /bin/bash	

# 发现问题：1、liunx命令少了 2、没有webapps，阿里云镜像的原因，默认是最小镜像，所有不必要的都剔除掉
# 保证最小可运行环境！

# 方式一：吧webapps.dis 复制到webapps目录下
cp -r webapps.dist/* webapss

# 查看所有文件
ls -al

```

思考问题：我们以后要部署项目，如果每次都要进入容器是不是十分麻烦？我要是可以在容器外部提供一个映射路径，webapps，我们在外部放置项目，就自动同步到内部就好了！

docker容器 tomcat+网站 docker+mysql

> 作业：部署 es+kibana

```shell
# es 暴露的端口很多！
# es 十分耗内存
# es 的数据一半需要放置到安全目录！挂载

# dockerhub 上搜索 elasticsearch
#	--net somenetwork ? 网络配置
#	tag	版本号
docker run -d --name elasticsearch --net somenetwork -p 9200:9200 -p 9300:9300 -e "discovery.type-single-node" elasticsearch:tag

# 去掉--net somenetwork 还没学	启动elasticsearch
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type-single-node" elasticsearch:tag

# 启动了liunx就很卡 直接卡住了

# 查看 cpu的状态
docker stats

# 增加内训的限制，修改配置文件 -e 环境配置修改
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type-single-node" -e ES_JAVA_OPTS="Xms64m -Xmx521m" elasticsearch:tag
```

> 作业：使用kibana连接ES？网络如何才能连接过去！

![image-20220122135221944](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220122135221944.png)

## 可视化

- portainer（先用这个）

  ```shell
  docker run -d -p 8080:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
  ```

  

- Rancher（CI/CD 再用）

**什么是portainer?**

Docker图形化页面管理工具！提供一个后台面板供我们操作！

```shell
docker run -d -p 8080:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
```

# Docker镜像讲解

## 镜像是什么

进项是一种轻量级，可执行的独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需的所有内容，包括代码、运行时、库、环境变量和配置文件。

所有的应用，直接打宝docker镜像，就可以直接跑起来！

**如何得到镜像：**

- 从远程仓库下载
- 朋友拷贝
- 自己制作一个镜像DockerFile

## Docker镜像加载原理

> UnionFS(联合文件系统)

UnionFS(联合文件系统）:Union文件系统( UnionFS )是一种分层、轻量级并且高性能的文件系统，它支持对文件系统的修改作为一次提交来一层层的盈加，同时可以将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtualfilesystem)。Union文件系统是Docker镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。
	特性∶一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统暨加起来，这样最终的文件系统会包含所有底层的文件和目录 

> Docker镜像加载原理

docker的镜像实际上由一层一层的文件系统组成，这种层级的文件系统UnionFS.

bootfs(boot file system)主要包含bootloader和kernel, bootloader主要是引导加载kernel, Linux刚启动时会加载bootfs文件系统，在Docker镜像的最底层是bootfs。这一层与我们典型的Linux/Unix系统是一样的，包含boot加载器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由bootfs转交给内核，此时系统也会卸载bootfs。

rootfs (root file system)，在bootfs之上。包含的就是典型Linux.系统中的/dev,/proc, /bin, letc等标准目录和文件。rootfs就是各种不同的操作系统发行版，比如Ubuntu , Centos等等。

![image-20220122141319653](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220122141319653.png)

平时我们安装金虚拟机的CentOs都是好几个G，为什么Docker这里才200M？

对于一个精简的OS，rootfs可以很小，只需要包含最基本的命令，工具和程序就可以了，应为底层直接用Hos的kernel，自己只需要提供rootfs就可以了。由此可见对于不同的liunx发型版，bootfs基本是一致的，rootfs会有差别，因此不同的发型版可以共用bootsf。

## 分层理解

> 分层的镜像

我们可以下载一个镜像，注意观察狭隘的日志输出，可以看到是一层一层的在下载！

思考:为什么Docker镜像要采用这种分层的结构呢?

最大的好处，我觉得莫过于是资源共享了!比如有多个镜像都从相同的Base镜像构建而来，那么宿主机只需在磁盘上保留一份base镜像，同时内存中也只需要加载一份base镜像，这样就可以为所有的容器服务了，而且镜像的每一层都可以被共享。

查看镜像分层的方式可以通过docker image inspect命令!

**理解**

所有的Docker镜像都起始于一个基础镜像层，当进行修改或增加新的内容时，就会在当前镜像层之上，创建新的镜像层。

举一个简单的例子，假如基于Ubuntu Linux 16.04创建一个新的镜像，这就是新镜像的第一层﹔如果在该镜像中添加Python包，就会在基础镜像层之上创建第二个镜像层﹔如果继续添加一个安全补丁，就会创建第三个镜像层。

该镜像当前已经包含3个镜像层，如下图所示(这只是一个用于演示的很简单的例子)。

![image-20220122142759911](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220122142759911.png)

在添加额外的镜像层的同时，镜像始终保持是当前所有镜像的组合，理解这一点非常重要。下图中举了一个简单的例子，每个镜像层包含3个文件，而镜像包含了来自两个镜像层的6个文件。

![image-20220122142826630](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220122142826630.png)

上图中的镜像层跟之前图中的略有区别，主要目的是便于展示文件。

下图中展示了一个稍微复杂的三层镜像，在外部看来整个镜像只有6个文件，这是因为最上层中的文件7是文件5的一个更新版本。

![image-20220122143037501](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220122143037501.png)

这种情况下，上层镜像层中的文件覆盖了底层镜像层中的文件。这样就使得文件的更新版本作为一个新镜像层添加到镜像当中。

 Docker通过存储引擎（新版本采用快照机制)的方式来实现镜像层堆栈，并保证多镜像层对外展示为统一的文件系统。

Linux上可用的存储引擎有AUFS、Overlay2、Device Mapper、Btrfs以及.ZFS。顾名思义，每种存储引擎都基于Linux中对应的文件系统或者块设备技术，并且每种存储引擎都有其独有的性能特点。

Docker在Windows上仅支持windowsfilter一种存储引擎，该引擎基于NTFS文件系统之上实现了分层和CoW[1].

下图展示了与系统显示相同的三层镜像。所有镜像层堆霄并合并，对外提供统一的视图。

![image-20220122143148110](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220122143148110.png)

> 特点

Docker镜像都是只读的，当容器启动时，一个新的科协层被加载到镜像的顶部！

这一层就是我们通常说的容器层，容器之下的都叫镜像层！

> 如何提交一个自己的镜像

## comment镜像

```shell
docker commit #提交容器成为一个新的副本

# 命令和git类似
docker commit -m="提交的描述信息" -a="作者" 容器id 目标镜像名：[TAG]版本号
```

**实战测试**

```shell
# 启动默认tomcat
docker run -it -p8080:8080 tomcat
	#-p 暴露端口
	#-it 交互模式启动
	
# 发现这个默认的tomcat是没有webapps应用，镜像的原因，官方的镜像默认webapps下面是没有文件的

# 查看容器
docker ps

# 进入容器
dockerexec -it 容器id /bin/bash

# 拷贝webapps.dist
cp -r weapps.dist/* weapps
	# -r 递归拷贝
	
	
# 提交镜像
docker commit -a="Star" -m="add webapps app" 容器id tomcat02:1.0
```

学习方式：理解概念，但是一定要实践，最后实践和理论结合，一次搞定这个知识！

```shell
# 如果你想保存当前容器的状态，就可以通过commit来提交，获得一个镜像
# 就好比学VM中的快照！
```

## 容器数据卷

### 什么是容器数据卷

**Docker历年回顾**

将应用和环境打包成一个镜像！

数据？如果数据都在容器中，那么我们容器删除，数据就会丢失！需求：数据可以持久化

MySQL，容器删了=删库跑路！需求：MySQL数据可以存储在本地！

容器之间可以有个数据共享技术！Docker容器中产生的数据，同步到本地！

这就是卷技术！目录的挂载，将我们容器内的目录，挂载到liunx上面！

![image-20220124174517502](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124174517502.png)

**总结：容器的持久化和同步操作！容器间也是可以数据共享的！**

### 使用数据卷

> 方式一：直接使用命令来挂载 -v  v = volume

```shell
docker run -it -v 主机目录:容器内目录

# 测试
docker run -it -v /home/ceshi:/home centos /bin/bash

# 启动起来之后，可以通过docker inspect 容器id 查看容器详细信息
docker inspect 容器ID

# 查看所有容器
docker ps -a

# 开启容器
docker start 容器ID

# 连接容器
docker attach 容器ID

```

![image-20220124175111448](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124175111448.png)

**好处：我们以后修改只需要在本地修改即可，容器会自动同步！**

### 实战：安装MySQL

思考：MySQL的数据持久化问题！

```shell
# 搜索mysql
docker search mysql

# 拉取mysql
docker pull mysql:5.7

# 安装启动MySQL 需要配置密码的，这是注意点！
# 运行容器，需要做数据挂载 /home/mysql真实路径 -v可以挂载多个目录
# 官方测试：docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:tag
# 启动我们的
-d 后台运行
-p 端口映射
-v 数据卷挂载
-e 环境配置
--name 容器名字
docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7

# 启动成功之后，在本地使用sql工具来测试一下
# sql工具连接到服务器的3310，3310和容器内的3306映射，这个时候就可以连接上了！

# 在本地测试创建一个数据库，查看ix我们映射的路径是否ok

# 删除容器
docker rm -f mysql01

# 查看所有容器
docker ps -a
```

**结论：假设容器删除，发现挂载到本地的数据卷依旧没有丢失，这就是实现了容器数据持久化功能！**

### 具名和匿名挂载

```shell
# 匿名挂载, -v 只指定容器内的，没有指定容器外的
-v 容器内路径！
docker run -d -p --name nainx01 -v /etc/nginx nginx

# 查看所有的volume的情况 
docker volume ls
local			3f388efefe8fe8fe8fe8fefafa8f8ef8

# 这里发现，这种就是匿名挂载，我们在 -v 只写了容器内的路径，没有写容器外的路径！

# 具名挂载
docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx nginx

# 通过 -v 卷名：容器内路径

#查看一下这个卷
docker volume inspect juming-nginx

```

![image-20220124185713741](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124185713741.png)

所有的docker容器内的卷，没有指定目录的情况下，都是在`/var/lib/docker/volume/xxx/...data`

我们通过具名挂载可以方便的找到我们的一个卷，大多数情况在使用`具名挂载`

```shell
# 怎么区分匿名挂载和具名挂载，还是指定路径挂载
-v 容器内的路径	# 匿名路径
-v 卷名:容器内的录# 具名路径
-v /宿主机路径:容器内路径	# 指定路径挂载
```

拓展：

```shell
# 通过 -v 容器内路径:ro rw 改变读写权限
ro redonly	#可读
rw readwrite	#可读可写

# 一旦这个设置了容器权限，容器对我们挂载出来的内容就有限定了！
docker run -d -P --name nginx2 -v juming-nginx:/etc/nginx:ro nginx
docker run -d -P --name nginx2 -v juming-nginx:/etc/nginx:rw nginx

# ro 只要看到ro就说明这个路径就只能通过宿主机来操作，容器内部是无法操作的。
# rw 容器可读可写
```

### 初识DockerFile

DockerFile就是来构建docker镜像的构建文件！命令脚本！先体验一下!

通过脚本可以生成惊镜像，镜像是一层一层的，脚本是一个个命令，

> 方式二：

```shell
# 创建一个dockerfile文件，名字可以随机，建议dockerfile
# 文件中的内容 指令（大写） 参数
# 编写脚本
vim dockerfile

# 脚本内容
FROM centos
# 匿名挂载
VOLUME ["volume01","volume02"]
CMD echo "----end----"
CMD /bin/bash

# 这里每个命令，就是镜像的一层

# 构建一个镜像
-f 构建的地址
.	构建到当前的目录下
docker build -f /home/docker-test-volume/dockerfile1 -t kuangshen/centos:1.0 .
```

![image-20220124191417058](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124191417058.png)

```shell
# 启动自己写的容器
docker run -it 镜像ID
```

![image-20220124192109918](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124192109918.png)

这个卷和外部一定有一个同步的目录！

![image-20220124192202034](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124192202034.png)

​	

```shell
# 查看匿名卷挂载的路径信息
docker inspect 容器ID
```

![image-20220124212023422](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124212023422.png)

这种方式文末未来使用非常多，因为我们通常会构建自己的镜像！

假设构建镜像时候没有挂载卷，就要手动挂载 -v 卷名:容器内路径！

### 数据卷容器

两个MySQL同步数据，数据共享！

![image-20220124212504180](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124212504180.png)

```shell
# 启动3个容器，通过我们刚才自己写的镜像启动
docker run -it --name kuangshen/centos:1.0

# 不关闭退出
ctrl+P+Q

# 绑定共享数据
docker run -it --name docker02 --volumes-from docker01 kuangshen/centos:1.0

# 进入容器
docker attach 容器ID

# 只要通过 --volumes-from 我们就可以容器间实现数据共享了
```

![image-20220124212704118](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124212704118.png)

```shell
# 测试，可以删除docker01，查看一下docker02和docker03是否还可以访问这个文件
# 测试发现依旧可以访问
```

![image-20220124213525327](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124213525327.png)

多个MySQL实现数据共享

```shell
# 启动两个MySQL实现数据共享
-d 后台运行
-p 端口映射
-v 数据卷
-e 环境配置
# 启动mysql 01
docker run -d -p 3310:3306 -v /etc/mysql/conf.d -v /var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql5.7

# 启动mysql 02 并绑定mysql 01 卷
docker run -d -p 3311:3306 -e MYSQL_ROOT_PASSWORD=123456 --volume-from --name mysql02 mysql5.7

# 这个时候，可以实现两个容器数据同步
```

**结论：**

容器之间配置信息传递，数据卷容器的生命周期一直持续到没有容器使用为止。

但是一旦持久化到了本地，这个时候本地的数据是不会删除的！

## DockerFile

### DockerFile介绍

dockerfile 是用来构建docker镜像的文件！命令参数脚本！

构建步骤：

1、编写一个 dockerfile 文件

2、docker build 构建一个镜像

3、docker run 运行镜像

4、docker push 发布镜像 （dockerHub、阿里云镜像仓库）

很多官方镜像都是基础包，很多功能没有，我们通常会自己搭建自己的镜像！

官方既然可以制作镜像，我们也可以！

### DockerFile的制作过程

**基础知识**

1、每个保留关键字（指令）都是必须是大写字母

2、执行从上到下顺序执行

3、#表示注释

4、每一个指令都会创建提交一个新的镜像层，并提交！

![image-20220124215303176](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124215303176.png)

dockerfile是面向开发的，我们以后要发布项目，做镜像，就需要编写dockerfile文件，这个文件十分简单！

Docker镜像逐渐成为企业交付的标准，必须要掌握！

DokcerFile：构建文件，定义了一切的步骤，源代码

DockerIamge：通过DockerFile构建生成的镜像，最终发布和运行的产品！原来是jar war，现在是直接通过Docker运行！

Docker容器：容器就是镜像运行起来提供服的！

### DockerFile指令

以前的话我们就是使用别人的，现在我们知道这些指令，我们来练习一个镜像！

```shell
FROM		# 基础镜像，一切从这里开始构建 需要centos
MAINTAINER	# 镜像是谁写的，姓名+邮箱
RUN			# 镜像构建的时候需要运行的命令
ADD			# 步骤：tomcat镜像，需要一个tomcat压缩包！添加内容
WORKDIR		# 镜像的工作目录
VOLUME		# 挂载的目录
EXPOSE		# 暴露端口配置
CMD			# 指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代
ENTRYPOINT	# 指定这个容器启动的时候需要运行命令，可以追加命令
ONBUILD		# 当构建一个被继承 DockerFile 这个时候就会运行ONBUILD 的指令，触发指令。
COPY		# 类似ADD ，将我们文件拷贝到镜像中
ENV			# 构建的时候设置环境变量！
```



![image-20220124215745623](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220124215745623.png)

### 实战测试

Docker Hub 中 99% 镜像都是从这个基础镜像过来的`FROM scratch`，然后配置需要的软件和配置来进行的构建

> 创建一个自己的centos

```shell
# 1、编写DockerFile的文件，编写脚本
vim mydockerfile-centeros

# 指定一个基础镜像
FROM centos
MAINTAINER QianXunJian<2589857361@qq.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools

EXPOSE 80

CMD echo $MYPATH
CMD echo "---end---"
CMD /bin/bash

# 2、通过这个文件构件镜像
# 命令 docker build -f dockerfile文件路径 -t 镜像名:[tag] .
docker build -f mydockerfile-centos -t mycentos0.1 .

# 3、测试运行
# 开启容器， -it 在后台运行
docker run -it mycentos:0.1
```

**我们可以列出本地进行的变更历史**

```shell
# 我们平时拿到镜像，可以研究一下它是怎么做的
docker history 镜像ID
```

> CMD和ENTRYPOINT的区别

```shell
CMD			# 指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代
ENTRYPOINT	# 指定这个容器启动的时候需要运行命令，可以追加命令
```

`测试cmd`

```shell
# 编写 dockerfile 文件
vim dockerfile-cmd-test

# 编写脚本
FROM centos
CMD ["ls",'-a']

# 构建镜像
docker build -f dockerfile-cmd-test -t cmdtest .

# run运行，发我们的ls -a 命令生效
docker run 镜像ID

# 想追加一个命令 -l; ls -al
docker run 镜像ID -l
# cmd的情况下， -l 替换了CMD ["ls","-a"]命令，-l 不是命令所以报错！
```

测试`ENTRYPOINT`

```shell
# 编写dockerfile文件
vim dockerfile-cmd-entrypoint

# 2、编写脚本
FROM centos
ENTRYPOINT ["ls","-a"]

# 3、构建
docker build -f dockerfile-cmd-entrypoint -t entrypoint-test .

# 我们的追加命令，是直接凭借在我们的 ENTRYPOINT 命令的后面！
docker run 镜像ID -l


```

DockerFile中很多命令都十分相似，我们需要了解他们的的区别，我们最好的学习就是对比他们然后测试效果！

### 实战：Tomcat镜像

1、准备镜像文件 tomcat 压缩包，jdk的压缩包！![image-20220125135041709](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125135041709.png)

2、编写Dockefile文件，`官方命名：Dockerfile`，build会自动寻找这个文件，不需要 -f 指定了！

```shell
# 1、编写 Dockerfilewe 文件
vim Dockerfile

# 2、开始编写脚本
FROM centos

MAINTAINER qianxunjian<2589857361@qq.com>

COPY readme.txt /usr/local/readme.txt

ADD jdk-8ull-linux-x64.gz /usr/local/
ADD apache-tomcat-9.0.22.tar.gz /usr/local/

RUN yum -y install vim

ENV MYPATH /usr/local
WORKDIR $MYPATH

ENV JAVA_HOME /usr/local/jdk1.8.0_11
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.22
ENV CATALINA_BASH /usr/local/apache-tomcat-9.0.22
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin

EXPOSE 8080

CMD /usr/local/apache-tomcat-9.0.22/bin/starup.sh && tail -F /url/local/apache-tomcat-9.0.22/bin/logs/catalina.out

# 3、构建镜像,由于官方命名，所以不用 -f 指定名字
docker build -t diytomcat .

# 4、启动
-d	# 后台运行
-p	# 暴露端口
-v	# 挂载 本地目录:容器内目录
docker run -d -p 9090:8080 --name qianxunjiantomcat -v /home/kuangshen/build/tomcat/test:/usr/local/apache-tomcat-9.0.22/webapps/test -v /home/kuangshen/build/tomcat/tomcatlogs:/usr/local/apache-tomcat-9.0.22/logs diytomcat

# 5、访问测试

# 6、发布项目（由于做了卷挂载，我们直接在本地编写项目就可以发布了！）

# 项目部署成功，可以直接访问OK！
```

```shell
# 停止容器
docker stop 容器id
```

我们以后开发的步骤：需要掌握Dockerfile的编写！我们之后的一切都是使用docker惊喜那个来发布运行！

### 发布自己的镜像

[狂神P32 发布镜像到阿里云容器服务](https://www.bilibili.com/video/BV1og4y1q7M4?p=32&spm_id_from=pageDriver)

> 发布在阿里云镜像服务上

1、登录阿里云

2、找到容器镜像服务

3、创建命名空间

4、创建容器镜像

5、浏览阿里云

![image-20220125143926820](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125143926820.png)



### 小节

![image-20220125144506963](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125144506963.png)



Docker网络

**理解Docker0**

清空所有环境

```shell
# 删除所有容器
docker rm -f $(docker ps -aq)

# 删除所有镜像
docker rmi -f $(docker images -aq)
```

> ip addr		查看到有三个网络

![image-20220125150800709](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125150800709.png)

问题：docker 是如何处理容器网络访问的？

![image-20220125151012875](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125151012875.png)

```shell
docker run -d -p --name tomcat01 tomcat

# 查看容器的内部网络地址ip addr，发现容器启动的时候会得到一个eth0 ip地址，docker分配的
docker exec -it tomcat01 ip addr

# 思考： liunx 能不能ping通容器内部！
# 答：liunx 可以 ping 通 docker 容器内部

```

> 原理

1、我们每启动一个 docker 容器，docker就会给容器分配一个ip，我们只要安装了docker，就会有一个网卡 docker0 桥接模式，使用的技术是 evth-pair 技术！

![image-20220125154303913](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125154303913.png)

2、在启动一个容器,发现又多了一对网卡！

```shell
# 启动容器 run
docker run -d -P -name tomcat02 tomcat

# 进入容器 -it后台运行
docker exec -it tomcat02 ip addr

# 我们发现这个容器带来网卡，都是一对对的
# evth-pair 就是一队的虚拟设备接口，他们都是成对出现的，一段连着下一，一段彼此相连
# 正因为这个特性，evth-pair 充当一个桥梁，连接各种虚拟网络设备的
# OpenStack，Docker容器之间的连接，ovs的连接，都是使用 evth-pair 技术
```

![image-20220125154432503](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125154432503.png)

3、我们来想一下tomcat01和tomcat02是否可以 ping 通？

```shell
docker exec -it tomcat02 ping 172.18.0.2

# 结论：容器和容器之间是可以相互ping通的！
```

![image-20220125155517534](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125155517534.png)

结论：tomcat01 和 tomcat02 是公用的一个路由器，docker0。

所有的容器不指定网络的情况下，都是 docker0 路由的，docker 会给我们的容器分配一个默认的可用IP

> 小节

Docker 使用的是Liunx的桥接，宿主机中是一个Docker容器的网桥 docker0。![image-20220125160009370](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125160009370.png)

Docker 中的所有的网络接口都是虚拟的。虚拟的转发效率高！（内网传输）

只要容器删除，对应网桥一对没了！

### --link

> `高可用`思考一个场景，我们编写一个微服务，database url = ip;项目不重启，数据库ip换掉了，我们希望可以处理这个问题，可以通过名字来进行访问容器？

```shell
docker exec -it tomcat 02 ping tomcat01
# ping 不通

# --link 命令链住
docker run -d -P --name tomcat03 --link tomcat02 tomcat

docker exec -it tomcat03 ping tomcat02
# ping 通了

# 反向可以ping通吗？
docker exec -it tomcat 02 ping tomcat03
# 反向 ping 不通！

# 查看网络的详细信息
docker network inspect [NETWORK ID]

```

探究：inspect！

```shell
hosts

# 查看tomcat03 的网络信息
docker exec -it tomcat03 cat /etc/hosts
```

![image-20220125161737071](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125161737071.png)

> --link 就是在我们的hosts配置中增加了一个172.18.0.3 tomcat 02 容器id
>
> 所以我们在tomcat03 中才可以通过容器名称或者容器ID去 ping 通 tomcat02
>
> `--link 现在Docker已经不推荐使用了`
>
> 自定义网络！不适用docker0！
>
> docker0问题：他不支持容器名连接访问
>
> 扩展：springcloud feign = 服务名



### 自定义网络

```shell
# 查看所有的Docker网络
docker network ls

# 移除网络
docker network rm [NAME]
```

**网络模式**

bridge：桥接 docker（默认，自己创建也使用bridge模式）

none：不配置网络

host：和宿主机共享网络

container：容器网络连通！（用的少！局限性很大）

**测试**

```shell
# 我们直接启动的命令，默认就有--net bridge，而这个就是我们的coker0
docker run -d -P --name tomcat01 tomcat  等于
docker run -d -P --name tomcat01 --net bridge tomcat

# docker0特点：默认，域名不能访问， --link可以打通连接！

# 我们可以自定义一个网络！
docker network create --driver brideg --subnet 192.168.0.0/16 --gateway 192.168.0.1 mynet

# 查看dokcer网络
docker network ls
```

![image-20220125163031844](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125163031844.png)

```shell
# 查看网络信息
docker network inspect [NAME]
```

![image-20220125163306058](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125163306058.png)

```shell
# 使用自己的网络
--net [网络NAME]
docker run -d -P --name tomcat-net-01 --net mynet tomcat
docker run -d -P --name tomcat-net-02 --net mynet tomcat

# 自定义的网络，对比docker0网络，自定义可以直接ping名字
docker exec -it tomcat-net-01 ping tomcat-net-02
```

> 结论：我们自定义的网络docker都已经帮我们维护好了我们对应的关系，推荐我们平时这样使用网络！

> 好处：搭建集群
> 		redis - 不同的集群使用不同的网络，保证集群是安全和健康的
>
> mysql - 不同的集群使用不同的网络，保证集群是安全和健康的

### 网络连通

```shell
# 容器连接到一个网络上
docker network connect mynet tomcat01

# 查看mynet的网络情况
docker network inspect mynet

# 连通之后就是将 tomcat01 放到了 mynet 网络下

# 官方解释：一个容器两个ip地址！
# 阿里云服务：公网ip 私网ip

# 测试：
# 01连通了mynet
# 02没有联通
```

![image-20220125164219316](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125164219316.png)

> 结论：假设要跨网络操作别的网段，就需要使用 docker network connect 连通！



### 实战：Redis集群

 ![image-20220125170732792](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125170732792.png)

```shell
# 移除容器
docker rm -f #(docker ps -aq)

# 创建一个网卡
docker network create redis --subnet 173.38.0.0/16

# 查看网络信息
docker network ls
docker network inspect redis

# 通过脚本创建六个redis配置
for port in $(seq 1 6):\
do \
mkdir -p /mydata/redis/node-${port}/conf
touch /mydata/redis/node-${port}/conf/redis.conf
cat << EOF >/mydata/redis/node-${port}/conf/redis.conf
port 6379
bind 0.0.0.0
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
cluster-announce-ip 172.38.0.1${port}
cluster-announce-port 6379
cluster-announce-bus-port 16379
appendonly yes
EOF
done

# 启动--编程脚本
docker run -p 637${port}:6379 -p 1637${port}:16379 --name redis-${port} \
-v /mydata/redis/node-${port}/data:/data \
-v /mydata/redis/node-${port}/conf/redis.conf:/etc/redis/redis.conf \
-d --net reddis --ip 172.38.0.1${port} redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf; \

# 启动--手动启动，改
docker run -p 6371:6379 -p 16371:16379 --name redis-1 \
-v /mydata/redis/node-1/data:/data \
-v /mydata/redis/node-1/conf/redis.conf:/etc/redis/redis.conf \
-d --net reddis --ip 172.38.0.11 redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf

# 创建集群
redis-cli --cluster create 172.38.0.11:6379 172.38.0.12:6379 172.38.0.13:6379 172.38.0.14:6379 172.38.0.15:6379 172.38.0.16:6379 --cluster-replicas 1
# 询问是否这么配置，输入yes

# 进入容器,redis中是没有bash命令的，用的sh命令
docker exec -it reids-1 /bin/sh

# 测试
redis-cli -c

# 集群的信息
cluster info

# 集群的节点
cluster nodes

# 新增一个值
set a b

# 停止一个redis，测试是否可以从机顶上来
docker stop redis-3

# 测试获取a的值，发现他是从从机上获取的，实现了高可用 
get a
```

docker搭建redis集群完成！

我们使用了docker之后，素有急速都会慢慢的变得简单起来！

## SpringBoot微服务打包Docker镜像

视频教程：[狂神视频](https://www.bilibili.com/video/BV1og4y1q7M4?p=39&spm_id_from=pageDriver)

1、构建springboot项目

2、打包应用

3、编写dockerfile

![image-20220125183323993](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220125183323993.png)

4、构建镜像

5、发布运行

> idea安装插件 搜索docker



## 

## 企业实战Docker Compose

### 简介

DockerFile build run 手动操作，单个容器！

微服务，100个微服务！依赖关系。

Docker Compose 来轻松高效管理容器！定义运行多个容器。

> 官方介绍

定义、运行多个容器。

YAML file 配置文件。

 single command 命令有哪些？

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see [the list of features](https://docs.docker.com/compose/#features).

所有的环境都可以使用 Compose

Compose works in all environments: production, staging, development, testing, as well as CI workflows. You can learn more about each case in [Common Use Cases](https://docs.docker.com/compose/#common-use-cases).

**三步骤：**

Using Compose is basically a three-step process:

1. Define your app’s environment with a `Dockerfile` so it can be reproduced anywhere.
   - DockeFile 保证我们的项目在任何地方可以运行。
2. Define the services that make up your app in `docker-compose.yml` so they can be run together in an isolated 
   environment.
   - service 什么是服务。
   - docker-compose.yml 这个文件怎么写！
3. Run `docker compose up` and the [Docker compose command](https://docs.docker.com/compose/cli-command/) starts and runs your entire app. You can alternatively run `docker-compose up` using the docker-compose binary.
   - 启动项目 

作用：批量容器编排。

> 狂神的理解

Compose 是 Docker 官方开源的项目。需要安装！

`Dockerfile` 让程序在任何的地方运行。web服务、redis、mysql、nginx...多个容器。

Compose

```shell
version: "3.9"  # optional since v1.27.0
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
      - logvolume01:/var/log
    links:
      - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

docker-compose up 100个服务

Compose ：重要的概念。

- 服务service，容器。应用。（web、redis、mysql...）
- 项目project。一组关联的容器。博客（web、mysql ）wp

### 安装

1、下载

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

官方下载非常慢，我们使用第三方的下载地址，可能会快点
cur1 -L https://get.daocloud.io/docker/compose/releases / download/1.25.5/docker-compose-"uname -s '- 'uname -m' > /usr/loca1/bin/docker-compose
```

![image-20220131094055139](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131094055139.png)

2、授权

```shell
 sudo chmod +x /usr/local/bin/docker-compose
 
 # 测试安装是否成功
 docker-compose version
```

### 体验

地址：https://docs.docker.com/compose/gettingstarted/

1、python 应用。计数器 redis

```shell
mkdir composetest
cd composetest

# 创建一个文件：app.py
# 编辑：app.py
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
    
# 编辑自动创建 requirements.txt
vim requirements.txt

# 编辑器内
flask
redis
```

第二步：创建一个dockerfile，应用打包为镜像

```shell
vim Dockerfile

# syntax=docker/dockerfile:1
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["python", "run"]
```

第三步：定义服务在 Compose file，（定义整个服务，需要的环境。web、redis）

```shell
vim docker-compose.yml

version: "3.9"
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```

第四步：用Compose 构建和运行你的app，启动compose 项目（docker-compose up)

```shell
docker-compose up
```

流程：

1、创建网络

2、执行 docker-compose.yml

3、启动服务

![image-20220131095910828](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131095910828.png)

默认规则：

![image-20220131100459574](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131100459574.png)

docker images

![image-20220131100536302](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131100536302.png)

默认的服务器名 文件名 _服务名 _1

多个服务器。集群。A、B _num 副本数量

服务Redis 服务 => 4个副本。

集群状态。服务都不可能只有一个运行实例。弹性、10 HA 高并发。

kubectl service 负载均衡

3、网络规则

```shell
# 查看网络
docker network ls

# 查看网络箱详细信息
docker network inspect NAME
```

![image-20220131101046632](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131101046632.png)

10个服务 ==> 项目 （项目中的内容都在通过网络下。域名访问）

![image-20220131101243324](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131101243324.png)

如果在同一个网络下，我们可以直接通过域名访问。

HA！

停止：docker-compose down / ctrl + c

![image-20220131101721631](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131101721631.png)

docker-compose

一起拿都是单个 docke run 启动容器。

docker-compose ：通过docker-compose 编写yaml配置文件、可以通过compose 一键启动所有服务，停止！

**Docker小结：**

1、Docker 镜像。run => 容器

2、 Docker File 构建镜像（服务打包）

3、 docker-compose 启动项目（编排、多个微服务/环境）

4、 Docker 网络



### yaml规则 

docker-compose.yaml 核心!

https://docs.docker.com/compose/compose-file/

```shell
# 有且只有三层!

version: ''	# 版本
service:	# 服务
	服务1：web
		# 服务配置 docker容器的配置
		images
		build
		network
		...
	服务2：redis
		...
	服务3：redis
		...
 # 其他配置 网络/卷、全局规则
 volumes:
 networks:
 configs:
```

多看多写。compose.yaml 配置！

1、官方文档

https://docs.docker.com/compose/compose-file/compose-file-v3/

2、开源项目 compose.yaml

redis、mysql、mq

### 开源项目（启动）

**博客**

下载程序、安装数据库、配置...

compose 应用。=>一键启动 

https://docs.docker.com/samples/wordpress/

1、下载项目（docker-compose.yaml)

2、如果需要文件 Dockerfile

3、文件准备齐全（直接一件启动）





```shell
# 后台启动
docker-compose up -d

# 停止
docker-compose down
```



掌握：docker基础，原理，网络，服务，集群，错误排查，日志。

liunx、docker、k8s 12k-20k



### 实战：





1、编写项目微服务，确保项目本地可以运行

2、编写接口地址：采用服务名替换服务器地址 redis、mysql

3、编写dockerfile 构建镜像

```shell
FROM java:8

COPY *.jar /app.jar

CMD ["--servcer.port=8080"]

EXPOSE 8080

ENTRYPOINT ["java","-jar","/app.jar"]
```

4、编写docker-compose.yaml 编排项目

```shell
version: '3.8'
service:
	chihiroapp
        build:.
        image:chihiroapp
        depends_on:
            - redis
		ports:
			- "8080:8080"
	redis
		image: "redis:alpine"
```

5、上传到服务器，docker-compose up

假设项目要重新部署打包

```shell
docke-compose up --build	# 重新构建
```

> 小结：
>
> 未来项目只要有 docker-compose 文件。按照这个规则，启动编排容器。
>
> 公司：docker-compose 直接启动
>
> 网上开源项目：docker-compose up 一键启动

**总结**：

**工程、服务、容器**

项目compose： 三层

- 工程 Porject
- 服务 服务
- 容器 容器运行实例！ docker k8s 容器 

## Docker Swarm

集群方式的部署

### 购买服务器

>4台阿里云服务、2核4g

到此，服务器购买完毕！1主，3从！



### 4台机器安装Docker

发送键到所有会话

![image-20220131112126621](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131112126621.png)

```shell
# 安装看前面 docker 单机教程
# 技巧：使用xshell直接同步操作，省时间
```

官网地址：https://docs.docker.com/engine/swarm/

### 工作模式

![image-20220131112932877](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131112932877.png)

**搭建集群**

```shell
# 查看网络
docker network ls
```

![image-20220131113047035](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131113047035.png)

```shell
# 查看 swarm 命令
docker swarm --help

# 初始化 swarm 节点
docker swarm init --help 
```

![image-20220131113127127](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131113127127.png)

```shell
# 初始化工作（主节点）节点 
docker swarm init --advertise-addr 主节点内网地址
```

![image-20220131115754208](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131115754208.png)

初始化节点`docker swarm init`

docker swarm join 加入一个节点！

```shell
# 获取令牌
# 创建一个管理者的 token 令牌 manager
docker swarm join-token manager
# 创建一个工作者的 token 令牌 worker
docker swarm join-token worker
```

![image-20220131120039932](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131120039932.png)

```shell
# 查看节点信息
docker node ls
```

![image-20220131120421473](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131120421473.png)

步骤：

1、生成主节点init

2、加入（管理者、worker）

目前是：双主双从！



### Raft协议

 双主双从：假设一个节点挂了！其他节点是否可用！

Raft协议：保证大多数节点存活才可用。只要>1，集群至少大于3台！

实验：

1、将 docker1 机器停止。模拟宕机！双主，另外一个主节点也不能使用了！**systemctl stop dorker** 命令模拟宕机。

![image-20220131121035561](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131121035561.png)

2、可用将其他节点离开

```shell
# 离开集群
docker swarm leave
```

![image-20220131121306254](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131121306254.png)

3、在创建一个管理者，要在管理者的机子中生成

```shell
# 创建一个管理者的 token 令牌 manager
docker swarm join-token manager

# work就是工作的，没办法用管理者的命令！
```

![image-20220131121526242](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131121526242.png)

> 小节：集群，可用！3个主节点。>1台管理节点存活！
>
> Reft协议：保证大多数节点存活，才可以使用。

### 服务

弹性、扩缩容！

以后告别docker run！

docker-compose up!	启动一个项目。单机

集群： swarm `docker service`

容器 => 服务！

容器 => 服务！=>副本！

redis服务 => 10个副本 （同时开启10个redis容器）

体验：创建服务、动态扩展服务、动态跟新服务、日志。

![image-20220131122830756](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131122830756.png)

灰度发布：金丝雀发布！

企业中很少停止网站发布：401！

```shell
# 容器启动！不具有扩缩容
docker run

# 服务！具有扩容，滚动更新！
docker service

# 创建一个服务
docker service create -p 8888:80 --name my-nginx nginx

# 查看一个服务 REPLICAS 显示副本数
docker service ps 服务名称
```

![image-20220131123311086](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131123311086.png)

 ```shell
 # 查看服务详细信息
 docker service inspect NAME
 
 # 动态扩缩容
 docker service update --replicas 3 NAME
 ```

服务在集群中任意的节点都可以访问。服务可以有多个副本动态扩缩容实现高可用！

```shell
# 动态扩缩容 和 update效果是一样的
docker service scale my-nginx=5
```

![image-20220131124507381](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131124507381.png)

```shell
# 移除服务
docker service rm my-nginx
```

docker swarm 其实并不难

只要会搭建集群、会启动服务、动态管理容器就可以了！

### 概念总结

**swarm**：集群的管理和编排。 docker 可以初始化一个swarm集群，其他节点可以加入。（管理、工作者）

**Node**： 就是一个docker节点。 多个节点就组成了一个网络集群。（管理、工作者）

**service**： 任务，可以在管理节点或者工作节点运行。 核心 ！ 用户访问！

**Task**：容器内的命令，细节任务

![image-20220131125107121](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131125107121.png)

**逻辑是不变的**

命令->管理->api->调度->工作节点（创建Task容器维护创建！）

> 服务副本与全局服务

![image-20220131125616766](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131125616766.png)

调整service 以什么方式运行

```shell
--mode string
service mode (replicated or global)(default "replicated")

docker service create --mode replicated --name mytom tomcat:7 默认的

docker service create --mode global --name haha alpine ping baidu.com

#场景？ 日志收集
每一个接地那有自己的日志收集器，过滤。把所有日志最终再传给日志中心
服务监控。状态性能。
```



## Docker Stack

docker-compose 单机部署项目！

Docker Stack 部署，集群部署！

```shell
# 单机
docker-compose up -d wordpress.yaml

# 集群
docker stack depoloy wordpress.yaml

# docker-compose 文件

```

## Docker Secret

安装！配置密码，证书！

![image-20220131133340424](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131133340424.png)



## Docker config

配置

![image-20220131133415303](E:\aChihiro\MD文件夹\开发区\存档文档\image-20220131133415303.png)

Docker compose Swarm！

学习方式：

网上找案例跑起来试试！查看命令帮助文档 --help，官网！

k8s docker go

## 扩展到K8S

**云原生时代** 大趋势！

Go语言！必须掌握！Java、Go！

Docker 是 Go开发的

k8s 也是Go开发的

Go是并发语言！

B语言 C语言的创始人。Unix创始人

云应用

电商网站

在线教育平台...

下载 => 配置！
