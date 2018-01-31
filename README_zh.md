dubbo-spring-boot-starter
===================================

[English](https://github.com/alibaba/dubbo-spring-boot-starter/blob/master/README.md)

Dubbo Spring Boot Starter。 

支持jdk版本为1.6或者1.6+

（在修改源码前，请导入googlestyle-java.xml以保证一致的代码格式）

### 如何发布dubbo服务

* 添加依赖:

```xml
    <dependency>
        <groupId>com.alibaba.spring.boot</groupId>
        <artifactId>dubbo-spring-boot-starter</artifactId>
        <version>1.0.0</version>
    </dependency>
```

* 在application.properties添加dubbo的相关配置信息,样例配置如下:

```properties
spring.dubbo.appname=dubbo-spring-boot-starter-provider-test
spring.dubbo.registry=multicast://224.0.0.0:1111
spring.dubbo.protocol=dubbo
```

* 接下来在Spring Boot Application的上添加`@EnableDubboConfiguration`, 表示要开启dubbo功能. (dubbo provider服务可以使用或者不使用web容器)

```java
@SpringBootApplication
@EnableDubboConfiguration
public class DubboProviderLauncher {
  //...
}
```

* 编写你的dubbo服务,只需要添加要发布的服务实现上添加`@Service`（import com.alibaba.dubbo.config.annotation.Service）注解 ,其中interfaceClass是要发布服务的接口.

```java
@Service(interfaceClass = IHelloService.class)
public class HelloServiceImpl implements IHelloService {
  //...
}
```

* 启动你的Spring Boot应用,观察控制台,可以看到dubbo启动相关信息.


### 如何消费Dubbo服务

* 添加依赖:

```xml
    <dependency>
        <groupId>com.alibaba.spring.boot</groupId>
        <artifactId>dubbo-spring-boot-starter</artifactId>
        <version>1.0.0</version>
    </dependency>
```

* 在application.properties添加dubbo的相关配置信息,样例配置如下:

```properties
spring.dubbo.appname=dubbo-spring-boot-starter-consumer-test
spring.dubbo.registry=multicast://224.0.0.0:1111
spring.dubbo.protocol=dubbo
```

* 开启`@EnableDubboConfiguration`

```java
@SpringBootApplication
@EnableDubboConfiguration
public class DubboConsumerLauncher {
  //...
}
```

* 通过`@Reference`注入需要使用的interface.

```java
@Component
public class HelloConsumer {
  @Reference
  private IHelloService iHelloService;
  
}
```

### 参考文档

* dubbo 介绍: http://dubbo.io/
* spring-boot 介绍: http://projects.spring.io/spring-boot/
