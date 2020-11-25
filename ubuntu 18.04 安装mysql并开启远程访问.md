## ubuntu 18.04 安装mysql并开启远程访问

1.直接采用apt 安装

```
apt install mysql-server
```

2.进入设置目录,打开设置文件

```
cd /etc/mysql/	mysql.conf.d
vim mysql.conf
```

将其中的bind-address = 127.0.0.1注销(前面加#号)

3.打开mysql(先切换到root用户)

```
mysqll -u root -p
```

提示输入密码,直接回车就进入了(因为root用户进入不需要密码)

```
use mysql;
```

```
update user set authentication_string=password("密码"),plugin='mysql_native_password' where user='root';
```

```
grant all privileges on *.* to 'root'@'%' identified by 'password';
```

```
select host,user from user;
```


如果出现2个root用户,如下图(1),如果没有直接

```
exit;
```

```
service mysql restart
```


图(1)

![image-20201019174045558](C:%5Cworkshop%5C%E5%B7%A5%E4%BD%9C%E7%AC%94%E8%AE%B0-%E8%AE%B0%E5%BD%95%20markdown%20Typora%5Cimages%5Cimage-20201019174045558.png)

需要删除**localhost**那个

```
delete from user where user='root' and host='localhost';
```

