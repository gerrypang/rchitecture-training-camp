# 模块二作业：分析微信朋友圈高性能复杂度

## 微信朋友圈功能分析

![微信朋友圈功能](H:\rchitecture-training-camp\part-02\image\微信朋友圈功能.png)



## 分析微信朋友圈复杂度

![复杂度](H:\rchitecture-training-camp\part-02\image\复杂度.png)

![发朋友圈1](H:\rchitecture-training-camp\part-02\image\发朋友圈1.png)



![查看朋友圈1](H:\rchitecture-training-camp\part-02\image\查看朋友圈1.png)



## 架构设计方案

### 发朋友圈设计方案

设计理由：

- 负载均衡：可以从不同层级进行考虑四层选择LVS，七层选择Nginx

- 网关层：需要考虑到身份认证，黑名单，服务路由功能可以选择spring gateway

- 服务层：服务注册与发现负责服务间的治理，选择 Nacos

- 数据代理层：由于要满足集群计算高性能和存储高性，这里选择了对数据库分库分表，对于分库分表选择Sharding-JDBC

- 存储层：

  - 1）发朋友圈主要存在三种形式（文字，视频，图片），对于文字我们可以直接存储MySQL，并缓存到Redis-Cluster。
  - 2）对于视频和图片需要我们做单独的分布式文件存储这里选择Fast DFS能够满足基本分布式文件存储需求。
  - 3）此外发送朋友圈后，需要将最新信息推送我的好友，对于这种异步消息，可以考虑MQ消息服务，选择kafka集群

  ![发朋友圈](H:\rchitecture-training-camp\part-02\image\发朋友圈.png)

### 查看友圈设计方案

设计理由：

与发朋友圈不同点在存储层：

- 1）对于近期发送的朋友圈（热数据）查询选择通过redis方式，提升查询性能
- 2）对于历史发送朋友圈（冷数据）查询选择通过MySQL方式查询。

![查看朋友圈](H:\rchitecture-training-camp\part-02\image\查看朋友圈.png)

### 单机房部署方案

![image-20211107003815658](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211107003815658.png)





参考资料

http://www.woshipm.com/evaluating/202916.html

https://www.jianshu.com/p/977404888afd

https://juejin.cn/post/6844903601588928520

