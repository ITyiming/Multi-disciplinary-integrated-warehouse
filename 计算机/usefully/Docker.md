## Docker

### 注明

该文章是由ChatGPT生成，**只做参考**，推荐学习网址[[zh-cn](https://docker-practice.github.io/zh-cn/)]

### Image与Container关系

**Docker 镜像（Image）：**

- **定义**：Docker 镜像是一个只读的、静态的文件，其中包含了运行应用程序所需的代码、运行时、系统工具、库以及设置。镜像是一个模板，用于创建容器实例。
- **特点**：
  - 不可修改：镜像是只读的，一旦构建完成，就不会发生改变。任何修改都会生成新的镜像。
  - 分层结构：镜像是由一系列分层组成的，每一层都代表一个特定的操作。这使得镜像的共享和复用变得更加高效。
- **用途**：镜像是容器的基础，它是容器运行时的环境。

**Docker 容器（Container）：**

- **定义**：容器是基于镜像创建的运行实例。它包含了运行时需要的应用程序、库、系统工具以及在镜像基础上的一层可写文件系统。
- **特点**：
  - 可读写：容器在运行时可以接受用户输入，并且可以修改容器内的文件系统，但这些修改仅存在于容器的生命周期内。
  - 可启动和停止：容器可以启动、停止、重启，并且可以与其他容器进行通信。
- **用途**：容器是应用程序的运行实例，可以被启动、停止、删除，并且可以在不同的环境中运行。

**关系：**

- **基于关系**：容器是基于镜像创建的，一个镜像可以创建多个容器实例。
- **镜像的唯一性**：每个容器都是镜像的一个运行实例，但容器的状态和文件系统是可变的，而镜像是不可变的。
- **分层结构**：容器实际上是在镜像的基础上添加了一层可写的文件系统。

在实际使用中，通常会通过 Docker 镜像构建容器，一个镜像可以生成多个容器实例，每个容器实例之间相互隔离。容器的运行状态可以被保存为一个新的镜像，形成新的容器，实现对应用程序和环境的快速部署和复制。

### Dockerfile、Docker和Docker Compose 

Dockerfile、Docker和Docker Compose 是 Docker 技术栈中的三个重要概念，它们之间有一定的关系，分别用于定义容器镜像构建、运行容器和多容器应用的编排。

1. **Dockerfile**:

   - **定义容器镜像构建过程**：Dockerfile 是一个文本文件，其中包含了一系列指令，用于描述如何构建一个 Docker 镜像。这些指令包括基础镜像的选择、文件复制、环境变量设置、运行命令等。通过 Dockerfile，你可以将应用程序及其依赖打包到一个容器中。

   - **例子**：

     ```bash
     FROM ubuntu:20.04
     RUN apt-get update && apt-get install -y nginx
     CMD ["nginx", "-g", "daemon off;"]
     ```

2. **Docker**:

   - **运行容器**：Docker 是一个开源平台，用于构建、发布和运行容器化应用。通过 Docker，你可以基于 Dockerfile 构建镜像，然后使用这些镜像创建和运行容器。Docker 提供了一套命令行工具和 API，用于与容器进行交互，例如启动、停止、查看日志等。

   - **例子**：

     ```bash
     # 从 Docker Hub 下载镜像并运行容器
     docker run -d -p 80:80 nginx
     ```

3. **Docker Compose**:

   - **多容器应用编排**：Docker Compose 是一个用于定义和运行多容器 Docker 应用程序的工具。通过一个单独的 `docker-compose.yml` 文件，你可以定义整个应用的服务、网络、卷等配置，然后使用 `docker-compose` 命令一键启动整个应用。这有助于简化多容器应用的管理和部署。

   - **例子**：`docker-compose.yml`

     ```bash
     version: '3'
     services:
       web:
         image: nginx
         ports:
           - "80:80"
       app:
         image: your-app-image
     ```

   - **命令**：

     ```bash
     # 在应用目录中运行
     docker-compose up
     ```

综合来说，Dockerfile 用于定义单个容器的构建规则，Docker 用于运行单个容器，而 Docker Compose 则用于定义和运行多个容器的应用程序。这三者协同工作，使得容器化应用的构建、运行和管理变得更加简单和可维护。

### Docker CE安装

Docker Community Edition

1. **载旧版本的 Docker**

如果之前安装过旧版本的 Docker，请先卸载：

```bash
sudo yum remove docker docker-common docker-selinux docker-engine
```

2. **安装 Docker CE 依赖**

```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

3. **添加 Docker 官方仓库**

```bash
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

4. **安装 Docker CE**

```bash
sudo yum install docker-ce
```

5. **启动 Docker 服务**

```bash
sudo systemctl start docker
```

6. **设置 Docker 服务自动启动**

```bash
sudo systemctl enable docker
```

7. **验证 Docker 安装**

```bash
docker --version
```

以上步骤完成后，Docker CE 就已经安装并且服务已经启动。你可以使用 `docker --version` 命令验证安装是否成功。

**使用非root用户运行 Docker 命令（可选）**

默认情况下，Docker 命令需要 root 权限。如果你想让普通用户也能运行 Docker 命令，可以将用户添加到 `docker` 用户组中：

```bash
sudo usermod -aG docker $USER
```

然后，注销并重新登录以使更改生效。

### 编译安装nginx

1. **查看Docker是否已安装：**

```bash
docker --version
```

2. **查看Nginx是否已安装：**

```bash
bnginx -v
```

如果Docker和Nginx未安装，可以按照以下步骤进行安装。

3. **在CentOS 7上安装Docker：**

```bash
sudo yum install docker
```

启动Docker服务：

```bash
sudo systemctl start docker
```

将Docker添加到开机启动：

```bash
sudo systemctl enable docker
```

4. **在Docker容器中编译安装Nginx：**

首先，创建一个Dockerfile用于构建Nginx的镜像。在你的项目目录下创建一个名为 `Dockerfile` 的文件，内容如下：

```dockerfile
DockerfileCopy codeFROM centos:7

RUN yum install -y epel-release && \
    yum install -y gcc make wget && \
    yum clean all

WORKDIR /tmp

RUN wget http://nginx.org/download/nginx-1.20.1.tar.gz && \
    tar -zxvf nginx-1.20.1.tar.gz

WORKDIR /tmp/nginx-1.20.1

RUN ./configure && \
    make && \
    make install

CMD ["nginx", "-g", "daemon off;"]
```

然后，构建Docker镜像：

```bash
docker build -t mynginx:latest .
```

最后，运行Docker容器：

```bash
docker run -p 80:80 mynginx:latest
```

现在，你可以通过访问 `http://localhost` 来验证Nginx是否成功安装和运行。

5. **使用Docker Compose：**

Docker Compose可以用来定义和运行多容器的Docker应用。创建一个名为 `docker-compose.yml` 的文件，内容如下：

```yaml
version: '3'
services:
  nginx:
    image: mynginx:latest
    ports:
      - "80:80"
```

然后，使用以下命令启动服务：

```bash
docker-compose up
```

这将根据 `docker-compose.yml` 文件中的配置启动Nginx容器。