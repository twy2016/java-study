# SpringBoot(1)SpringBoot入门

# SpringBoot学习笔记（一）：入门篇

> 本文介绍springboot的简单入门

### 一、springboot的优点

1. 使用Java开发基于Spring的应用程序非常容易。
2. 开箱即用，有自己自定义的配置就是用自己的，没有就使用官方提供的默认的。
3. 避免了编写大量的样板代码，注释和XML配置。
3. 提供嵌入式HTTP服务器，如Tomcat，Jetty等，以开发和测试Web应用程序非常容易。

### 二、springboot的简单搭建
1.使用idea新建项目

![1570549187669-8e74f1d7-ffd8-4ce0-b5e1-7178cf6346c5](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/1570549187669-8e74f1d7-ffd8-4ce0-b5e1-7178cf6346c5.jpeg)

![1570549187547-23d92b3b-9345-41b4-ace1-cd65e004936b](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/1570549187547-23d92b3b-9345-41b4-ace1-cd65e004936b.jpeg)

2.选择Spring Web
![1570549187552-fafab87e-b4d0-4006-9675-97b5ec18cbea](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/1570549187552-fafab87e-b4d0-4006-9675-97b5ec18cbea.jpeg)

3.编写一个HelloWorld

```java
package com.twy.springbootdemo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
    
    @GetMapping("/hello")
    public String hello() {
        return "hello springboot!";
    }
}
```

3.测试
![](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/1570549187719-c5a4b18f-3bf0-4ed5-bf6f-336812551d89.jpeg)

### 三、@SpringBootApplication核心注解


- springboot需要一个启动类，该类必须在所有的包最外层

```java
package com.twy.springbootdemo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SpringbootDemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootDemoApplication.class, args);
    }

}
```

`@SpringBootApplication`注解


```java
@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited				 
@SpringBootConfiguration //表示当前为注解类
@EnableAutoConfiguration //开启springboot的注解功能
@ComponentScan(			 //扫描路径
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication 
...
}
```

#### @ComponentScan(扫描加载bean)

配置组件扫描的指令

- 组件扫描，可自动发现和装配Bean，功能其实就是是

- 我们可以通过basePackages等属性来细粒度的定制`@ComponentScan`自动扫描的范围，如果不指定，则默认Spring框架实现会从声明`@ComponentScan`所在类的package进行扫描。

- 默认扫描SpringApplication的run方法里的Booter.class所在的包路径下文件，所以最好将该启动类放到根包路径下。

#### @EnableAutoConfiguration(开启自动配置)

开启自动配置

简单概括一下就是，是借助`@Import`的帮助，收集和注册特定场景相关的 bean 定义。

最关键的要属 @Import(AutoConfigurationImportSelector.class)，借助 AutoConfigurationImportSelector，@EnableAutoConfiguration 可以帮助 SpringBoot 应用将所有符合条件的 @Configuration 配置都加载到当前 SpringBoot 创建并使用的 IoC 容器。

![image-20210223232427677](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/image-20210223232427677.png)

![image-20210223233143369](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/image-20210223233143369.png)

![image-20210223233226099](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/image-20210223233226099.png)

![image-20210223233304391](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/image-20210223233304391.png)

![image-20210223233557160](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/image-20210223233557160.png)

![image-20210223233634501](https://image-twy2018.oss-cn-hangzhou.aliyuncs.com/note/image-20210223233634501.png)

#### @SpringBootConfiguration(标记当前类为配置类)

`@SpringBootConfiguration`本质就是`@Configuration`，`@Configuration` 这个注解的作用就是声明当前类是一个配置类，然后Spring会自动扫描到添加了@Configuration的类，读取其中的配置信息，而@SpringBootConfiguration是来声明当前类是SpringBoot应用的配置类，项目中只能有一个。




