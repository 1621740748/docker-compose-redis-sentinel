# docker-compose-redis-sentinel
docker-compose编排方式安装redis 主从复制与哨兵机制

         
# 安装准备：
[root@localhost ]#mkdir -p  /usr/local/docker-compose-redis-sentinel
将准备文件全部上传到docker-compose-redis-sentinel目录下

[root@localhost ]#cd /usr/local/docker-compose-redis-sentinel

[root@localhost docker-compose-redis-sentinel]# ll
total 8
drwxrwxrwx. 2 root root   51 Nov 27 20:27 conf
-rwxrwxrwx. 1 root root 3984 Nov 27 21:56 docker-compose.yaml
-rw-r--r--. 1 root root  201 Nov 27 22:15 Dockerfile
drwxrwxrwx. 2 root root   84 Nov 27 21:56 redis-master-conf
drwxrwxrwx. 2 root root   87 Nov 27 22:02 redis-sentinel1-conf
drwxrwxrwx. 2 root root   87 Nov 27 22:02 redis-sentinel2-conf
drwxrwxrwx. 2 root root   87 Nov 27 22:02 redis-sentinel-conf
drwxr-xr-x. 2 root root   84 Nov 27 21:52 redis-slave1-conf
drwxrwxrwx. 2 root root   84 Nov 27 21:56 redis-slave2-conf




# 1.构建镜像

#在dockerfile目录 执行下面代码，注意后面上下文点号，执行创建镜像；创建完成后可以docker images查看生成的镜像
[root@localhost docker-compose-redis-sentinel]# docker build -t redis .


# 2.编写docker-compose编排文件docker-compose.yaml

查看构建编排文件的版本
[root@localhost docker-compose-redis-sentinel]# docker-compose version
docker-compose version 1.18.0, build 8dd22a9
docker-py version: 2.6.1
CPython version: 3.6.8
OpenSSL version: OpenSSL 1.0.2k-fips  26 Jan 2017
# 【注意：安装的时候如果版本不对会自动提示版本】
例子：
[root@localhost docker-compose-redis-sentinel]# docker-compose up -d
WARNING: Found multiple config files with supported names: docker-compose.yml, docker-compose.yaml
WARNING: Using docker-compose.yml

ERROR: Version in "./docker-compose.yml" is unsupported. You might be seeing this error because you're using the wrong Compose file version. Either specify a supported version (e.g "2.2" or "3.3") and place your service definitions under the `services` key, or omit the `version` key and place your service definitions at the root of the file to use version 1.

# 3.执行编排
[root@localhost docker-compose-redis-sentinel]# docker-compose up -d
Creating dc-redis-sentinel ... done
Creating dc-redis-slave1 ... 
Creating dc-redis-master ... 
Creating dc-redis-sentinel1 ... 
Creating dc-redis-sentinel2 ... 
Creating dc-redis-sentinel ... 



# 4.执行成功后查看容器
[root@localhost docker-compose-redis-sentinel]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                                NAMES
f5464135219f        redis               "/bin/bash start.sh"   6 seconds ago       Up 5 seconds        6379/tcp, 0.0.0.0:26360->26379/tcp   dc-redis-sentinel
b27b9a7cb185        redis               "/bin/bash start.sh"   6 seconds ago       Up 5 seconds        6379/tcp, 0.0.0.0:26361->26379/tcp   dc-redis-sentinel1
36b81cbe821d        redis               "/bin/bash start.sh"   6 seconds ago       Up 5 seconds        6379/tcp, 0.0.0.0:26362->26379/tcp   dc-redis-sentinel2
804f547c09db        redis               "/bin/bash start.sh"   6 seconds ago       Up 6 seconds        0.0.0.0:6360->6379/tcp               dc-redis-master
b366a048a4d9        redis               "/bin/bash start.sh"   7 seconds ago       Up 6 seconds        0.0.0.0:6361->6379/tcp               dc-redis-slave1
e53b98603a3c        redis               "/bin/bash start.sh"   7 seconds ago       Up 6 seconds        0.0.0.0:6362->6379/tcp    


# 5.编排的启动和关闭都需要在对应的目录下执行

docker-compose start

docker-compose stop

# 6.查看编排容器

[root@localhost docker-compose-redis-sentinel]# docker-compose ps
       Name               Command          State                   Ports               
---------------------------------------------------------------------------------------
dc-redis-master      /bin/bash start.sh   Exit 137                                     
dc-redis-sentinel    /bin/bash start.sh   Up         0.0.0.0:26360->26379/tcp, 6379/tcp
dc-redis-sentinel1   /bin/bash start.sh   Up         0.0.0.0:26361->26379/tcp, 6379/tcp
dc-redis-sentinel2   /bin/bash start.sh   Up         0.0.0.0:26362->26379/tcp, 6379/tcp
dc-redis-slave1      /bin/bash start.sh   Up         0.0.0.0:6361->6379/tcp            
dc-redis-slave2      /bin/bash start.sh   Up         0.0.0.0:6362->6379/tcp  



