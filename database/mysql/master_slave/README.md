https://www.cnblogs.com/gl-developer/p/6170423.html

用法：
1. 先确保主从库都正常安装好
2. 确保datadir下server-uuid唯一，因为有的人习惯直接拷贝
3. 确保主从库的端口不一致
4. 分别将my-master.ini和my-slave.ini拷贝到相应的目录，并且修改为my.ini
5. master提供账号，不细说，直接看链接
```
create user 'servant'@'localhost' identified by '321';
grant replication slave on *.* to 'servant'@'localhost';

show master status; # 查看master的日志文件，及位置
```
6. slave连接到账号，这里不细说，直接看链接
```
CHANGE MASTER TO
  MASTER_HOST='localhost',
  MASTER_USER='servant',
  MASTER_PASSWORD='321',
  MASTER_PORT=3306,
  MASTER_LOG_FILE='mysql-bin.000002',
  MASTER_LOG_POS=617, # 上面master节点的位置
  MASTER_CONNECT_RETRY=10; # 这行非必须

start slave

show slave status\G
```