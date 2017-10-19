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

#### 某架构

##### 整体架构图
![](/resources/images/architecture/1/3.1.服务层架构.png)

1. 客户端
	
  DNS劫持: HttpDNS   LocalDNS	
  CDN加速: 静态资源（js、css 、image）
  客户端缓存:  HTTP头设置  Cache-Control
  服务降级： 网络高峰时减少非关键服务的请求
  网络质量检测: 按客户不同网络环境设置超时参数、服务并发数、产品体验（image质量）


2. 入口
智能DNS分发流量,制定策略,按地域切分
DDOS防护
SLB负载均衡
Nginx+Lua反向代理、分流限流、AB测试、灰度发布、故障切换、服务降级

3. 网关：
安全控制：身份认证、数据加密
分流与限流：按业务分流，设定阀值

4. 服务层：

5. 缓存层:
图片

6. 数据层：
不同数据中心   专线


