##### 登入root用户
    mysql -uroot -p
 
##### 建库
    create database onecard;
    alter database onecard character set utf8;
 
##### 登入数据库
    use tour;
 
##### 建用户 (%表示登陆者可以是任意ip)
    CREATE USER 'onecard'@'%' IDENTIFIED BY 'onecard';
 
##### 授权
    grant all privileges on onecard.* to 'onecard'@'%' identified by 'onecard';
 
##### 导出
    mysqldump -u root -p onecard > C:\test.sql
 
##### 导入(需使用root用户)
    mysql -u root -p onecard < C:\test.sql

##### 删除用户
    Delete FROM mysql.user Where User='onecard' and Host='localhost';