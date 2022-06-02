## 总体步骤

1.   搜索镜像
2.   拉取镜像
3.   查看镜像
4.   启动镜像
5.   停止容器
6.   移除容器

## 安装 Tomcat

1.   docker hub 上面查找 Tomcat 镜像。

     ![image-20220602195500954](img/image-20220602195500954.png)

2.   从 docker hub 上拉取 Tomcat 镜像到本地。

     ![image-20220602195716363](img/image-20220602195716363.png)

3.   docker images 查看是否有拉取到的 Tomcat。

     ![image-20220602195735790](img/image-20220602195735790.png)

4.   使用 Tomcat 镜像创建容器实例（也叫做运行镜像）。

     >   docker run -it -p 8080:8080 tomcat 

5.   访问 Tomcat 首页。

     ![image-20220602200138185](img/image-20220602200138185.png)

## 安装 MySQL

1.   docker hub 上面查找 MySQL 镜像。

     ![image-20220602200350300](img/image-20220602200350300.png)

2.   从 docker hub 上（阿里云加速器）拉取 MySQL 镜像到本地标签为 5.7。

     ![image-20220602200536352](img/image-20220602200536352.png)

3.   使用 MySQL 5.7 镜像创建容器（也叫运行镜像）。

     1.   命令出处，哪里来的？

          ￼![image-20220602200727863](img/image-20220602200727863.png)

     2.   简单版

          >   使用 MySQL 镜像：
          >
          >   docker run -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.7
          >
          >   docker ps
          >
          >   docker exec -it 容器 ID /bin/bash
          >
          >   mysql -uroot -p
          >
          >   ![image-20220602201054941](img/image-20220602201054941.png)
          >
          >   
          >
          >   建库建表插入数据：
          >
          >   ![image-20220602201343122](img/image-20220602201343122.png)
          >
          >   
          >
          >   问题：插入中文数据试试？为什么报错？
          >
          >   答：Docker 上默认字符集编码隐患。
          >
          >   ![image-20220602201619795](img/image-20220602201619795.png)
          >
          >   ![image-20220602201711375](img/image-20220602201711375.png)

     3.   实战版

          1.   新建 MySQL 容器实例

               >   docker run -d -p 3306:3306 --privileged=true -v /zzyyuse/mysql/log:/var/log/mysql -v /zzyyuse/mysql/data:/var/lib/mysql -v /zzyyuse/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456 --name mysql mysql:5.7 
               >
               >   ![image-20220602202118519](img/image-20220602202118519.png)

          2.   新建 my.cnf，通过容器卷同步给 MySQL 容器实例

               >   client]
               >
               >   default_character_set=utf8 
               >
               >   [mysqld] 
               >
               >   collation_server = utf8_general_ci 
               >
               >   character_set_server = utf8 
               >
               >   ![image-20220602202153638](img/image-20220602202153638.png)

          3.   重新启动 MySQL 容器实例再重新进入并查看字符编码

               ![image-20220602202207696](img/image-20220602202207696.png)

          4.   再新建库新建表再插入中文测试

               ![image-20220602202217833](img/image-20220602202217833.png)

          5.   结论

               ![image-20220602202245554](img/image-20220602202245554.png)

## 安装 Redis

1.   从 docker hub 上（阿里云加速器）拉取 Redis 镜像到本地标签为 6.0.8

     ![image-20220602202718913](img/image-20220602202718913.png)

2.   入门命令

     ![image-20220602202839451](img/image-20220602202839451.png)

3.   在 Ubuntu 宿主机下新建目录 /app/redis

     ![image-20220602203059023](img/image-20220602203059023.png)

4.   将一个 redis.conf 文件模板拷贝进 /app/redis 目录下

5.   /app/redis 目录下修改 redis.conf 文件

     ![image-20220602203215253](img/image-20220602203215253.png)

6.   使用 Redis 6.0.8 镜像创建容器（也叫运行镜像）

     >   docker run -p 6379:6379 --name myr3 --privileged=true -v /app/redis/redis.conf:/etc/redis/redis.conf -v /app/redis/data:/data -d redis:6.0.8 redis-server /etc/redis/redis.conf 

     ![image-20220602203618109](img/image-20220602203618109.png)

7.   测试 redis-cli 连接上来

