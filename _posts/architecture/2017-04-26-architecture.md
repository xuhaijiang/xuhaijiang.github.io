---
layout: post
title: 某电商架构
date: 2017-04-26 17:33:17 +0800
category : 技术文档
tag :
- java
- 架构设计
---
* content
{:toc}

#### 整体架构图

![](/resources/images/architecture/1/3.1.服务层架构.png)

#### 客户端

  DNS劫持: HttpDNS、LocalDNS	
  CDN加速: 静态资源（js、css 、image）
  客户端缓存:  HTTP头设置  Cache-Control
  服务降级： 网络高峰时减少非关键服务的请求
  网络质量检测: 按客户不同网络环境设置超时参数、服务并发数、产品体验（image质量）
  
#### 入口层

![](/resources/images/architecture/1/2.入口层架构.png)	

#### 网关层

安全控制：身份认证、数据加密
分流与限流：按业务分流，设定阀值

#### 服务层

![](/resources/images/architecture/1/3.1.服务层架构.png)
![](/resources/images/architecture/1/3.2.服务层过程调用.png)

#### 缓存层


![](/resources/images/architecture/1/4.1.缓存层架构-游览记录.png)
![](/resources/images/architecture/1/4.2.缓存层架构-列表数据.png)
![](/resources/images/architecture/1/4.3.缓存层架构-订单数据.png)

#### 数据层

不同数据中心 专线


