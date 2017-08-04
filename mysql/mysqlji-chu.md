##### 登入root用户
    mysql -uroot -p
 
建库
create database tour;
alter database tour character set utf8;
 
登入数据库
use tour;
 
建用户 (%表示登陆者可以是任意ip)
CREATE USER 'dwz_spring'@'%' IDENTIFIED BY 'dwz_spring';
 
授权
grant all privileges on dwz_springmvc.* to 'dwz_spring'@'%' identified by 'dwz_spring';
 
导出
mysqldump -u root -p afternine > G:\微电商\A9\test.sql
 
导入(需使用root用户)
mysql -u root -p swifi < E:\afternine\server\test.sql


--删除用户
Delete FROM mysql.user Where User='swifi ' and Host='localhost';