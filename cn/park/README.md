# 目前完成的内容一览表

**内部SVN服务器提交的项目工程** 
* alpaca-park
> park主要工程，包含注册中心、配置中心、Spring Boot Admin Server、Turbine（监控聚合服务）、Zipkin Server（服务跟踪相关）等主要功能
* alpaca-service
> 服务父工程，里面包含一个服务示例service-account
* alpaca-park-common
> 公用的包模块，包含一个logback的xml配置、MyBatis单表实体生成器、一些父类、一些公用VO等
* [alpaca-service-archetype](https://github.com/gstripe/alpaca-service-archetype.git)
> 生成服务工程的原型工具

**alpaca-park工程说明**
* park-admin
> 基于Spring Boot Admin，加入Trubine对聚合数据的显示。
* park-config-server
> 配置中心，基于SVN分发配置文件，目前取消用消息来进行配置变更后的通知更新。
* park-eureka-server
> 注册中心，配置为三台集群，为服务提供注册与发现功能。
* park-gateway
> API网关，提供服务的代理转发工作，目前配置成可以对代理的服务进行重试，熔断功能，添加sleuth，将跟踪信息发往park-zipkin-server
* park-turbine
> 监控聚合服务，聚合所有服务的监控信息，并通过Hystrix Dashboard进行显示
* park-zipkin-server
> 分布式服务跟踪，对服务的请求链路进行记录。
* park-manager
> 目前仅仅只是演示一个服务消费者调用service-account获得Account列表的分页表格功能（基于简单的Bootstrap样式与模板引擎Thymeleaf）

**alpaca-service工程说明**
> 主要提供一个service-account的示例工程，里面主要包含对MyBatis的使用、如果将工程转成一个服务注册到注册中心。

* [从archetype创建服务工程](/cn/park/new_service_project_from_archetype.md)
* [服务工程结构说明](/cn/park/service_project_structure.md)

**服务的部署方式**
* [服务实例包部署安装](/cn/park/service_package_deployment-install.md)

**开发虚拟机环境部署**
![](/cn/park/images/vm_list.png)