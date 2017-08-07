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
    
    
##### 查询重复的数据

    //模版
    select 字段1,字段2, count(*) from 表名 group by 字段1,字段2 having count(*) > 1
    
    //查询重复的数据
    Select owner from dba_tables group by owner having count(*)>1;
    //查询出没有重复的数据
    Select owner from dba_tables group by owner having count(*)=1;

##### 删除重复的数据
**方法1：**
直接删除
               
    //效率低，不适合大数据量
    delete from 表名 a where 字段1,字段2 in (select 字段1,字段2,count(*) from 表名 group by 字段1,字段2 having count(*) > 1) 

**方法2：**
先将查询到的重复的数据插入到一个临时表中，然后再进行删除

    //建临时表，将查询到的数据插入其中
    CREATE TABLE 临时表 AS 
    ( 
        select 字段1,字段2, count(*) as row_num 
        from 表名 
        group by 字段1,字段2 
        having count(*) > 1 
    );
    
    //删除重复数据
    delete from 表名 a where 字段1,字段2 in (select 字段1，字段2 from 临时表);














    