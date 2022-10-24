# 微服务组件（SpringCloudAlibaba）
目前SpringCloud已经是Java实现微服务架构的事实标准，在此基础上，阿里巴巴开源了SpringCloudAlibaba。替换了一些组件的实现，使用起来更方便、稳定，因此我们采用Alibaba这一套框架进行学习。

|名称|SpringCloud|SpringCloudAlibaba|
|--|--|--|
|注册中心|Eureka、Consul|Nacos|
|配置中心|SpringCloud Config|Nacos|
|网关|SpringCloud Zuul|SpringCLoud Gateway|
|负载均衡|Ribbon|LoadBalancer|
|熔断降级|Hysrix|Sentinel|
|服务调用|Feign|OpenFeign|

## 注册中心
### 一些概念
- 服务发现：比如服务A调用服务B，服务B负载过高时，需要再加一个节点，怎么让服务A发现这个新的服务B节点，这个过程就叫服务发现。  
- 服务注册：服务在启动时，向“注册中心”注册自己，建立一条ServiceName -> ip:port 的映射关系
- 注册中心：负责维护ServiceName -> ip:port列表的维护，同时与服务建立长链接，主动推送节点状态变更

### Nacos
Nacos本身是阿里巴巴开源的一个配置中心，其名字取自：Name and Config Service首字母。从[官网首页](https://nacos.io/zh-cn/index.html)就能发现它的核心功能在于：服务发现、配置管理。  

![NacosHome](./static/Nacos-Home.png)

本文主要参考文档：
- [Nacos架构](https://nacos.io/zh-cn/docs/architecture.html)  
- [SpringCloudAlibaba-服务注册与发现](https://spring-cloud-alibaba-group.github.io/github-pages/2021/zh-cn/index.html#_spring_cloud_alibaba_nacos_discovery)

这里仅简单列举

#### 快速启动单机测试
采用容器方式快速启动单机测试，具体见[NacosDocker](https://nacos.io/zh-cn/docs/quick-start-docker.html)。  

“配置管理”，可以将项目中的application.properties迁移到这里，做集中配置管理，这是Nacos最开始的功能。  
“服务管理”负责承担注册中心的职责。  

![Nacos](./static/Nacos-Preview1.png)

### 服务注册/发现: Nacos Discovery
