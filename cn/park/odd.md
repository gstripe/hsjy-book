### CentOS 相关操作
* .sh 赋予执行权限
```
chmod a+x startall.sh
```

### JHipster 学习

JHipster Quick Start

* Install JHipster **yarn global add generator-jhipster**
* Create a new directory and go into it **mkdir myApp && cd myApp**
* Run JHipster and follow instructions on screen **jhipster**
* Model your entities with [JDL Studio](http://www.jhipster.tech/jdl-studio/) and download the resulting **jhipster-jdl.jh** file
* Generate your entities with **jhipster import-jdl jhipster-jdl.jh**
* \* Assuming you have already installed [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html), [Git](http://git-scm.com/), [Node.js](http://nodejs.org/), [Yarn](https://yarnpkg.com/en/docs/install) and [Yeoman](http://yeoman.io/learning/index.html). For AngularJS 1, you will also need [Bower](http://bower.io/#install-bower) and [Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md)

good4you

在线创建应用
> https://start.jhipster.tech

## Spring框架中的设计模式学习

### 创建模式三剑客和1个行为模式

#### 解释器设计模式
在编程中，分析一件事情，并决定它是什么意思。
此模式基于表达式和评估器部分

#### 建设者模式
创建对象模式之一
简化复杂对象的创建，构建器背后隐藏了对象构造的复杂性
org.springframework.beans.factory.support.BeanDefinitionBuilder

#### 工厂方法
创建对象模式之一
通过公用静态方法对象进行初始化
public static Welcomer createWelcomer(MessageLocator messagesLocator)

#### 抽象工厂
抽象的工厂设计模式，看起来类似于工厂方法。不同之处在于，我们可以将抽象工厂视为这个词的工业意义上的工厂，即。作为提供所需对象的东西。工厂部件有：抽象工厂，抽象产品，产品和客户。更准确地说，抽象工厂定义了构建对象的方法。抽象产品是这种结构的结果。产品是具有同样结构的具体结果。客户是要求创造产品来抽象工厂的人。
org.springframework.beans.factory.BeanFactory

### 策略和模板方法

#### 代理模式
代理就像对象的镜像一样。所以它不仅可以覆盖真实对象，还可以扩展其功能。
可以通过代理来定义第二个对象的调用。
代理是封装真实对象的对象。
例子：org.springframework.aop.framework.ProxyFactoryBean
该工厂根据Spring bean构建AOP代理
getObject()返回实例的AOP代理

#### 复合模式
基于具有共同行为的多个对象的存在，用于构建更大的对象。
较大的对象仍然具有与最小对象相同的特征。那么用它来定义相同的行为。
在Spring世界中，我们检索复合对象的概念是org.springframework.beans.BeanMetadataElement接口
** _TODO 那一段解释看不懂_ **

#### 策略模式

#### 模板模式