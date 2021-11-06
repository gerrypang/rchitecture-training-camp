# 模块一作业

## 一、微信业务架构图

![wechat](https://github.com/gerrypang/rchitecture-training-camp/blob/main/part-01/image/wechat.png)


## 二、学生管理系统毕业设计

### 方案一（推荐）

#### 架构图

![plan-1](https://github.com/gerrypang/rchitecture-training-camp/blob/main/part-01/image/plan-1.png)

#### 方案说明

- 语言选择java

- 一台云应用Server，单体服务（ssm+layui），不考虑前后端分离架构

- 两台云数据MySQL（主备模式）

- DNS申请外网域名

#### 优缺点：

优点：方案简单，使用云服务搭建方便快捷，直接可以在提供外网访问。只能够满足毕设中基本要求。

缺点：可用性差

### 方案二

#### 架构图

![plan-2](https://github.com/gerrypang/rchitecture-training-camp/blob/main/part-01/image/plan-2.png)

#### 方案说明

- 语言选择java

- 一台负载均衡Nginx

- 4台应用Server，2台部署前端（vue），2台后端（spring boot）

- 两台数据MySQL（主从模式）

- DNS申请外网域名

#### 优缺点
优点：可用性高，使用云服务，搭建简单，直接可以在提供外网访问。次机构能够满足毕设中基本要求

缺点：相对于学生来说成本更高，复杂性高
