#### 云相关概念

![](../image/cloud/云计算的组成.png)

#### LAAS 

基础设施即服务

1. 计算与网络
  - 云服务器CVM
  - 私有网络VPC
  - 负载均衡CLB
  - 云数据库CDB
2. 存储与内容分发
  - 对象存储COS
  - 内容分发网络CDN
3. 数据库
  - 云数据库CDB
  - 云存储Redis
  - 云缓存Memcached

#### PAAS

平台即服务
1. 音视频方案、消息推送

#### SAAS

软件即服务
1. 云盘、在线文档协作

#### CDN(Content Delivery Network)

内容分发网路,通过分布在全球各地的机房为用户提供就近接入

**CDN调度原理:**

DNS,域名系统。通过主机名，最终得到该主机名对应的IP地址

![](../image/cloud/CDN原理.png)


#####GSLB(Global Server Load Balancing)技术
全球服务器负载均衡，用于灾备和路由优化



#### COS(Cloud Object Storage)

面向厂商和开发者的网络硬盘，替代传统服务器硬盘和数据存放方式的存储解决方案

#### BGP(Border Gateway Protocol) 边界网关协议

用来连接 Internet 上的独立系统的路由选择协议

**应用：**

1. 为运营商之间的互联提供了稳定而安全的路由协议 
2. 自主网络系统中网关之间交换器路由信息的协议，互联网的网关之间

#### 负载均衡
- SLB(server load balancing) 
- CLB(client load balancing)
##### SLB
服务器负载均衡，负载均衡算法：
- WRR(weighted round robin)：加权轮询算法分配连接。
- WLC(weighted least connections)：通过一定的权值，将下一个连接分配给活动连接数少的服务器。
##### CLB
客户负载均衡，采用一致性hash算法，映射到服务节点。
##### F5
硬件，直接通过智能交换机实现。
##### NGINX
软负载，采用反向代理技术。

#### 云服务器弹性计算服务 ECS
ECS(elastic compute service) 是一种弹性可伸缩的计算服务。

#### 地址转换 NAT

##### SNAT
源地址转换，其作用是将IP数据包的源地址转换成另外一个地址。
源地址转换即将内网地址向外网访问时，发起访问的内网IP地址转换为指定的IP地址(可指定具体的服务以及相应的端口或端口范围)，这可以使内网中使用保留IP地址的主机访问外部网络，即内网的多部主机可以通过一个有效的公网IP地址访问外部网络。

##### DNAT

