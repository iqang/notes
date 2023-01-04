![](/Users/elggurts/Downloads/hanhua/notes/InstallationInstructions/mysql/images/mysql-logo.png)

# 创建MySQL的本地目录，并添加配置文件

> MySQL数据需要挂载至宿主机文件目录中，因此需要先创建宿主机的目录和对应的文件

```sh
#创建mysql的目录
mkdir -p /opt/docker/mysql/log /opt/docker/mysql/data /opt/docker/mysql/conf /opt/docker/mysql/mysql-files

#创建mysql的配置文件
touch /opt/docker/mysql/conf/my.cnf

#复制配置文件内容到创建的mysql文件中
```

```tex
[mysqld]
user=mysql
character-set-server=utf8mb4
default_authentication_plugin=mysql_native_password
secure_file_priv=/var/lib/mysql
expire_logs_days=7
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
max_connections=1000
 
[client]
default-character-set=utf8mb4
 
[mysql]
default-character-set=utf8mb4

```



# 启动MySQL容器

```shell
# 根据实际情况修改开放端口和mysql账户的密码信息
docker run -d -p 3306:3306 --name mysql -v /opt/docker/mysql/log:/var/log/mysql -v /opt/docker/mysql/data:/var/lib/mysql -v /opt/docker/mysql/conf/my.cnf:/etc/mysql/my.cnf -v /opt/docker/mys
ql/mysql-files:/var/lib/mysql-files -e MYSQL_ROOT_PASSWORD=Mysql@openwrt mysql
```



# 配置MySQL远程访问

1. 进入mysql容器的交互命令行

   ```sh
   docker exec -it mysql /bin/bash 
   ```

   

2. 登录mysql服务器

   ```
   mysql -uroot -pMysql@openwrt
   ```

   

3. 执行sql语句

   ```sql
   use mysql;
   alter USER 'root'@'localhost' IDENTIFIED BY 'Mysql@openwrt';
   update user set host = "%" where user='root';
   ```

   

4. 刷新权限

   ```sql
   flush privileges;
   ```