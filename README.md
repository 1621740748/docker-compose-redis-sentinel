# docker-compose-redis-sentinel
docker-compose编排方式安装redis 主从复制与哨兵机制

         
# 安装准备：
[root@localhost ]#mkdir -p  /usr/local/docker-compose-redis-sentinel

将准备文件全部上传到docker-compose-redis-sentinel目录下

[root@localhost ]#cd /usr/local/docker-compose-redis-sentinel

[root@localhost docker-compose-redis-sentinel]#ll




# 1.构建镜像

#在dockerfile目录 执行下面代码，注意后面上下文点号，执行创建镜像；
创建完成后可以docker images查看生成的镜像
[root@localhost docker-compose-redis-sentinel]# docker build -t redis .


# 2.编写docker-compose编排文件docker-compose.yaml

查看构建编排文件的版本

[root@localhost docker-compose-redis-sentinel]# docker-compose version


# 3.执行编排
[root@localhost docker-compose-redis-sentinel]# docker-compose up -d




# 4.执行成功后查看容器
[root@localhost docker-compose-redis-sentinel]# docker ps -a


# 5.编排的启动和关闭都需要在对应的目录下执行

docker-compose start

docker-compose stop

# 6.查看编排容器
[root@localhost docker-compose-redis-sentinel]# docker-compose ps



