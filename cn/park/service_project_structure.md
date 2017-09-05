# 服务工程结构说明

## 项目结构预览

![](/cn/park/images/service_project_structure.png)

## 项目结构详解

* ### ServiceMainApplication
> Spring Boot 应用启动类
    
    ```
    @EnableSwagger2Doc // 默认使用swagger做为api文档
    @EnableDiscoveryClient // 默认为一个服务实例
    @SpringBootApplication // 一个SpringBoot应用的固定声明
    @MapperScan("alpaca.service.example.mapper") // 扫描Mybatis Mapper
    public class ServiceMainApplication {
    
        // 通过java -jar xxx.jar 启动服务
        public static void main(String[] args) {
            SpringApplication.run(ServiceMainApplication.class, args);
        }
    }
    ```




    