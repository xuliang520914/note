#### `Docker`安装

```shell
# 首先升级
yum -y update
# 然后安装docker
yum -y install docker
```

#### `Docker`的启动、停止、重启命令

```shell
# 启动
service docker start
# service 可以换成 systemctl start docker.service，其他命令一样
# 停止
service docker stop
# 重启
service docker restart
```

#### 在线安装镜像

```shell
# 如果下载镜像时候很慢，建议配置加速器，例如：阿里云
# https://cr.console.aliyun.com/?spm=a2c4e.11153940.0.0.52027e29JK3UPx 
# 登录控制台之后，左侧的加速器帮助页面就会显示为你独立分配的加速地址
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://xxxxx.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
# xxxxx是[系统分配前缀]
# --------------------
# 搜索，比如php
docker search php
# 搜索出来之后选择要安装的对应name
docker pull docker.io/php #安装最新版本
```

#### 查看已安装镜像

```shell
docker images
```

#### 导出与导入镜像

```shell
# 导出镜像
docker save docker.io/php > /home/php74.tar.gz
# 导入镜像
docker load < /home/php74.tar.gz
# 删除已导入的镜像
docker rmi docker.io/php
```

#### 启动容器

```shell
# run：启动  -it：启动容器后开启一个交互界面，不加则没有交互界面  --name：给容器起一个名字（可选）  bash：启动容器后运行什么程序，表示运行bash命令行
docker run -it --name php74 docker.io/php bash
# -p：表示启动后运行那些端口，映射到宿主机的端口 9000是宿主机端口，8080是容器端口 可以跟多个映射端口，也就是可以跟多个'-p'
docker run -it --name php74 -p 9000:8080 -p 9001:8085 docker.io/php bash
# 表示文件映射到宿主机。 -v：表示映射，'/home/project'表示宿主机文件夹，'/soft'表示容器文件夹。'--privileged'：表示容器操作映射文件或者目录的时候是使用的最高权限
docker run -it --name php74 -v /home/project:/soft --privileged docker.io/php bash
# -d：后台启动容器 -e：启动参数 --net：使用的内部网段（下文）--ip：容器分到的内部网段的ip地址
docker run -d --name php74 -v /home/project:/soft --privileged docker.io/php bash
```

#### 暂停和停止容器

```shell
# php74是启动时的name，若启动时没有指定名称，则后面跟上容器启动的编号
# 暂停运行
docker pause php74
# 恢复运行
docker unpause php74
# 停止运行
docker stop php74
# 重新启动运行
docker start -i php74
# 在容器中使用exit退出容器，同时也会停止容器运行

# 删除容器，必须先停止运行
docker rm php74
# 查看创建的所有容器
docker ps -a
```

#### 镜像名称修改

```shell
# 该命令执行后，会复制新的然后命名php74，以前的那个docker.io/php还是存在
docker tag docker.io/php php74
```

#### `Docker`创建内部网络

```shell
docker network create net1
docker network rm net1
# 创建网段名称net1，--subnet：指定网段，子网掩码24位
docker network create --subnet=172.18.0.0/24 net1
# 查看创建的网段
docker inspect net1
```

#### `Docker`卷

```shell
# 有些无法实现目录/文件映射的时候可以使用
# 在宿主机上的Docker创建一个卷，这个卷在宿主机上可以看到目录，然后把卷映射给容器。这样就可以把容器中的数据映射到卷里面，在宿主机上就可以看到映射出来的数据
docker volume create volume1
# 或者
docker volume create --name=volume1
# 查看卷的信息
docker inspect volume1
# 删除卷
docker volume rm volume1

```

