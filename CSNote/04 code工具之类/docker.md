## Docker概述 [	](docker_20201125093504113)


### 安装Docker [	](docker_20201124103028682)

1. `yum update`:{{c1::yum 包更新到最新 }}
2. `yum install -y yum-utils device-mapper-persistent-data lvm2`:{{c1::安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的 }}
3. `yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo`:{{c1:: 设置yum源}}
4. `yum install -y docker-ce`:{{c1:: 安装docker，出现输入的界面都按 y }}
5. `docker -v`:{{c1:: 查看docker版本，验证是否验证成功}}

### Docker基础概念 [	](docker_20201124103028685)
+ 镜像（Image）：{{c1:: Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。 }}
+ 容器（Container）：{{c1:: 镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和对象一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。 }}
+ 仓库（Repository）：{{c1:: 仓库可看成一个代码控制中心，用来保存镜像。 }}

## Docker基本操作 [	](docker_20201125093504115)

### Docker进程相关命令 [	](docker_20201124103028687)

+ 启动docker服务: {{c1:: `systemctl start docker` }}
+ 停止docker服务: {{c1:: `systemctl stop docker` }}
+ 重启docker服务: {{c1:: `systemctl restart docker` }}
+ 查看docker服务状态: {{c1:: `systemctl status docker` }}
+ 设置开机启动docker服务: {{c1:: `systemctl enable docker` }}

### Docker 镜像相关命令 [	](docker_20201124103028692)

+ 查看镜像: 查看本地所有的镜像
    1. {{c1:: `docker images` }}
    2. {{c1:: `docker images –q` # 查看所用镜像的id }}
+ 搜索镜像:从网络中查找需要的镜像
  
    + {{c1:: `docker search` 镜像名称 }}
+ 拉取镜像:从Docker仓库下载镜像到本地，镜像名称格式为 名称:版本号，如果版本号不指定则是最新的版本。如果不知道镜像版本，可以去docker hub 搜索对应镜像查看。
  
    + {{c1:: `docker pull 镜像名称` }}
+ 删除镜像: 删除本地镜像
    ```shell
    #{{c1::
    docker rmi 镜像id # 删除指定本地镜像
    docker rmi `docker images -q` # 删除所有本地镜像
    #}}
    ```
### Docker 查看容器命令 [	](docker_20201124103028695)
+ 查看正在运行的容器:{{c1::`docker ps `}}
+ 查看所有容器:{{c1::`docker ps –a `}}

### Docker 创建并启动容器命令 [	](docker_20201124103028697)
+ 语法：{{c1:: `docker run 参数` }}
+ 参数：
  + `-i`：{{c1:: 保持容器运行。通常与 -t 同时使用。加入it这两个参数后，容器创建后自动进入容器中，退出容器后，容器自动关闭。 }}
  + `-t`：{{c1:: 为容器重新分配一个伪输入终端，通常与 -i 同时使用。 }}
  + `-d`：{{c1:: 以守护（后台）模式运行容器。创建一个容器在后台运行，需要使用docker exec 进入容器。退出后，容器不会关闭。 }}
  + `-it`：{{c1:: 创建的容器一般称为交互式容器，-id 创建的容器一般称为守护式容器 }}
  + `--name`：{{c1:: 为创建的容器命名。 }}
  + `-p 8080:8080`：{{c1:: 将容器的8080端口映射到主机的8080端口 }}

### Docker 容器相关命令 [	](docker_20201124103028700)
+ 进入容器：
  + {{c1:: `docker exec 参数 # 退出容器，容器不会关闭` }}
+ 停止容器：
  + {{c1:: `docker stop 容器名称` }}
+ 启动容器：
  + {{c1:: `docker start 容器名称` }}
+ 删除容器：
  + {{c1:: `docker rm 容器名称` }}
  + 注意：{{c1:: 如果容器是运行状态则删除失败，需要停止容器才能删除 }}
+ 查看容器信息：
  + {{c1:: `docker inspect 容器名称` }}

## 数据卷 [	](docker_20201125093504119)

### 配置数据卷 [	](docker_20201124103028704)

+ 命令：{{c1:: `docker run ... –v 宿主机目录(文件):容器内目录(文件) ...` }}
  + 注意：{{c1:: 是创建启动容器时，使用 `–v` 参数 设置数据卷 }}
+ 注意事项：
  1. 目录必须是绝对路径
  2. 如果目录不存在，会自动创建
  3. 可以挂载多个数据卷
### 配置数据卷容器 [	](docker_20201124103028706)
+ ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201119212013.png)
1. 创建启动c3数据卷容器，使用{{c1:: `–v`  }}参数 设置数据卷
   + {{c1:: `docker run –it --name=c3 –v /volume centos:7 /bin/bash` }}
   + 注意:{{c1:: 没有指定宿主机目录会自动生成一个挂载目录，可以使用`docker inspect c3`查看`source`属性 }}
2. 创建启动 c1 c2 容器，使用{{c1:: `–-volumes-from` }}参数 设置数据卷
   + {{c1:: ps `docker run –it --name=c1 --volumes-from c3 centos:7 /bin/bash` }}
   + {{c1:: `docker run –it --name=c2 --volumes-from c3 centos:7 /bin/bash` }}

## Docker 镜像 [	](docker_20201125093504121)

### Docker 镜像原理 [	](docker_20201124103028708)

1. Docker 镜像本质是什么？
   + {{c1:: 是一个分层文件系统 }}
1. Docker 中一个centos镜像为什么只有200MB，而一个centos操作系统的iso文件要几个个G？
   + {{c1:: Centos的iso镜像文件包含bootfs和rootfs，而docker的centos镜像复用操作系统的bootfs，只有rootfs和其他镜像层 }}
3. Docker 中一个tomcat镜像为什么有500MB，而一个tomcat安装包只有70多MB？
   + {{c1:: 由于docker中镜像是分层的，tomcat虽然只有70多MB，但他需要依赖于父镜像和基础镜像，所有整个对外暴露的tomcat镜像大小500多MB }}
+ 图示：{{c1:: ![](https://gitee.com/xieyun714/nodeimage/raw/master/img/20201119213314.png) }}

### 镜像制作 [	](docker_20201124103028711)

+ 提交镜像:{{c1:: `docker commit 容器id 镜像名称:版本号` }}
+ 导出镜像:{{c1:: `docker save -o 压缩文件名称 镜像名称:版本号` }}
+ 加载镜像:{{c1:: `docker load –i 压缩文件名称` }}

## Dockerfile [	](docker_20201125093504124)

### Dockerfile关键字 [	](docker_20201124103028713)

+ `FROM`
	+ 作用：{{c1:: 基础镜像，当前新镜像是基于哪个镜像的 }}
+ `MAINTAINER`
	+ 作用：{{c1:: 镜像维护者的姓名和邮箱地址 }}
+ `RUN`
	+ 作用：{{c1:: 容器构建时需要运行的命令 }}
+ `EXPOSE`
	+ 作用：{{c1:: 当前容器对外暴露出的端口 }}
+ `WORKDIR`
	+ 作用：{{c1:: 指定在创建容器后，终端默认登陆的进来工作目录，一个落脚点 }}
+ `ENV`
	+ 作用：{{c1:: 用来在构建镜像过程中设置环境变量 }}
+ `ADD`
	+ 作用：{{c1:: 将宿主机目录下的文件拷贝进镜像且ADD命令会自动处理URL和解压tar压缩包 }}
+ `COPY`
	+ 作用：{{c1:: 类似ADD，拷贝文件和目录到镜像中。将从构建上下文目录中 <源路径> 的文件/目录复制到新的一层的镜像内的 <目标路径> 位置 }}
		+ 例：{{c1:: `COPY src dest` `COPY ["src", "dest"]` }}
+ `VOLUME`
	+ 作用：{{c1:: 容器数据卷，用于数据保存和持久化工作 }}
+ `CMD`
	+ 作用：{{c1:: 指定一个容器启动时要运行的命令 }}
	+ 注意：Dockerfile 中可以有多个 CMD 指令，但只有最后一个生效，CMD 会被 docker run 之后的参数替换
+ `ENTRYPOINT `
	+ 作用：{{c1:: 指定一个容器启动时要运行的命令 }}
	+ 注意：{{c1:: ENTRYPOINT 的目的和 CMD 一样，都是在指定容器启动程序及参数，区别在于不会被覆盖 }}
+ `ONBUILD`
	+ 作用：{{c1:: 当构建一个被继承的Dockerfile时运行命令，父镜像在被子继承后父镜像的onbuild被触发 }}

### Dockerfile案例：自定义centos7镜像 [	](docker_20201124103028717)
+ 要求：
  1. 默认登录路径为 /usr
  2. 可以使用vim
+ 实现步骤
  1. 定义父镜像：{{c1:: `FROM centos:7` }}
  2. 定义作者信息：{{c1:: `MAINTAINER itheima <itheima@itcast.cn>` }}
  3. 执行安装vim命令：{{c1:: ` RUN yum install -y vim` }}
  4. 定义默认的工作目录：{{c1:: `WORKDIR /usr` }}
  5. 定义容器启动执行的命令：{{c1:: `CMD /bin/bash` }}
  6. 通过dockerfile构建镜像：{{c1:: `docker bulid –f dockerfile文件路径 –t 镜像名称:版本` }}

### Dockerfile案例：发布springboot项目 [	](docker_20201124103028720)
+ 要求：定义dockerfile，发布springboot项目
+ 实现步骤
    1. 定义父镜像：{{c1:: `FROM java:8` }}
    2. 定义作者信息：{{c1:: `MAINTAINER itheima <itheima@itcast.cn>` }}
    3. 将jar包添加到容器：{{c1:: `ADD springboot.jar app.jar` }}
    4. 定义容器启动执行的命令：{{c1:: `CMD java–jar app.jar` }}
    5. 通过dockerfile构建镜像：{{c1:: `docker bulid –f dockerfile文件路径 –t ` }}



## Docker Compose [	](docker_20201124103028722)

### 安装Docker Compose [	](docker_20201124103028726)

```shell
# Compose目前已经完全支持Linux、Mac OS和Windows，在我们安装Compose之前，需要先安装Docker。下面我 们以编译好的二进制包方式安装在Linux系统中。 
curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
# 设置文件可执行权限 
chmod +x /usr/local/bin/docker-compose
# 查看版本信息 
docker-compose -version
```
+ {{c1:: 理解 }}

### 卸载Docker Compose [	](docker_20201124103028730)
```shell
# 二进制包方式安装的，删除二进制文件即可
rm /usr/local/bin/docker-compose
```
+ {{c1:: 理解 }}


### 使用docker compose编排nginx+springboot项目 [	](docker_20201124103028734)

1. 创建docker-compose目录
    ```shell
    mkdir ~/docker-compose
    cd ~/docker-compose
    ```
2. 编写 docker-compose.yml 文件
    ```yml
    version: '3'
    services:
      nginx:
        image: nginx
        ports:
          - 80:80
        links:
          - app
        volumes:
          - ./nginx/conf.d:/etc/nginx/conf.d
      app:
        image: app
        expose:
          - "8080"
    ```
3. 创建./nginx/conf.d目录
    ```shell
    mkdir -p ./nginx/conf.d
    ```
4. 在./nginx/conf.d目录下 编写itheima.conf文件
    ```shell
    server {
        listen 80;
        access_log off;

        location / {
            proxy_pass http://app:8080;
        }
    
    }
    ```
5. 在~/docker-compose 目录下 使用docker-compose 启动容器
    ```shell
    docker-compose up
    ```
6. 测试访问
    ```shell
    http://192.168.149.135/hello
    ```
+ {{c1:: 理解 }}


## Docker 私有仓库 [	](docker_20201124103028736)

### Docker私有仓库搭建 [	](docker_20201124103028738)

```shell
# 1、拉取私有仓库镜像 
docker pull registry
# 2、启动私有仓库容器 
docker run -id --name=registry -p 5000:5000 registry
# 3、打开浏览器 输入地址http://私有仓库服务器ip:5000/v2/_catalog，看到{"repositories":[]} 表示私有仓库 搭建成功
# 4、修改daemon.json   
vim /etc/docker/daemon.json    
# 在上述文件中添加一个key，保存退出。此步用于让 docker 信任私有仓库地址；注意将私有仓库服务器ip修改为自己私有仓库服务器真实ip 
{"insecure-registries":["私有仓库服务器ip:5000"]} 
# 5、重启docker 服务 
systemctl restart docker
docker start registry
```
+ {{c1:: 理解 }}

### 将镜像上传至Docker私有仓库 [	](docker_20201124103028740)

```shell
# 1、标记镜像为私有仓库的镜像     
docker tag centos:7 私有仓库服务器IP:5000/centos:7
 
# 2、上传标记的镜像     
docker push 私有仓库服务器IP:5000/centos:7

```
+ {{c1:: 理解 }}

### 从Docker私有仓库拉取镜像  [	](docker_20201124103028742)

```shell
#拉取镜像 
docker pull 私有仓库服务器ip:5000/centos:7
```
+ {{c1:: 理解 }}