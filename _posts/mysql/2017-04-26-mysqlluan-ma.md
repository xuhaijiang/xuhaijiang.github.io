---
layout: post
title: mysql - 编码
date: 2017-04-26 17:33:17 +0800
category : 技术文档
tag :
- mysql
---
* content
{:toc}


#### mysql乱码
##### 解决方法如下:

- 修改字符编码
        SHOW VARIABLES LIKE 'character_set_%';
- 修改数据库成utf8的
        alter database vteam character set utf8;
- 修改表默认用utf8
        alter table type character set utf8;
- 修改字段用utf8
        alter table type modify type_name varchar(50) CHARACTER SET utf8;

#### 新建数据库时指定
        create database name character set utf8;