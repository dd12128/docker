# Docker的概述

## Docket为什么会出现？

一款产品:开发-上线两套环境!应用环境,应用配置!

开发--- 运维。问题:我在我的电脑上可以运行!版本更新,导致服务不可用!对于运维来说,考验就十分大?

环境配置是十分的麻烦,每-个机器都要部署环境(集群Redis、ES、 Hadoo....) ! 费时费力。

发布一个项目(jar+ ( Redis MySQL jdk ES ) ),项目能不能都带上环境安装打包!

之前在服务器配置-个应用的环境Redis MySQL jdk ES Hadoop , 配置超麻烦了,不能够跨平台。

Windows , 最后发布到Linux !

传统:开发jar，运维来做!

现在:开发打包部署上线，一套流程做完!.





java - apk -发布( 应用商店) ---张三使用apk ---安装即可用!

java -- jar (环境) --- 打包项目带上环境(镜像)---- ( Docker命库:商店) ---下载我们发布的镜像--直接运行即可!

Docker给以上的问题,提出了解决方案!

![image](image\image-20210725185551771.png)

Docker给以上的问题，提出了解决方案!



Docker的思想就来自于集装箱

JRE --多个应用(端口冲突) --- 原来都是交叉的!

隔离: Docker核心思想!打包装箱!每个箱子是互相隔离的。

Docker通过隔离机制，可以将服务器利用到极致!

## Docker的历史

2010年,几个搞IT的年轻人,就在美国成立了一家公司

Docker越来越多的人发现了docker的优点!火了, Docker 每个月都会更新一个版本!

2014年4月9日, Docker1.0发布!

Docker为什么这么火?十分的轻巧!

在容器技术出来之前,我们都是使用虚拟机技术!

虚拟机:在window中装一个 Vmware ,通过这个软件我们可以虚拟出来一台或者多台电脑 !笨重!

虚拟机也是属于虚拟化技术，Docker容器技术，也是一种虚拟化技术!

```shell
vm :   linux centos原生镜像(一个电脑! )隔离， 需要开启多个虚拟机! 几个G 几分钟
docker:隔离，镜像(最核心的环境4m + jdk + mysq1) 十分的小巧，运行镜像就可以了! 小巧!几个M KB秒级 启动!
```

到现在,所有开发人员都必须要会Docker !

> 聊聊Docker	

Docker是基于Go语开发的！开源项目！

官网地址：https://www.docker.com/

官网手册：https://docs.docker.com/

![image](image\image-20210725190335398.png)

 仓库地址：https://hub.docker.com/

## Docker能干嘛

> 之前的虚拟机技术！

![image](image\image-20210725191528635.png)

**虚拟机技术缺点:**

1、资源占用十分多

2、冗余步骤多

3、启动很慢!

> 容器化技术！	

容器化技术不是模拟的一个完整的操作系统

![image](image\image-20210725192003179.png)

比较Docker和虚拟机技术的不同:

​	● 传统虚拟机,虚拟出一条硬件,运行一个完整的操作系统,然后在这个系统上安装和运行软件

​    ● 容器内的应用直接运行在宿主机的内容,容器是没有自己的内核的,也没有虚拟我们的硬件,所以就轻便了

​    ● 每个容器间是互相隔离,每个容器内都有一个属于自己的文件系统,互不影响。



> ​	DevOps (开发、运维)

**应用更快速的交付和部署**

传统: -堆帮助文档,安装程序

Docker :打包镜像发步测试,一键运行

**更便捷的升级和扩缩容**

使用了Docker之后,我们部署应用就和搭积木一样!

**更简单的系统运维**

在容器化之后,我们的开发,测试环境都是高度-致的。

**更高效的计算资源利用:**

Docker是内核级别的虚拟化,可以再一个物理机上可以运行很多的容器实例!服务器的性能可以被压榨到极致。

# Docker安装

## Docker基本组成

![image](image\image-20210725192652706.png)

**镜像 (image)：**

docker镜像就好比是一个模板 ,可以通过这个模板来创建容器服务, tomcat镜像===> run==> tomcat01容器( 提供服务器),

通过这个镜像可以创建多个容器(最终服务运行或者项目运行就是在容器中的)。

**容器 (container):**

Docker利用容器技术,独立运行-个或者一个组应用,通过镜像来创建的。

启动,停止,删除,基本命令!

目前就可以把这个容器理解为就是一个简易的linux系统

**仓库 (repository):**

仓库就是存放镜像的地方!

仓库分为公有仓库和私有仓库!

Docker Hub (默认是国外的)

阿里云...都有容器服务器(配置镜像加速! )

## 安装Docker

> 准备环境	

1、需要会一点点的Linux的基础

2、CentOS 7 

3、我们使用Xshell 连接远程服务器进行操作!

> 环境查看

```shell
#系统内核是 3.10 以上的
[root@yjy100 /]# uname -r
3.10.0-1127.el7.x86_64
```

```shell
#系统版本
[root@yjy100 /]# cat /etc/os-release
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```

> 安装

帮助文档：

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
                  
# 2、安装需要的安装包
  yum install -y yum-utils
# 3、设置镜像仓库
 yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo # 默认是国外的
    
    yum-config-manager \
    --add-repo \
   https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo    # 建议使用阿里云或者其他国内镜像
# 、更新yum软件包索引    
 yum makecache fast

# 4、安装dokcer相关的额 docker-ce 社区    ee企业版
  yum install docker-ce docker-ce-cli containerd.io

# 5、启动docker  
systemctl start docker
# 开机自启动
systemctl enable docker
# 6、使用docker version 验证安装成功
[root@yjy100 /]#  docker version
Client: Docker Engine - Community
 Version:           20.10.7
 API version:       1.41
 Go version:        go1.13.15
 Git commit:        f0df350
 Built:             Wed Jun  2 11:58:10 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.7
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       b0f5bc3
  Built:            Wed Jun  2 11:56:35 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.8
  GitCommit:        7eba5930496d9bbe375fdf71603e610ad737d2b2
 runc:
  Version:          1.0.0
  GitCommit:        v1.0.0-0-g84113ee
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
 # 7、hello-world
 docker run hello-world
```

![image](image\image-20210725195318014.png)

```shell
# 8、查看一下下载的hello-world 镜像
[root@yjy100 /]# docker images
REPOSITORY            TAG       IMAGE ID       CREATED        SIZE
hello-world           latest    d1165f221234   4 months ago   13.3kB
```

## 通过脚本进行安装docker

```shell
# https://get.docker.com/  脚本下载的地址
# curl -fsSL get.docker.com -o get-docker.sh  下载到本地
# sh get-docker.sh	运行脚本
```



了解：卸载Docker

```shell
# 1、卸载依赖
yum remove docker-ce docker-ce-cli containerd. io 

#2、删除资源
rm -rf /var/1ib/docker

# /var/1ib/docker  doqker的默认工作路径!
```

## 阿里云镜像加速

1、登录阿里云找到容器服务

![image](image\image-20210725200459663.png)

2、找到镜像加速地址

![image](image\image-20210725200620246.png)

3、配置使用

```shell
 mkdir -p /etc/docker
 vim /etc/docker/daemon.json
daemon.json文件
{
  "registry-mirrors": ["https://ovvphjcn.mirror.aliyuncs.com"]
}

systemctl daemon-reload 
systemctl restart docker
```

## 回顾HelloWorld流程

![image](image\image-20210725195318014.png)

![image](image\image-20210725201254366.png)

## 底层原理

**Docker是什么工作的?**

Docker是-个Client - Server结构的系统, Docker的守护进程运行在主机上。通过Socket从客户端访问 !

DockerServer接收到Docker-Client的指令,就会执行这个命令!

![image](image\image-20210725201417461.png)

**Docker为什么比VM快?**

1、Docker有 着比虚拟机更少的抽象层。

2、docker 利用的是宿主机的内核, vm需要是Guest OS。

![image](image\image-20210725201530424.png)

所以说,新建一个容器的时候 , docker不需要想虚拟机-样重新加载一个操作系统内核 ,避免引导。虚拟机是加载GuestOS ,分

钟级别的,而docker是利用宿主机的操作系统吗,省略了这个复杂的过程,秒级 !

![image](image\image-20210725201937230.png)

# Docker的常用命令

## 帮助命令

```shell
docker version     #显示docker版本信息
docker info		   #显示docker的系统信息，包括镜像和容器的数量
docker 命令 --help  #帮助命令
docker container   #后面可以更所有的命令 
	比如：docker container run  # 运行一个容器
		 docker container ls # 显示正在运行的容器
# 注意：docker container run 等价于 docker run 可以不加container
```

## 镜像命令

**docker images**  查看所有本地的主机上的镜像

```shell
[root@yjy100 ~]# docker images
REPOSITORY   TAG        IMAGE ID       CREATED        SIZE
centos       latest    300e315adb2f   7 months ago   209MB

#解释
REPOSITORY 镜像的仓库源
TAG        镜像的标签
IMAGE ID   镜像的id
CREATED	   镜像的创建时间
SIZE       镜像的大小

#可选项
-a, --all  			# 列出所有的镜像
-q, --quiet         # 只显示镜像的id
```

**docker search**  搜索镜像

```shell
[root@yjy100 ~]# docker search mysql
NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   11168     [OK]       
mariadb                           MariaDB Server is a high performing open sou…   4238      [OK]       

# 可选项，通过搜索来过滤
-- filter=STARS=3000   # 搜索出来的镜像就是STARS大于3000的
[root@yjy100 ~]# docker search mysql --filter=STARS=3000
NAME      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mysql     MySQL is a widely used, open-source relation…   11168     [OK]       
mariadb   MariaDB Server is a high performing open sou…   4238      [OK]       

```

**docker pull**  下载镜像

```shell
# 下载镜像  docker pull 镜像名 [:tag]
[root@yjy100 ~]# docker pull mysql
Using default tag: latest  # 如果不写 tag，默认就是 latest
latest: Pulling from library/mysql
33847f680f63: Pull complete  # 分层下载，docker image的核心 联合系统文件
5cb67864e624: Pull complete 
1a2b594783f5: Pull complete 
b30e406dd925: Pull complete 
48901e306e4c: Pull complete 
603d2b7147fd: Pull complete 
802aa684c1c4: Pull complete 
715d3c143a06: Pull complete 
6978e1b7a511: Pull complete 
f0d78b0ac1be: Pull complete 
35a94d251ed1: Pull complete 
36f75719b1a9: Pull complete 
Digest: sha256:8b928a5117cf5c2238c7a09cd28c2e801ac98f91c3f8203a8938ae51f14700fd  # 签名
Status: Downloaded newer image for mysql:latest # 真实地址
docker.io/library/mysql:latest

#等价于它
docker pull mysql
docker pull io/library/mysql:latest	

# 指定版本下载
[root@yjy100 ~]# docker pull mysql:5.7
5.7: Pulling from library/mysql
33847f680f63: Already exists 
5cb67864e624: Already exists 
1a2b594783f5: Already exists 
b30e406dd925: Already exists 
48901e306e4c: Already exists 
603d2b7147fd: Already exists 
802aa684c1c4: Already exists 
5b5a19178915: Pull complete 
f9ce7411c6e4: Pull complete 
f51f6977d9b2: Pull complete 
aeb6b16ce012: Pull complete 
Digest: sha256:be70d18aedc37927293e7947c8de41ae6490ecd4c79df1db40d1b5b5af7d9596
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7
```

**docker rmi**  删除镜像！

```shell
[root@yjy100 ~]# docker rmi -f 镜像id  # 删除指定的镜像
Untagged: mysql:5.7
Untagged: mysql@sha256:be70d18aedc37927293e7947c8de41ae6490ecd4c79df1db40d1b5b5af7d9596
Deleted: sha256:8cf6250709314f2fcd2669e8643f5d3bdebfe715bddb63990c8c96e5d261d6fc
Deleted: sha256:452fe6896278c26338d547f8d1092011d923785247c46629b374d3477fe28c84
Deleted: sha256:bd40bf60af5d06e6b93eaf5a648393d97f70998faa3bfa1b85af55b5a270cb35
Deleted: sha256:c43e9e7d1e833650e0ed54be969d6410efa4e7fa6e27a236a44a2b97e412ee93
Deleted: sha256:70f18560bbf492ddb2eadbc511c58c4d01e51e8f5af237e3dbb319632f16335b
# docker rmi -f 镜像id  # 删除指定的镜像
# docker rmi -f 镜像id 镜像id 镜像id 镜像id  # 删除多个镜像
# docker rmi -f $(docker images -aq) # 删除全部镜像
# 如果镜像的id名称相同的话，通过
# docker rmi -f 镜像名:tag
```

**docker tag 给镜像打标签**

```shell
[root@dongdong html]# docker tag 4037a5562b03 docker.io/dongdongaini/nginx:v1.12.2
# 语法：docker tag 镜像id 远程仓库地址/注册仓库id/名字:tag
[root@dongdong html]# docker images
REPOSITORY           TAG       IMAGE ID       CREATED        SIZE
dongdongaini/nginx   curl      0353445c85ca   42 hours ago   179MB
mysql                latest    ecac195d15af   2 weeks ago    516MB
dongdongaini/nginx   v1.12.2   4037a5562b03   3 years ago    108MB
nginx                1.12.2    4037a5562b03   3 years ago    108MB
```

## 容器命令

**说明：我们有了镜像才可以创建容器**

```shell
docker pull centos  # 拉取centos镜像文件
```

**容器并启动**

```shell
docker run [可选参数] image

# 参数说明
--name="Name"   容器的名字 用来区分容器
-d （detached）  后台方式运行，非交互式

--rm			用完即删除
-it	            使用交互方式运行，进入容器查看内容
-p              指定容器的端口 -p 8080:8080
	-p ip:主机端口：容器端口
	-p 主机（容器外）端口:容器内端口  (常用)
	-p 容器端口
-P              随机指定主机端口（容器外）



# 测试，并启动进入容器
[root@yjy100 ~]# docker run -it centos /bin/bash
[root@0db58e7bc7f5 /]# ls  # 查看容器内部
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

# 从容器中返回主机
[root@d0e27684d521 /]# exit
exit
[root@yjy100 /]# ls
bin  boot  dev  etc  home  lib  lib64  lost+found  media  mnt  newdisk  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  www
```

**attached和detached模式**

```shell
docker run nginx # 在windows下的命令行 按住Ctrl + c就不会停止nginx服务  这就是attached模式
docker run nginx # 在Linux下的命令行  按住Ctrl + c就会停止nginx服务
# 如果不想使用attached模式的化可以 用-d(detached)命令 如：docker run -d nginx  就是进入到了datached模式
# 如果想从datached模式切换到attached模式可以使用 docker attach 容器id 如果输入Ctrl + c就会把当前正在运行的容器给停掉
```

**列出所有的运行的容器**

```shell
# docker ps 
	# 列出当前正在运行的容器
-a	# 列出当前正在运行的容器+带出历史运行过的容器
-n=?	# 显示最近创建的容器
-q   # 只显示容器的id
[root@yjy100 /]# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED             STATUS             PORTS     NAMES
25c78354b268   centos    "/bin/bash"   About an hour ago   Up About an hour             loving_shirley

[root@yjy100 /]# docker ps -a
CONTAINER ID   IMAGE          COMMAND       CREATED             STATUS                           PORTS     NAMES
d0e27684d521   centos         "/bin/bash"   6 minutes ago       Exited (0) 6 minutes ago                   elated_chaum
f3fa7f2dcacb   centos         "/bin/bash"   8 minutes ago       Exited (0) 8 minutes ago                   wizardly_kirch
0db58e7bc7f5   centos         "/bin/bash"   10 minutes ago      Exited (0) 8 minutes ago                   inspiring_wing
c7fba1ff4ea4   centos         "/bin/bash"   About an hour ago   Exited (127) About an hour ago             angry_saha
25c78354b268   centos         "/bin/bash"   About an hour ago   Up About an hour                           loving_shirley
fb4c80015bc2   centos         "/bin/bash"   About an hour ago   Exited (0) About an hour ago               gallant_elgamal
30059b8eed31   d1165f221234   "/hello"      About an hour ago   Exited (0) About an hour ago               zealous_snyder

[root@yjy100 /]# docker ps -aq
d0e27684d521
f3fa7f2dcacb
0db58e7bc7f5
c7fba1ff4ea4
25c78354b268
fb4c80015bc2
30059b8eed31
```

**退出容器**

```shell
exit  # 直接容器停止并退出
Ctrl + p + q  # 容器不停止退出
```

**删除容器**

```shell
docker rm 容器id                        # 删除指定容器，不能删除正在执行的容器 ，如果要强制删除 rm -f
docker rm -f $(docker ps -aq)          #删除所有的容器
docker ps -a -q | xargs docker rm      # 删除所有的容器
```

启动和停止容器的操作

```shell
docker start 容器id      # 启动容器
docker restart 容器id    # 重启容器
docker stop 容器id       # 停止当前正在运行的容器
docker kill 容器id       # 强制停止当前容器
```

**load与save**

```shell
docker load -i 文件.tar   #docker load用来载入镜像包
docker save 镜像 > new_centos.tar #docker save保存的是镜像（image）
```

## 常用其他命令

**后台启动容器**

```shell
#  命令 docker run -d 镜像名！
[root@yjy100 /]# docker run -d centos

#问题docker ps，发现centos停止了

#坑: docker 容器使用后台运行，就必须要有一个前台进程，docker发现没有应用，就会自动停止
#nginx，容器启动后，发现自己没有提供服务，就会立刻停止，就是没有程序了
```

**查看日志**

```shell
docker logs -f -t --tail 

#写一段shell脚本呢
"while true;do echo '你好';sleep 2;done;"

docker run -d centos /bin/sh -c "while true;do echo '你好';sleep 2;done;"

#显示日志
-tf  
-- tail number  #显示日志的条数
[root@yjy100 /]# docker logs -tf --tail 10 ab768bfc3982
2021-07-25T08:25:32.234855854Z 你好
2021-07-25T08:25:34.237170167Z 你好
2021-07-25T08:25:36.240902938Z 你好
2021-07-25T08:25:38.242297413Z 你好
2021-07-25T08:25:40.243872993Z 你好
2021-07-25T08:25:42.247716855Z 你好
2021-07-25T08:25:44.251531774Z 你好
2021-07-25T08:25:46.253234499Z 你好
2021-07-25T08:25:48.257269584Z 你好
2021-07-25T08:25:50.259898636Z 你好
2021-07-25T08:25:52.264924375Z 你好
2021-07-25T08:25:54.268967514Z 你好
2021-07-25T08:25:56.273349847Z 你好
2021-07-25T08:25:58.274902895Z 你好
2021-07-25T08:26:00.278531561Z 你好
2021-07-25T08:26:02.281345134Z 你好

```

**查看容器中的进程信息ps**

```shell
# 命令 docker top 容器id
[root@yjy100 /]# docker top 25c78354b268
UID                 PID                 PPID                C                   STIME               TTY     
root                19455               19436               0                   14:50               pts/0              

```

**查看镜像的源数据**

```shell
# 命令 docker inspect 容器id
[root@yjy100 /]#  docker inspect 25c78354b268
[
    {
        "Id": "25c78354b268ae1a4bb63e63be48ab09775080be62ca5021699a574b089051d2",
        "Created": "2021-07-25T06:50:05.754512519Z",
        "Path": "/bin/bash",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 19455,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2021-07-25T06:50:06.099284345Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:300e315adb2f96afe5f0b2780b87f28ae95231fe3bdd1e16b9ba606307728f55",
        "ResolvConfPath": "/var/lib/docker/containers/25c78354b268ae1a4bb63e63be48ab09775080be62ca5021699a574b089051d2/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/25c78354b268ae1a4bb63e63be48ab09775080be62ca5021699a574b089051d2/hostname",
        "HostsPath": "/var/lib/docker/containers/25c78354b268ae1a4bb63e63be48ab09775080be62ca5021699a574b089051d2/hosts",
        "LogPath": "/var/lib/docker/containers/25c78354b268ae1a4bb63e63be48ab09775080be62ca5021699a574b089051d2/25c78354b268ae1a4bb63e63be48ab09775080be62ca5021699a574b089051d2-json.log",
        "Name": "/loving_shirley",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/da9d431969c7d91c941a51eac1ed300c4a248e05867c292d040db74b9745875a-init/diff:/var/lib/docker/overlay2/9f2d043564b8d24b864d2708a0ab1451d9e0bbebd1cdcaf2415d6f06239989ad/diff",
                "MergedDir": "/var/lib/docker/overlay2/da9d431969c7d91c941a51eac1ed300c4a248e05867c292d040db74b9745875a/merged",
                "UpperDir": "/var/lib/docker/overlay2/da9d431969c7d91c941a51eac1ed300c4a248e05867c292d040db74b9745875a/diff",
                "WorkDir": "/var/lib/docker/overlay2/da9d431969c7d91c941a51eac1ed300c4a248e05867c292d040db74b9745875a/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "25c78354b268",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20201204",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "8a8a134ccee623581281044e6fe37ed2417a7d993fd92e73f8ddfffc093fc1e5",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/8a8a134ccee6",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "a3f6862b2649ddb90a9481608c2382dc839fb1f09a63467e9dd0bea802711a27",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "430467e28c48d641acde8b3ba7b3c65247b653b3203f7968d2824cff3946ff83",
                    "EndpointID": "a3f6862b2649ddb90a9481608c2382dc839fb1f09a63467e9dd0bea802711a27",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
```

**进入当前正在运行的容器**

```shell
# 我们通常容器都是使用后台方式运行的，需要进入容器，修改一些配置

# 命令
docker exec -it 容器id bashShell

[root@yjy100 /]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
ab768bfc3982   centos    "/bin/sh -c 'while t…"   11 minutes ago   Up 11 minutes             competent_burnell
25c78354b268   centos    "/bin/bash"              2 hours ago      Up 2 hours                loving_shirley
[root@yjy100 /]# docker exec -it 25c78354b268 /bin/bash/
OCI runtime exec failed: exec failed: container_linux.go:380: starting container process caused: exec: "/bin/bash/": stat /bin/bash/: not a directory: unknown: Are you trying to mount a directory onto a file (or vice-versa)? Check if the specified host path exists and is the expected type
[root@yjy100 /]# docker exec -it 25c78354b268 /bin/bash
[root@25c78354b268 /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@25c78354b268 /]# ps -ef
UID         PID   PPID  C STIME TTY          TIME CMD
root          1      0  0 06:50 pts/0    00:00:00 /bin/bash
root         22      0  0 08:35 pts/1    00:00:00 /bin/bash
# 方式二
docker attach 容器id
[root@yjy100 /]# docker attach 25c78354b268
运行正在执行的代码 --->


# docker exec   进入容器后开启一个新的终端，可以在里面操作(常用)
# docker attach  进入容器正在执行的终端，不会启动新的进程
```

**从容器内拷贝文件到主机上**

```shell
# docker cp 容器id:容器内路径  目录的主机路径

# 进入docker容器内部
[root@yjy100 home]# docker attach 824699ce176c 
[root@824699ce176c /]# cd /home
[root@824699ce176c home]# ls
# 在容器内部新建一个文件
[root@824699ce176c home]# touch hello.java
[root@824699ce176c home]# exit
exit
[root@yjy100 home]# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
ab768bfc3982   centos    "/bin/sh -c 'while t…"   24 minutes ago   Up 24 minutes             competent_burnell
# 查看历史容器
[root@yjy100 home]# docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS                      PORTS     NAMES
824699ce176c   centos         "/bin/bash"              3 minutes ago    Exited (0) 36 seconds ago             gracious_sanderson
ab768bfc3982   centos         "/bin/sh -c 'while t…"   25 minutes ago   Up 25 minutes                         competent_burnell
8efdcf27de14   centos         "/bin/bash"              36 minutes ago   Exited (0) 36 minutes ago             musing_hopper
d0e27684d521   centos         "/bin/bash"              53 minutes ago   Exited (0) 53 minutes ago             elated_chaum
f3fa7f2dcacb   centos         "/bin/bash"              55 minutes ago   Exited (0) 55 minutes ago             wizardly_kirch
0db58e7bc7f5   centos         "/bin/bash"              57 minutes ago   Exited (0) 55 minutes ago             inspiring_wing
c7fba1ff4ea4   centos         "/bin/bash"              2 hours ago      Exited (127) 2 hours ago              angry_saha
25c78354b268   centos         "/bin/bash"              2 hours ago      Exited (0) 8 minutes ago              loving_shirley
fb4c80015bc2   centos         "/bin/bash"              2 hours ago      Exited (0) 2 hours ago                gallant_elgamal
30059b8eed31   d1165f221234   "/hello"                 2 hours ago      Exited (0) 2 hours ago                zealous_snyder
# 将文件拷贝到主机上
[root@yjy100 home]# docker cp 824699ce176c:/home/hello.java /home
[root@yjy100 home]# ls
abc.txt  fox          hello.java  jack      jeryy  mycal          myhome.zip  pc.tar.gz  tom  xq
cat.txt  Hello.class  Hello.java  java.txt  mucal  myhome.tar.gz  my.sh       pig.txt    xh   yjy

```

## 可视化

什么是 portainer ？

Docker图形化界面管理工具！提供一个后台模板我们操作！

```shel
docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v /home/docker/portainer:/data --name portainer --restart=always portainer/portainer
```

访问：http:// 本地ip :端口号

# Docker镜像

## 镜像是什么

镜像是一种轻量级、 可执行的独立软件包,用来打包软件运行环境和基于运行环境开发的软件,它包含运行某个软件所需的所有内

容,包括代码、运行时、库、环境变量和配置文件。

所有的应用,直接打包docker镜像, 就可以直接跑起来!

如何得到镜像:

​	● 从远程仓库下载

​	● 朋友拷贝给你.

​	● 自己制作一个镜像DockerFile.

## Docker镜像加载原理

> **UnionFS ( 联合文件系统)**

UnionFS (联合文件系统) : Union文件系统( UnionFS)是-种分层、 轻量级并且高性能的文件系统,它支持对文件系统的修改

作为一次提交来-层层的叠加,同时可以将不同目录挂载到同一个虚拟文件系统下(unite several directories into a single virtual

filesystem)。Union 文件系统是Docker镜像的基础。镜像可以通过分层来进行继承,基于基础镜像(没有父镜像)，可以制作各种具体的应用镜像。

特性:一次同时加载多个文件系统,但从外面看起来,只能看到一个文件系统,联合加载会把各层文件系统叠加起来,这样最终的文件系统会包含所有底层的文件和目录

> **Docker镜像加载原理**	

docker的镜像实际上由一层一层的文件系统组成,这种层级的文件系统UnionFS。

bootfs(boot file system)主要包含bootloader和kernel, bootloader主要是弓|导加载kernel, Linux刚启动时会加载bootfs文件系

统,在Docker镜像的最底层是bootfs。这一层与我们典型的Linux/Unix系统是一样的 ,包含boo加载器和内核。当bootfs加载完成

之后整个内核就都在内存中了,此时内存的使用权已由bootfs转交给内核,此时系统也会卸载bootfs.

rootfs (root file system) , 在bootfs之上。包含的就是典型Linux系统中的/dev, /proc, /bin, /etc等标准目录和文件。rootfs就是

各种不同的操作系统发行版,比如Ubuntu , Centos等等。

<img src="image\image-20210725203216717.png" alt="image-20210725203216717" style="zoom:150%;" />

平时我们安装进虚拟机的CentOS都是好几个G ,为什么Docker这里才200M ?

<img src="image\image-20210725203332970.png" alt="image-20210725203332970" style="zoom: 150%;" />

对于一个精简的OS , rootfs 可以很小,只需要包含最基本的命令,工具和程序库就可以了,因为底层直接用Host的kernel ,自己只

需要提供rootfs就可以了。由此可见对于不同的linux发行版, bootfs基本是一致的, rootfs会有差别,因此不同的发行版可以公用bootfs.

## 分层理解

> 分层的镜像

思考:为什么Docker镜像要采用这种分层的结构呢?

最大的好处,我觉得莫过于是资源共享了! 比如有多个镜像都从相同的Base镜像构建而来,那么宿主机只需在磁盘上保留一份base

镜像,同时内存中也只需要加载一份base镜像 ,这样就可以为所有的容器服务了,且镜像的每- 层都可以被共享。

查看镜像分层的方式可以通过docker image inspect命令!

**理解**

所有的Docker镜像都起始于一个基础镜像层,当进行修改或增加新的内容时,就会在当前镜像层之上,创建新的镜像层。

举一个简单的例子,假如基于Ubuntu Linux 16.04 创建一个 新的镜像,这就是新镜像的第一层;如果在该镜像中添加Python包，

就会在基础镜像层之上创建第二个镜像层;如果继续添加一个安全补丁,就会创建第三个镜像层。

该镜像当前已经包含3个镜像层,如下图所示(这只是一个用于演示的很简单的例子 )。

![image](image\image-20210725203812163.png)

在添加额外的镜像层的同时,镜像始终保持是当前所有镜像的组合,理解这一点非常重要。下图中举了一个简单的例子,每个镜像

层包含3个文件,而镜像包含了来自两个镜像层的6个文件。

![image](image\image-20210725203909860.png)

上图中的镜像层跟之前图中的略有区别,主要目的是便于展示文件。

下图中展示了-个稍微复杂的三层镜像,在外部看来整个镜像只有6个文件,这是因为最上层中的文件7是文件5的一个更新版本。

![image](image\image-20210725203952072.png)

这种情况下，上层镜像层中的文件覆盖了底层镜像层中的文件。这样就使得文件的更新版本作为一个新镜像层添加到镜像当中。

Docker通过存储引擎(新版本采用快照机制)的方式来实现镜像层堆栈,并保证多镜像层对外展示为统一的文件系统。

Linux.上可用的存储弓|擎有AUFS、Overlay2、 Device Mapper、Btrfs 以及ZFS.顾名思义, 每种存储弓|擎都基于Linux中对应的

文件系统或者块设备技术,诅每种存储引擎都有其独有的性能特点。

Docker在Windows.上仅支持windowsfilter -种存储引擎,该引擎基于NTFS文件系统之上实现了分层和CoW[1]。

下图展示了与系统显示相同的三层镜像。所有镜像层堆叠并合并,对外提供统一的视图。

![image](image\image-20210725204131206.png)

> **特点**

Docker镜像都是只读的,当容器启动时, -个新的可写层被加载到镜像的顶部 !

这一层就是我们通常说的容器层,容器之下的都叫镜像层 !

**commit 镜像**

```shell
docker commit 提交容器成为一个新的副本

docker commit -m="提交的描述信息" -a="作者" 容器id  目标镜像名：[TAG]
```

**测试**

```shell
# 1、启动一个默认的tomcat

# 2、发现这个默认的tomcat是没有webapps应用， 镜像的原因，官方的镜像默认webapps下面是没有文件的!

# 3、我自己拷贝进去了基本的文件!

# 4、将我们操作过的容器通过commit提交为一个镜像!我们以后就使用我们修改过的镜像
```

![image](image\image-20210725181212671.png)

# 容器数据卷

## 什么是容器数据卷

**docker的理念回顾**

将应用和环境打包成一个镜像！

数据？如果数据都在容器中，那么我们容器删除，数据就会丢失！==需求：数据可以持久化==

Mysql，容器删了，删库跑路 ==需求：Mysql数据可以存储在本地==

容器之间可以有一个数共享的技术！Docker容器中产生的数据。同步到本地！

这就是容器卷技术！目录挂载，将我们容器内的目录，挂载到Linux上面！

**总结：容器的持久化和同步操作！容器间也可以数据共享！**

## 使用数据卷

> 方式一：直接使用命令来挂载 -v	

```shell
docker run -it -v 主机（容器外）目录:容器内目录

# 测试 
[root@yjy100 home]# docker run -it -v /home/text:/home centos /bin/bash

# 启动起来我们可以通过 docker inspect 容器id
```

![image](image\image-20210725224119581.png)

测试文件的同步

![image](image\image-20210725224536120.png)

再来测试！

1、停止容器

2、服务器上修改文件

3、启动容器

4、容器内的数据依旧是可以同步的！

![image](image\image-20210725225337289.png)

**好处：我们以后修改只需要在本地修改即可，容器内会自动同步！**



## 传递环境变量

```shell
docker run -e 环境变量key=环境变量value


[root@dongdong ~]# docker run --rm -e E_os=123457 nginx:1.12.2 printenv
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=d7505db4f036
E_os=123457
NGINX_VERSION=1.12.2-1~stretch
NJS_VERSION=1.12.2.0.1.14-1~stretch
HOME=/root
```

## 容器内安装软件（工具）

```shell
yum/apt-get/apt等

tee /etc/apt/sources.list << EOF
deb http://mirrors.163.com/debian/ jessie main non-free contrib
deb http://mirrors.163.com/debian/ jessie-updates main non-free contrib
EOF
apt-get update
```



## 具民和匿名挂载

```shell
# 匿名挂载
-v 容器内路径！
-P 随机分配端口
docker run -d -P --name nginx01 -v/ect/nginx nginx

# 查看所有的 volume 的情况
[root@yjy100 /]# docker volume ls
DRIVER    VOLUME NAME
local     6b8732509c725932efc92102e0fd010f382152a3a46ea8af7e6d26e3013988cc

# 这里发现,这种就是匿名挂载，我们在 -v 只写了容器内的路径，没有写容器外的路径！

#具民挂载
root@yjy100 /]# docker run -d -P --name nginx03 -v yujiayi-x:/etx/nginx nginx
local     yujiayi-x

# 通过 -v 卷名:容器内路径
# 查看一下卷
```

![image](image\image-20210725231631010.png)

所有的docker容器内的卷，没有指定目录的情况下都是在`/var/lib/docker/volumes/xxxx/_data  `

我们通过具名挂载可以方便的找到我们的-个卷，大多数情况在使用的`具民挂载`

```shell
#如何确定是具名挂载还是匿名挂载，还是指定路径挂载!
-v 容器内路径                #匿名挂载
-V 卷名:容器内路径            #具名挂载
-V /宿主机路径:容器内路径     #指定路径挂载!
```

扩展

```shell
#通过-V容器内路径: ro rw改变读写权限
ro readonly #只读
rw readwrite # 可读可写

#一旦这个了设置了容器权限，容器对我们挂载出来的内容就有限定了!
docker run -d -P --name nginx02 -v yujiayi-x:/etc/nginx:ro nginx
docker run -d -P --name nginx02 -v yujiayi-x:/etc/nginx:rw nginx

# ro只要看到ro就说明这个路径只能通过宿主机来操作，容器内部是无法操作!
```

## 初识DockerFile

Dockerfile就是用来构建docker镜像的构建文件!命令脚本!先体验一下 !

通过这个脚本可以生成镜像,镜像是一-层- 层的,脚本一个个的命令,每个命令都是-一层 !

```shell
# 创建一个dockerfile文件，名字可以随意取 建议Dockerfile
# 文件中的内容 指令(大写)   参数

FROM centos

VOLUME ["voluem01","voluem02"]    # 匿名挂载

CMD echo "------end------"
CMD /bin/bash

# 这里的每一个命令，就是镜像的一层
```

![image](image\image-20210726133007096.png)

```shell
#启动自己的容器
```

![image](image\image-20210729022625906.png)

这个卷和外部一定有一个同步的目录  



docker inspect 容器id

查看一下文件是否同步

![image](image\image-20210726135453413.png)



测试一下刚才文件是否同步

![image](image\image-20210726135614018.png)

假如构建镜像时候没有挂载卷，需要手动挂载 -v卷名：容器内路径！

## 数据卷容器

多个mysql同步数据！

![image](image\image-20210726140100310.png)

```shell
# 启动3个容器，
```

![image](image\image-20210726140946214.png)

![image](image\image-20210726141546813.png)

![image](image\image-20210726141803696.png) 

![image](image\image-20210726142116461.png)

**结论：**

容器之间配置信息的传递，数据卷容器的生命周期一直持续到没有人使用为止  通过 --volumes-from

但是一旦你持久化到本地，这个时候，本地的数据是不会被删除的 

# DockerFile

## DockerFile介绍

dockerfile 是用来构建docker镜像的文件！命令参数脚本！

构建步骤：

1、编写一个dockerfile 文件

2、docker build构建成为一个镜像

3、docker run运行镜像

4、docker push发布镜像( DockerHub、阿里云镜像仓库! )

## DockerFile构建过程

**基础知识:**

1、每个保留关键字(指令)都是必须是大写字母，命名用小写，（**尽管指令大小写不敏感，但是还是强烈建议指令用大写**）

2、执行从上到下顺序执行

3、#示注释

4、每一个指令都会创建提交一个新的镜像层, 并提交 !

![image](image\image-20210726145017031.png)

dockerfile是面向开发的,我们以后要发布项目,做镜像,就需要编写dockerfile文件,这个文件十分简单 !

DockerFile :构建文件,义了一切的步骤,源代码

Dockerlmages :过DockerFile构建生成的镜像,最终发布和运行的产品 !

Docker容器:容器就是镜像运行起来提供服务器

## **DockerFile的指令**

```shell
FROM                # 基础镜像 ，一切从这里开始搭建
MAINTAINER          # 镜像是谁写的，姓名+邮箱
RUN					# 镜像构建的时候需要运行的命令
ADD					# 步骤: tomcat镜像， 这个tomcat压缩包!添加内容
USER				# 定义你使用哪个用户
WORKDIR				# 镜像的工作目录
VOL UME				# 挂载的目录
EXPOSE				# 保留端口配置
CMD					# 指定这个容器启动的时候要运行的命令,只有最后一个会生效，可被替代
ENTRYPOINT			# 指定这个容器启动的时候要运行的命令，可以追加命令
ONBUILD				# 当构建一个被继承DockerFile 这个时候就会运行ONBUILD 的指令。触发指令。
COPY				# 类似ADD，将我们文件拷贝到镜像中
ENV					# 构建的时候设置环境变量！
```

## 实战测试

Docker Hub 中 99%的镜像都是从基础镜像过来的 FROM scratch，然后配置需要软件和配置来进行的构建

> 创建一个自己的centos

```shell
# 编写Dockerfile文件
[root@yjy100 dockerfile]# cat mydockerfile-centos 
FROM centos
MAINTAINER yujiayi<1302525942@qq.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools

EXPOSE 80

CMD echo $MYPATH
CMD echo "-----end-----"
CMD /bin/bash
# 通过这个文件来构建镜像
#命令docker build -f dockerfile 文件路径 -t 镜像名: [tag]
# 注意：文件路径.表示在当前目录构建镜像
# 注意：如果编写dockerfile文件开头是以大写D开头的在构建镜像的时候就不需要加-f 这个参数官方也规定编写dockerfile文件首字母大写
```

Successfully built fc71ab59d268
Successfully tagged mycentos:0.1

**对比一下：**

<img src="image\image-20210726153307529.png" alt="image-20210726153307529" style="zoom: 200%;" />

![image-20210726153335193](image\image-20210726153335193.png)

我们可以列出本地进行的变更历史

![image-20210726153603189](image\image-20210726153603189.png)

> CMD 和 ENTRYPOINT的区别

```shell
ENTRYPOINT			# 指定这个容器启动的时候要运行的命令，可以追加命令
ONBUILD				# 当构建一个被继承DockerFile 这个时候就会运行ONBUILD 的指令。触发指令。
```

测试CMD

```shell
# 编写dockerfile文件
[root@yjy100 dockerfile]# vim test-centos

# 构建镜像
[root@yjy100 dockerfile]# docker build -f test-centos -t testmy .
Sending build context to Docker daemon  3.072kB
Step 1/2 : FROM centos
 ---> 300e315adb2f
Step 2/2 : CMD ["ls","-a"]
 ---> Running in c332ce4c46d5
Removing intermediate container c332ce4c46d5
 ---> 0200b602ccdc
Successfully built 0200b602ccdc
Successfully tagged testmy:latest

#运行
[root@yjy100 dockerfile]# docker run 0200b602ccdc
.
..
.dockerenv
bin
dev
etc
home
lib
lib64
lost+found
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
# 想追加一个 -l ls -al
[root@yjy100 dockerfile]# docker run 0200b602ccdc -l
docker: Error response from daemon: OCI runtime create failed: container_linux.go:380: starting container process caused: exec: "-l": executable file not found in $PATH: unknown.
ERRO[0001] error waiting for container: context canceled 
# cmd -l 替换了CMD ["ls","-a] 命令 -l不是命令所以不报错
```

测试ENTRYPOINT

```shell
[root@yjy100 dockerfile]# vim entrypoint
FROM centos
ENTRYPOINT ["ls","-al"]

[root@yjy100 dockerfile]# docker build -f entrypoint -t enty .
Sending build context to Docker daemon  4.096kB
Step 1/2 : FROM centos
 ---> 300e315adb2f
Step 2/2 : ENTRYPOINT ["ls","-a"]
 ---> Running in 7ffde187e9a0
Removing intermediate container 7ffde187e9a0
 ---> 2b154443e88c
Successfully built 2b154443e88c
Successfully tagged enty:latest

[root@yjy100 dockerfile]# docker run 2b154443e88c
total 56
drwxr-xr-x   1 root root 4096 Jul 26 08:00 .
drwxr-xr-x   1 root root 4096 Jul 26 08:00 ..
-rwxr-xr-x   1 root root    0 Jul 26 08:00 .dockerenv
lrwxrwxrwx   1 root root    7 Nov  3  2020 bin -> usr/bin
drwxr-xr-x   5 root root  340 Jul 26 08:00 dev
drwxr-xr-x   1 root root 4096 Jul 26 08:00 etc
drwxr-xr-x   2 root root 4096 Nov  3  2020 home
lrwxrwxrwx   1 root root    7 Nov  3  2020 lib -> usr/lib
lrwxrwxrwx   1 root root    9 Nov  3  2020 lib64 -> usr/lib64
drwx------   2 root root 4096 Dec  4  2020 lost+found
drwxr-xr-x   2 root root 4096 Nov  3  2020 media
drwxr-xr-x   2 root root 4096 Nov  3  2020 mnt
drwxr-xr-x   2 root root 4096 Nov  3  2020 opt
dr-xr-xr-x 243 root root    0 Jul 26 08:00 proc
dr-xr-x---   2 root root 4096 Dec  4  2020 root
drwxr-xr-x  11 root root 4096 Dec  4  2020 run
lrwxrwxrwx   1 root root    8 Nov  3  2020 sbin -> usr/sbin
drwxr-xr-x   2 root root 4096 Nov  3  2020 srv
dr-xr-xr-x  13 root root    0 Jul 26 05:36 sys
drwxrwxrwt   7 root root 4096 Dec  4  2020 tmp
drwxr-xr-x  12 root root 4096 Dec  4  2020 usr
drwxr-xr-x  20 root root 4096 Dec  4  2020 var
[root@yjy100 dockerfile]# docker run 2b154443e88c -l
total 56
drwxr-xr-x   1 root root 4096 Jul 26 08:00 .
drwxr-xr-x   1 root root 4096 Jul 26 08:00 ..
-rwxr-xr-x   1 root root    0 Jul 26 08:00 .dockerenv
lrwxrwxrwx   1 root root    7 Nov  3  2020 bin -> usr/bin
drwxr-xr-x   5 root root  340 Jul 26 08:00 dev
drwxr-xr-x   1 root root 4096 Jul 26 08:00 etc
drwxr-xr-x   2 root root 4096 Nov  3  2020 home
lrwxrwxrwx   1 root root    7 Nov  3  2020 lib -> usr/lib
lrwxrwxrwx   1 root root    9 Nov  3  2020 lib64 -> usr/lib64
drwx------   2 root root 4096 Dec  4  2020 lost+found
drwxr-xr-x   2 root root 4096 Nov  3  2020 media
drwxr-xr-x   2 root root 4096 Nov  3  2020 mnt
drwxr-xr-x   2 root root 4096 Nov  3  2020 opt
dr-xr-xr-x 245 root root    0 Jul 26 08:00 proc
dr-xr-x---   2 root root 4096 Dec  4  2020 root
drwxr-xr-x  11 root root 4096 Dec  4  2020 run
lrwxrwxrwx   1 root root    8 Nov  3  2020 sbin -> usr/sbin
drwxr-xr-x   2 root root 4096 Nov  3  2020 srv
dr-xr-xr-x  13 root root    0 Jul 26 05:36 sys
drwxrwxrwt   7 root root 4096 Dec  4  2020 tmp
drwxr-xr-x  12 root root 4096 Dec  4  2020 usr
drwxr-xr-x  20 root root 4096 Dec  4  2020 var

```

## 实战：Tomcat镜像

1、准备镜像文件tomcat 压缩包, jdk的压缩包! 

![image-20210726161036945](image\image-20210726161036945.png)

2、编写dockerfile文件，官方命名`Dockerfile`,build会自动寻找这个文件，就不需要-f指定了！

```shell
FROM centos
MAINTAINER yujiayi<1302525942@qq.com>

ADD jdk-8u261-linux-x64.tar.gz
ADD pache-tomcat-8.5.59.tar.gz

RUN yum -y install vim
ENV MYPATH /usr/local
WORK $MYPATH

ENV JAVA_HOME /usr/local/jdk1.8.0_11
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-8.5.59
ENV CATALINE_BASH /usr/local/apache-tomcat-8.5.59
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINE_HOME/bin


EXPOSE 8080
CMD /usr/local/apache-tomcat-8.5.59/bin/startup.sh && tail -F /url/local/apache-tomcat-8.5.59/bin/logs/catalina.out

```

3、构建镜像

```shell
 # docker build -t diytomcat .
```

4、启动镜像

5、访问测试

6、发布项目 (由于做了卷挂载，我们直接在本地编写项目岂可)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<note>
  <to>Tove</to>
  <from>Jani</from>
  <heading>Reminder</heading>
  <body>Don't forget me this weekend!</body>
</note>
```

```jsp	
<html>
    <head>
           <title>第一个 JSP 程序</title>
    </head>
    <body>
           <%
                  out.println("Hello World！");
           %>
    </body>
</html>
```

![image](image\image-20210727003037706.png)

## 发布自己的镜像

> Docker Hub

1、地址: https://hub.docker.com/  注册自己的账号

2、确定自己账户可以登录

3、在服务器提交自己的镜像

```shell
[root@yjy100 tomcatlogs]# docker login --help

Usage:  docker login [OPTIONS] [SERVER]

Log in to a Docker registry.
If no server is specified, the default is defined by the daemon.

Options:
  -p, --password string   Password
      --password-stdin    Take the password from stdin
  -u, --username string   Username

```

4、登录完毕后就可以提交镜像了  docker    push

```shell
[root@yjy100 tomcatlogs]# docker login -u dongdongaini
Password: 
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded

# push镜像的问题
[root@yjy100 tomcatlogs]# docker push dongdongaini/diytomcat:1.0
The push refers to repository [docker.io/dongdongaini/diytomcat]
An image does not exist locally with the tag: dongdongaini/diytomcat


# 解决 ，增加一个tag
[root@yjy100 tomcatlogs]# docker tag 7141ace759b3 dongdongaini/diytomcat:1.0

# docker push上去即可 自己发布的镜像尽量带版本号
[root@yjy100 tomcatlogs]# docker push dongdongaini/diytomcat:1.0
The push refers to repository [docker.io/dongdongaini/diytomcat]
6ab2f0ce3310: Pushed 
6972e42dd0b0: Pushed 
784f4ce251b6: Pushed 
2653d992f4ef: Mounted from library/centos 
1.0: digest: sha256:8ed3e7e6dde0ed4b44061dd77cb33aaaf47073d7735c39a57fd39817cac7dc44 size: 1166
```

> 阿里云镜像服务

1、登录到阿里云

2、找到容器镜像服务

3、创建命名空间

![image](image\image-20210727010244610.png)

4、创建容器镜像

![image](image\image-20210727010521379.png)

5、浏览阿里云

![image](image\image-20210727010623339.png)

# Docker网络

## 理解Docker0

 ```shell
 # 问题：docker 是如何处理网络访问的？
 ```

![image](image\image-20210727012231898.png)

```shell
# [root@yjy100 ~]# docker run -d -P --name tomcat01 tomcat

# 查看容器的内部网络地址 ip addr
[root@yjy100 ~]# docker exec -it tomcat01 ip addr    发现容器启动的时候会得到一个eth0@if26  ip地址，docker分配的!
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
25: eth0@if26: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever

```

> 原理	

1、我们每启动一个docker容 器，docker就会给docker容器分配一个ip ，我们只要安装了docker，就会有一个网卡docker0

桥接模式,使用的技术是evth-pair技术 !

```shell
# 容器带来的网卡，都是一对一对
# evth-pair就是一对的虚拟设备接口，他们都是成对出现的，-段连着协议，-段彼此相连
# 正因为有这个特性，evth-pair 充当一个桥梁，连接各种虚拟网络设备的
```

 网络原理图

![image](image\image-20210727014511792.png)

结论: tomcat01和tomcat02是公用的一个路由器, docker0。

所有的容器不指定网络的情况下,都是docker0路由的, docker会给我们的容器分配一个默认的可用IP

> 小结

Docker使用的是Linux的桥接，宿主机中是一个Dokcer容器的网桥docker0

![image](image\image-20210727014744283.png)

Docker中的所有的网络接口都是虚拟的。虚拟的转发效率高! ( 内网传递文件 ! )

只要容器删除,对应网桥-对就没了 !

## --Link

> 思考一个场景，我们编写了一个微服务，database url=ip:，项目不重启,数据库ip换掉了,我们希望可以处理这个问题 ，可以
>
> 名字来进行访问容器?

```shell
[root@yjy100 ~]# docker exec -it tomcat2 ping tomcat1 
ping: tomcat1: Name or service not known

# 解决呢  ---Link 即可以解决网络连通问题
[root@yjy100 ~]# docker exec -it tomcat3 ping tomcat2
PING tomcat2 (172.17.0.3) 56(84) bytes of data.
64 bytes from tomcat2 (172.17.0.3): icmp_seq=1 ttl=64 time=0.131 ms
64 bytes from tomcat2 (172.17.0.3): icmp_seq=2 ttl=64 time=0.061 ms
64 bytes from tomcat2 (172.17.0.3): icmp_seq=3 ttl=64 time=0.061 ms
64 bytes from tomcat2 (172.17.0.3): icmp_seq=4 ttl=64 time=0.092 ms
64 bytes from tomcat2 (172.17.0.3): icmp_seq=5 ttl=64 time=0.126 ms

```

其实这个tomcat3就是在本地配置了tomcat2的配置

```shell
# 查看host 文件
[root@yjy100 ~]# docker exec -it tomcat3 cat /etc/hosts
127.0.0.1	localhost
::1	localhost ip6-localhost ip6-loopback
fe00::0	ip6-localnet
ff00::0	ip6-mcastprefix
ff02::1	ip6-allnodes
ff02::2	ip6-allrouters
172.17.0.3	tomcat2 56bcf4bc642b
172.17.0.4	e01ada162c52

```



本质探究: -link就是我们在hosts配置中增加了一个172.18.0.3 tomcat02 312857784cd4

我们现在玩Docker已经不建议使用-link了 !

自定义网络!不适用docker0 !

## 自定义网络

> 查看所有docker网络	

<img src="image\image-20210727141524658.png" alt="image-20210727141524658" style="zoom:150%;" />

**网络模式**

bridge：桥接 docker (默认，自己搭桥)

none：不配置网络

host：和宿主机共享网络

container：容器网络连通！ （用的少 局限性大）

**测试**

```shell
# 我们直接启动的命令  --net bridge，而这个就是我们的docker0
[root@yjy100 ~]# docker run -d -P --name tomcat01  tomcat
[root@yjy100 ~]# docker run -d -P --name tomcat01 --net bridge tomcat

# docker0特点 默认，域名不能访问 --link可以打通连接 ！
# 我们可以自定义一个网络
# --driver bridge
# --subnet 192.168.0.0/16
#--gateway 192.168.0.1
[root@yjy100 ~]# docker network create --driver bridge --subnet 192.168.0.0/16 --gateway 192.168.0.1 mynet
82d3d6358487df6a6fee3113fc930e88612912baf814b31c4e72e9be5dcd3196
[root@yjy100 ~]# docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
1d46b9f7d2b9   bridge    bridge    local
69cc74df6fae   host      host      local
82d3d6358487   mynet     bridge    local
34bfdfda8eae   none      null      local
```

![image](image\image-20210727143234651.png)

```shell
[root@yjy100 ~]# docker run -d -P --name tomcat01-net --net mynet tomcat
c31ed6d8d85a1603593ad6effe32a403380a6dfa07b28ea354a9378bdcaf19ad
[root@yjy100 ~]# docker run -d -P --name tomcat02-net --net mynet tomcat
b396a28478235d85cf0d180f8b6316ab934f1b2517a3f594568c239608e98c0a
[root@yjy100 ~]# docker network inspect mynet
[
    {
        "Name": "mynet",
        "Id": "82d3d6358487df6a6fee3113fc930e88612912baf814b31c4e72e9be5dcd3196",
        "Created": "2021-07-27T14:28:15.849746523+08:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "192.168.0.0/16",
                    "Gateway": "192.168.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "b396a28478235d85cf0d180f8b6316ab934f1b2517a3f594568c239608e98c0a": {
                "Name": "tomcat02-net",
                "EndpointID": "63bc7e70e5baaba96ceb1d885bab89c2bb4077974246ff756ea8e7f9171530ed",
                "MacAddress": "02:42:c0:a8:00:03",
                "IPv4Address": "192.168.0.3/16",
                "IPv6Address": ""
            },
            "c31ed6d8d85a1603593ad6effe32a403380a6dfa07b28ea354a9378bdcaf19ad": {
                "Name": "tomcat01-net",
                "EndpointID": "efc911a1ae97bfab5192d10b7c09fa50125d8f09141cde231ff21678a24696b8",
                "MacAddress": "02:42:c0:a8:00:02",
                "IPv4Address": "192.168.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
# 再次测试ping
[root@yjy100 ~]# docker exec -it tomcat01-net ping 192.168.0.3
PING 192.168.0.3 (192.168.0.3) 56(84) bytes of data.
64 bytes from 192.168.0.3: icmp_seq=1 ttl=64 time=0.215 ms
64 bytes from 192.168.0.3: icmp_seq=2 ttl=64 time=0.136 ms
64 bytes from 192.168.0.3: icmp_seq=3 ttl=64 time=0.060 ms
64 bytes from 192.168.0.3: icmp_seq=4 ttl=64 time=0.062 ms
64 bytes from 192.168.0.3: icmp_seq=5 ttl=64 time=0.146 ms
64 bytes from 192.168.0.3: icmp_seq=6 ttl=64 time=0.060 ms
^C
--- 192.168.0.3 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 10ms
rtt min/avg/max/mdev = 0.060/0.113/0.215/0.058 ms
#现在不使用--1ink也可以ping名字了!
[root@yjy100 ~]# docker exec -it tomcat01-net ping tomcat02-net
PING tomcat02-net (192.168.0.3) 56(84) bytes of data.
64 bytes from tomcat02-net.mynet (192.168.0.3): icmp_seq=1 ttl=64 time=0.051 ms
64 bytes from tomcat02-net.mynet (192.168.0.3): icmp_seq=2 ttl=64 time=0.060 ms
64 bytes from tomcat02-net.mynet (192.168.0.3): icmp_seq=3 ttl=64 time=0.062 ms
^C
--- tomcat02-net ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 5ms

```

我们自定义的网络docker都已经帮我们维护好了对应的关系,推荐我们平时这样使用网络 !

## 网络连通

```shell
# 测试打通 tomcat1 到 mynet
# 连通之后就是将 tomcat1 放到了 mynet网络中

```

![image](image\image-20210727144831082.png)

```shell
# tomcat1是可以打通的
```



![image](image\image-20210727144927338.png)

结论:假设要跨网络操作别人,就需要使用docker network connect连通!。。。。



# Docker Compose

## 简介

Docker

DockerFile   build  run  手动操作，单个容器

Docker Compose 来轻松高校的管理容器，定义运行多个容器。

```shell
Compose 是一个用于定义和运行多容器 Docker 应用程序的工具。借助 Compose，您可以使用 YAML 文件来配置应用程序的服务。然后，使用单个命令，从配置中创建并启动所有服务。要了解有关 Compose 的所有功能的更多信息，请参阅功能列表。

Compose 适用于所有环境：生产、登台、开发、测试以及 CI 工作流。您可以在Common Use Cases 中了解有关每个案例的更多信息。

使用 Compose 基本上是一个三步过程：

使用 定义您的应用程序的环境，Dockerfile以便它可以在任何地方复制。

定义组成您的应用程序的服务，docker-compose.yml 以便它们可以在隔离的环境中一起运行。

运行docker compose up和码头工人组成命令启动并运行你的整个应用程序。您也可以docker-compose up使用 docker-compose 二进制文件运行。
```

**总结：**

定义、运行多个容器。

YAML file 配置文件。

single command。命令 有哪些?



Compose 是Docker官方的开源项目。需要安装！

==Dockerfile== 让程序在任何地方运行。 web服务，redis，mysql，nginx....多个容器 。run

Compose：重要的概念

* 服务servies，容器。应用。 (web，redis，mysql.....)
* 项目project。一组关联的容器

## 安装

1、下载

```shell
# 使用国内镜像源，速度较快
sudo curl -L "https://get.daocloud.io/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

```

![image](image\image-20210730212404331.png)

**下载成功**

2、授权

```shell
sudo chmod +x /usr/local/bin/docker-compose
```

![image](image\image-20210730212602721.png)

# 体验

1、应用app.py 

```shell
 # 为项目创建一个目录
 mkdir composetest
 cd composetest
 import time
# 创建app.py 写入内容
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
```

2、Dockerfile 应用打包为镜像

```shell
# 创建Dockerfile
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
CMD ["flask", "run"]
```

3、Docker-compose yaml文件(定义整 个服务，需要的环境。web、 redis) 完整的上线服务!

```shell
# 创建docker-compose.yml
version: "3.9"
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```

4、启动compose项目(docker-compose up)

```shell
# docker-compose up
```

![image](image\image-20210730230220266.png)

流程:

1、创建网络

2、执行Docker-compose yaml

3、启动服务。

Docker-compose yaml

Creating composetest web_ .1 .... done

Creating composetest redil 1.. done

自动的默认规则？

![image](image\image-20210730225833448.png)

docker images

![image](image\image-20210730230327161.png)

默认的服务名文件名 服务名_ num

多个服务器。集群。A B_ _num 副本数量

服务redis服务=> 4个副本。

集群状态。服务都不可能只有一个运行实例。

**网络规则**

![image](image\image-20210730230438084.png)

![image](image\image-20210730230622275.png)

**docker-compose**

以前都是单个docker run启动容器。

docker-compose。通过docker-compose编写yaml配置文件、可以通过compose -键启动所有服务,停止。!

**Docker小结:**

1、Docker镜像。run=>容器

2、DockerFile 构建镜像(服务打包)

3、docker-compose 启动项目(编排、多个微服务/环境)

4、Docker 网络 !

## yaml 规则

docker-compose.yaml 核心 ！

```yaml
# 3层 ！
version:  # 版本
servicer: # 服务
	服务1：web
		# 服务配置
		images
		build
		network
		.....
	服务2：redis
	........
	服务3：....
# 其他配置  网络/卷  全局规则
volumes:
network:
configs:
	
```

# 开源项目

## 博客

下载程序，安装数据库，配置.....

compose应用。=> 一键启动

1、下载项目 (docker-compose.yml)

2、如果需要文件。Dockerfile

3、文件准备齐全，(直接一键启动！)

docker-compsoe up 前台启动

docker-compose up -d 后台启动

假设项目要重新部署打包

```shell
docker-compose up build # 重新构建
```

**总结:**

**工程、服务、容器**

项目compose:三层

● 工程Porject

● 服务服务

● 容器运行实例! docker k8s

# Docker Swarm

## 工作模式

![image](image\image-20210731151902414.png)

初始化一个主节点 ==docker swarm init==

docker swarm init --advertive-addr ip地址

docker node ls 查看节点  

docker swarm join 加入一个节点

```shell
# 获取令牌
docker swarm join-token manager
docker swarm join-token worker
```

**总结：**

1、生成主节点init

2、加入 (manage，worker)

# Raft协议

双主双从:假设- 个节点挂了!其他节点是否可以用!

集群，可用 ！至少需要三个主系欸但   >1台管理节点存活 

Raft协议:I保证大多数节点存活才可以用。高可用

work就是工作的不能使用管理的命令 管理节点可以操作 

docker-composeup! 启动一个项目。单机!

集群: swarm

# docker serivce

容器=>服务!

容器=>服务! =>副本!

redis服务=> 10个副本! (同时开启10个redis容器)

```shell
docker run   容器启动！ 不具备扩缩容器
docker service 服务！ 具备扩缩容器  滚动更新！
```

动态扩缩容

服务,集群中任意的节点都可以访问。服务可以有多个副本动态扩缩容实现高可用 !

弹性、扩缩容!



## **概念总结**

**swarm**

集群的管理和编号。docker可以初始化- 个swarm集群，其他节点可以加入。(管理、 工作者)

**Node**

就是一个docker节点。多个节点就组成了-个网络集群。(管理、 工作者)

**Service**

任务，可以在管理节点或者工作节点来运行。核心。!用户访问!

**Task** 

容器内的命令，细节任务!



拓展:网络模式: "PublishMode'": "ingress"

Swarm:

Overlay:

ingress :特殊的Overlay网络!负载均衡的功能! IPVS VIP!



虽然docker在4台机器上,实际网络是同一个!    ingress 网络，是一个特殊的Overlay网络！

# Docker Stack



# Docker Secret

# Docker Config
