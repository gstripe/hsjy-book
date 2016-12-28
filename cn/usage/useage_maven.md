# Maven 使用

## settings.xml配置

* 首先创建用户目录下的.m2目录与本地仓库地址

  ```
  # 通过命令行方式，进入Window用户目录
  cd %HOMEPATH%
  # 创建.m2目录
  mkdir .m2
  # 创建本地仓库目录
  # 在dev4j目录下创建 repo 目录
  ```

* 复制settings.xml文件到.m2目录中修改，不建议直接修改原目录下的配置文件

* 配置本地仓库目录路径

  ![](/cn/usage/images/dev4j_mvn_settings_localRepository.png)

  > 打开.m2目录下的settings.xml，在localRepository下加入`<localRepository>C:\dev4j\repo</localRepository>`
  >
  > 注: C:\dev4j\repo为你本地仓库地址

* 配置私服地址

  ```
  <!--在mirros下加入以下配置片段 -->
  <mirror>
      <id>icsshs-nexus</id>
      <mirrorOf>*</mirrorOf>
      <name>ICSSHS Nexus</name>
      <url>http://10.188.180.195:8081/nexus/content/groups/public/</url>
  </mirror>
  ```

* 测试一下,命令行下执行一下mvn help:system命令看看都打印了什么  
  ![](/cn/usage/images/dev4j_mvn_help!system.png)

  > 从配置的私服里面下载所需要的依赖包,如果没有配置会从中央仓库进行下载,正常情况下要很久很久.
  >
  > 直到显示BUILD SUCCESS后说明配置无问题.
  >
  > 同时,可以看到本地仓库目录里保存的从私服下载下来的依赖包.

## 基础用法

* 创建项目骨架

  ```
  mvn archetype:generate -DgroupId=com.icsshs.demo.mvn -DartifactId=mvn-ch01 -Dversion=0.0.1-SNAPSHOT -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false -DarchetypeCatalog=internal
  ```

* 编译

  ```
  mvn compile
  ```

* 测试

  ```
  mvn test
  ```

* 清空

  ```
  mvn clean
  ```

* 打包

  ```
  mvn package
  ```

* 运行

  ```
  java -cp target/mvn-ch01-0.0.1-SNAPSHOT.jar com.icsshs.demo.mvn.App
  ```

## 发布

* 发布到本地仓库

  ```
  mvn install
  ```

* 发布到远程仓库

  ```
  mvn deploy
  ```

## 配置远程仓库\(连到nexus私服\)

1. settings.xml里配置用户/密码

   ```
   <!-- servers下进行配置，这里配置snapshot。icsshs为测试账号。-->
   <server>
       <id>icsshs-snapshot</id>
       <username>jydemo</username>
       <password>jydemo</password>
   </server>
   ```

2. 项目中的pom.xml配置release和snapshot仓库地址

   ```
   <!-- properties nexus -->
   <sonatype.nexus.baseurl>http://10.188.180.195:8081/nexus</sonatype.nexus.baseurl>

   <!-- distributionManagement -->
   <distributionManagement>
       <repository>
           <id>icsshs-release</id>
           <name>Release</name>
           <url>${sonatype.nexus.baseurl}/content/repositories/releases/</url>
       </repository>
       <snapshotRepository>
           <id>icsshs-snapshot</id>
           <name>Snapshot</name>
           <url>${sonatype.nexus.baseurl}/content/repositories/snapshots/</url>
       </snapshotRepository>
   </distributionManagement>
   ```

## settings-security.xml

用户/密码配置为非明文方式

