#  docker是什么？
## 前言
用一句话概括就是：docker可以将我们的项目打包，然后无障碍地部署到大部分服务器上。docker本身可以运行在大部分系统上，但使用 docker部署的项目必须基于 linux系统。也就是说我们可以在 windows上用 docker部署运行在 Linux上的项目，但是我们没办法在 windows上用 docker部署运行在 windows上的项目，当然在 Linux上也不行。 
  
在手动部署项目的时候我们通常会先把代码上传到服务器、然后安装相关依赖、配置环境、最后启动项目。通常这些过程都需要我们手动敲入命令，每次部署的时候都需要重新敲一遍。而 docker做的工作就是将这些命令记录下来，在部署的时候再逐个执行。

看到这里可能会有人问：这和我写的部署脚本有什么区别？如果 docker仅仅只做这些事的话，那真的是没有啥区别。但是 docker还能够保证每次运行的环境都是一致的，并且与宿主机的环境进行隔离。相信看到这里大家已经能够 get到 docker的妙用了。
## Docker 的组成
##### Docker 镜像(image): 
就是一个只读的模板。镜像可以用来创建 Docker 容器，一个镜像可以创建很多容器。它也相当于是一个root文件系统。比如官方镜像 centos:7 就包含了完整的一套 centos:7 最小系统的 root 文件系统。相当于容器的“源代码”，docker镜像文件类似于Java的类模板，而docker容器实例类似于java中new出来的实例对象。  

##### Docker 仓库(Registry): 
仓库（Repository）是集中存放镜像文件的场所。类似于Maven仓库，存放各种jar包的地方；github仓库，存放各种git项目的地方；Docker公司提供的官方registry被称为Docker Hub，存放各种镜像模板的地方。仓库分为公开仓库（Public）和私有仓库（Private）两种形式。最大的公开仓库是 Docker Hub(https://hub.docker.com/)，存放了数量庞大的镜像供用户下载。国内的公开仓库包括阿里云 、网易云等
##### Docker 容器(Container):
1、从面向对象角度:
   Docker 利用容器（Container）独立运行的一个或一组应用，应用程序或服务运行在容器里面，容器就类似于一个虚拟化的运行环境，容器是用镜像创建的运行实例。就像是Java中的类和实例对象一样，镜像是静态的定义，容器是镜像运行时的实体。容器为镜像提供了一个标准的和隔离的运行环境，它可以被启动、开始、停止、删除。每个容器都是相互隔离的、保证安全的平台

2、从镜像容器角度:
   可以把容器看做是一个简易版的 Linux 环境（包括root用户权限、进程空间、用户空间和网络空间等）和运行在其中的应用程序。


## Dockerfile是什么
前面讲到了 docker通过记录执行的命令来保证每次部署时执行的命令都一致，Dockerfile就是保存这些命令的文件。docker会根据 Dockerfile来构建环境并生成一个镜像，最后通过运行镜像来完成项目部署。

想要快速上手 docker我们需要了解下面这几个命令：FROM, MAINTAINER, ENV, ADD, COPY, EXPOSE, ENTRYPOINT, WORKDIR, RUN, CMD等。下面我们对他们进行逐个介绍。

### 1.1 FROM

`FROM`用来指定基础镜像。可以理解为所需要的的操作系统，不过与操作系统不同的是 `FROM` 指定的镜像通常会配置好我们所需要的的环境。比如下面这行代码就指定了带有 `python` 环境的镜像，我们可以在构建好的镜像中直接使用 `python` 而不需要额外安装。

```text
FROM python:3.6
```

### 1.2 MAINTAINER

`MAINTAINER` 指定了 Dockerfile的作者，或者说维护者。可填可不填。

### 1.3 ENV

`ENV`用来设置环境变量。示例如下：

```text
ENV PRODUCTION_ENV 1
```

### 1.4 ADD

`ADD` 命令可以用来向镜像中添加我们需要的文件，比如配置文件、代码、资源文件等等。`ADD` 中所使用的的路径是 Dockerfile所在目录的相对路径，也可以使用 URL，如果目标文件是一个 tar压缩包的话会被自动解压成目录。示例如下，其中第一个参数是要添加的文件，第二个参数是镜像中对应的文件，如果不存在会自动创建：

```text
ADD ./database.ini /root
ADD ./src /root
ADD http://www.baidu.com /root
ADD code.tar /root
```

### 1.5 COPY

`COPY` 的功能和 `ADD` 相似，不过 `COPY` 只能复制本地的文件到镜像中，并且不会自动解压 tar压缩包。

### 1.6 EXPOSE

`EXPOSE` 声明容器中要使用的端口，仅仅做声明，没有实际作用。运行时使用 `-p 容器端口:宿主机端口` 指定端口映射。

```text
EXPOSE 80
EXPOSE 80 8080
```

### 1.7 ENTRYPOINT

容器启动时执行的命令，并且不会被 `docker run` 的参数覆盖。如果指定了多个 `ENTRYPOINT` 只有最后一个会被执行。命令的格式如下：

-   `ENTRYPOINT ["可执行文件", "参数1", "参数2"]`
-   `ENTRYPOINT 命令 参数1 参数2`

### 1.8 WORKDIR

`WORKDIR` 指定工作目录。后续的所有命令都会在这个目录下面执行。

### 1.9 RUN

`RUN` 表示要执行的命令，比如我们在 `/root/project` 下面有一个 `requirements.txt` 文件，保存了我们项目的依赖，下面的命令可以让我们在构建镜像时安装依赖：

```bash
WORKDIR /root/project
RUN pip isntall -r requirements.txt
```

### 1.10 VOLUME

`VOLUME` 声明容器中的挂载点，在运行的时候通过 `-v` 绑定到宿主机目录，注意需要提供完整的目录路径。

也可以用下面的方法在 Dockerfile中指定，但是这种方法绑定的目录是以 docker的安装目录加上容器 ID为根目录的，也就是不能指定具体的目录，如果想指定具体的目录必须在运行时通过 `-v` 绑定。

```text
VOLUME ["/data", "/data"]
```

上面的 `/data` 可能在宿主机上的路径为 `d:/docker/一长串容器ID字符/data`。

## 2 实践
前面命令讲了那么多，现在我们来实践一下。我们先来创建一个项目，目录结构如下：

```text
httpServer/
│  log/
│  http.py
└─ Dockerfile
```

其中我们在 `http.py` 中写了一个简单的 HTTP服务器，这个服务器在接收到请求时会将请求报文的第一行保存到 `log.txt` 中，并返回 `this is docker server!`。为了防止重复部署时 `log.txt` 中的内容丢失，我们使用 `VOLUME` 声明一个挂在点，这样就可以将 `log.txt` 保存在宿主机上。

`http.py` 中的内容如下：

```python
import socket

from multiprocessing import Process


def handle_client(client_socket):
    # 解析请求报文
    request_data = client_socket.recv(1024)
    request_lines = request_data.splitlines()
    request_start_line = request_lines[0]

    # 打开日志文件写入日志 这个日志文件保存在宿主机上
    with open('./log/log.txt', 'ab') as f:
        f.write(request_start_line + b'\n')

    # 构建响应
    response_start_line = "HTTP/1.1 200 OK\r\n"
    response_headers = "Server: docker server\r\n"
    response_body = "The is docker server!"
    response = response_start_line + response_headers + "\r\n" + response_body

    # 向客户端返回响应数据
    client_socket.send(bytes(response, "utf-8"))

    # 关闭客户端连接
    client_socket.close()


if __name__ == "__main__":
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server_socket.bind(('0.0.0.0', 8000))
    server_socket.listen(128)

    while True:
        client_socket, client_address = server_socket.accept()
        handle_client_process = Process(target=handle_client, args=(client_socket,))
        handle_client_process.start()
        client_socket.close()
```

下面我们来编写 Dockerfile：

```text
# 指定带有 python 3.6环境的镜像
FROM python:3.6
# 作者
MAINTAINER geebos
# 将当前目录所有文件添加到要构建的镜像中
COPY . /root/httpServer
# 声明容器中的 /root/httpServer/log 目录为挂载点
VOLUME /root/httpServer/log
# 设置工作目录
WORKDIR /root/httpServer
# 绑定端口
EXPOSE 8000
# 设置启动命令
ENTRYPOINT python http.py
```

上面这些文件都创建好之后我们开始构建镜像：

首先运行 `docker build -t http-server .` 构建镜像。 - 其中 `-t http-server` 指定了镜像的名字为 `http-server`，我们也可以这样设置来指定镜像的版本 `-t http-server:1.0`，不过如果我们指定了版本号的话，在启动容器的时候也需要带上版本号，否则会找不到镜像。

然后运行 `docker run -id -v d:/dockerTest/httpServer/log:/root/httpServer/ log -p 8000:8000 --name http-server-container http-server` 来启动容器。其中 ：

-   `-d` 表示后台启动
-   `--name http-server-container` 指定容器的名称为 `http-server-container`
-   `-v d:/dockerTest/httpServer/log:/root/httpServer/log`绑定挂载目录
-   `-p 8000:8000` 指定端口映射。

启动之后我们可以访问 `http://127.0.0.1:8000`。访问之后查看 `d:/dockerTest/httpServer/log/log.txt` 中会发现我们的请求记录被保存到宿主机上了。

我们可以使用 `docker exec -it http-server-container /bin/bash` 进入到容器内部。也可以试着更改 Dockerfile中的参数看看有什么效果。

## 3 常用 docker命令

-   `docker build`：构建镜像。

-   常用格式：`docker build -t 镜像名 Dockerfile所在路径`。
-   示例： `dcoker build -t image-name .`。

-   `docker run`：基于镜像启动容器。

-   常用格式：`docker run -id -t --name 容器名 镜像名/镜像ID`。
-   示例：`docker run -id -t --name container-name image-name`。

-   `docker ps`：显示所有容器信息。
-   `docker images`：显示所有镜像信息。
-   `docker stop`：停止容器运行。
-   `docker start`：重新运行一个已停止的容器。
-   `docker rm`：删除容器，删除之前要先确保容器已经停止运行。可以指定多个容器。

-   示例：`docker rm container-name`。

-   `docker rmi`：删除镜像，删除之前要确保没有基于该镜像的容器存在。可以指定多个镜像。

-   示例：`docker rmi image-name/image-id`

-   `docker exec`：在容器中执行命令。

-   示例：`docker exec -it container-name /bin/bash`。这命令可以启动容器内的 `bash`，其中 `-i` 表示以交互的方式运行命令，`-t` 表示在终端（tty）中运行。

## **4 docker部署常用流程**

-   上传项目文件到服务器
-   进入项目文件夹运行 `docker build -t image-name:version .` 构建镜像，强烈建议指定版本号，这样在部署出错的情况下可以快速回滚。

-   示例：`docker build -t server:v1 .`

-   在运行容器之前先停止老版本的容器释放端口等资源，`docker stop server-container:v0`
-   镜像构建完成之后再运行 `docker run -d --name container-name:version image-name:version`

-   示例：`docekr run -d --name server-container:v1 server:v1`

-   确定服务正常运行之后删除之前版本的镜像和容器，如果服务器空间足够的话可以先不删除镜像，只删除容器。

-   `docker rm server-container:v0`
-   `docker rmi server:v0`

-   如果在部署后发现有问题需要恢复之前的版本

-   `docker stop server-container:v1`
-   `docker run -d --name server-contaienr:v0 server:v0`