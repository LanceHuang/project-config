https://www.cnblogs.com/gl-developer/p/6170423.html

�÷���
1. ��ȷ�����ӿⶼ������װ��
2. ȷ��datadir��server-uuidΨһ����Ϊ�е���ϰ��ֱ�ӿ���
3. ȷ�����ӿ�Ķ˿ڲ�һ��
4. �ֱ�my-master.ini��my-slave.ini��������Ӧ��Ŀ¼�������޸�Ϊmy.ini
5. master�ṩ�˺ţ���ϸ˵��ֱ�ӿ�����
```
create user 'servant'@'localhost' identified by '321';
grant replication slave on *.* to 'servant'@'localhost';

show master status; # �鿴master����־�ļ�����λ��
```
6. slave���ӵ��˺ţ����ﲻϸ˵��ֱ�ӿ�����
```
CHANGE MASTER TO
  MASTER_HOST='localhost',
  MASTER_USER='servant',
  MASTER_PASSWORD='321',
  MASTER_PORT=3306,
  MASTER_LOG_FILE='mysql-bin.000002',
  MASTER_LOG_POS=617, # ����master�ڵ��λ��
  MASTER_CONNECT_RETRY=10; # ���зǱ���

start slave

show slave status\G
```