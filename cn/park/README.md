# 目前完成的内容一览表

**内部SVN服务器提交项目工程** 
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
* park-config-server
* park-eureka-server
* park-gateway
* park-turbine
* park-zipkin-server

**alpaca-service工程说明**
* [从archetype创建服务工程](/cn/park/new_service_project_from_archetype.md)
* [服务工程结构说明](/cn/park/service_project_structure.md)

**服务的部署**
* [服务实例包部署安装](/cn/park/service_package_deployment-install.md)