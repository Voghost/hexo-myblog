---
title: spring 框架 (spring5)

date: 2020-11-18 15:28:02

cover: https://oss.ghovos.top/hexo/myblog/spring/spring5-study/1-06-01.png

mathjax: true

categories: 
	- spring
	- spirng5 框架

tags: 
	- spring
	- spring5

---

## 1. Spring 概念
### 1.1 轻量、开源
### 1.2 解决企业应用开发的复杂性
### 1.3 核心 `IOC` 和 `AOP`
1. `IOC`: 控制反转，把创建对象过程交给Spring进行管理
2. `Aop`: 面向切面，不修改源代码进行功能增强 

### 1.4 特点
1. 方便解耦、简化开发
2. Aop编程支持
3. 方便程序测试
4. 方便集成各种优秀框架
5. 方便事物操作 ...

<!--more-->
### 1.5 入门案例
1. 下载 spring5 的jar包
	* 下载地址: [repo.spring.io/release/org/springframework/spring](https://repo.spring.io/release/org/springframework/spring/)
2. idea 新建java普通项目并导入相关包(基础)<br/>
<img width=60%  src="https://oss.ghovos.top/hexo/myblog/spring/spring5-study/1-06-01.png"/>
<img width=60%  src="https://oss.ghovos.top/hexo/myblog/spring/spring5-study/1-06-02.png"/><br>
3. 创建一个普通类 `User`

```java
package top.ghovos.spring5;

public class User {
    public void add(){
        System.out.println("add ......");
    }
}
```

4. 创建配置文件`bean1.xml` 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--配置User类对象创建-->
    <bean id="user" class="top.ghovos.spring5.User"></bean>
</beans>
```
5. 创建测试类 `TestSpring5`

```java
package top.ghovos.spring5.testdemo;

import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import top.ghovos.spring5.User;

public class TestSpring5 {
    @Test
    public void testAdd(){
        //1 加载配置文件
        ApplicationContext context=new ClassPathXmlApplicationContext("bean1.xml");

        //2 获取配置创建的对象
        User user = context.getBean("user", User.class);

        System.out.println(user);
        user.add();
    }
}
```

6. 各个文件的关系<br>
<img src="https://oss.ghovos.top/hexo/myblog/spring/spring5-study/1-06-03.png" width=60%/>


## 2. IOC 容器
### 2.1 IOC 底层原理
1. xml解析、工厂模式、反射
    1. 配置xml文件

    ```xml
    <bean id="dao" class="top.ghovos.spring5.User"></bean>
    ```
    2. 有seriece类和dao类，创建`工厂类`

    ```java
    //创建工厂类
    class UserFactory{
    public static UserDao getDao(){
        String classValue = class属性值; //1. 通过xml解析
        Class clazz = Class.forName(classValue); //2. 通过反射创建对象
        return (UserDao)clazz.newInstance(); //初始化对象并返回
        }
    }
    ```
### 2.2 IOC 接口(BeanFactory)
#### 1. IOC思想基于IOC容器完成，IOC容器底层就是**对象工厂**

#### 2. Spring 提供IOC容器实现的两种方式
1. `BeanFactory` : IOC容器的基本实现，是Spring内部的使用接口，不提供开发人员使用
    * 加载配置文件的时候不会创建对象，对象使用才会创建对象
2. `ApplicationContext` BeanFactory 的子接口，提供更多强大的功能,一般由开发人员使用
    * 加载配置文件时就会创建对象
3. ApplicationContext 接口有实现类

### 2.3 IOC 操作Bean管理(基于xml)
#### 1. 什么是Bean管理
1. Bean 管理只两个操作
    1. sping 创建对象
    2. spirng 注入属性 (如: getter 或 setter)

#### 2. Bean 管理的操作两种方式
1. 基于xml配置文件方式
    * DI: 依赖注入， 就是注入属性
    1. 创建对象

    ```xml
    <bean id = "user" class = "top.ghovos.spring5.Book" name=""><bean>
        <!--id: 唯一标识-->
        <!--class: 类全路径(包类路径)-->
        <!-- 创建对象时候，默认也是**无参数构造**方法完成对象创建-->
    ```
    2. 用set方式主语注入属性

    ```java
    // 1. 使用set方式注入
    public void setBook(String bName){
        this.bName=bName;
    }

    public void setBookAuthor(String bAuthor){
        this.bAuthor=bAuthor;
    }
    ```
    ```xml
     <!--配置User对象-->
    <bean id="book" class="top.ghovos.spring5.Book">
        <!--使用property完成属性注入-->
        <!--注意 用property 要完成**上面** set方法(只能是set方法) 后配置-->
        <property name="bName" value="someBook"></property>
        <property name="bAuthor" value="someOne"></property>
        <!--
        name: 属性名称
        value：属性值
        -->
    </bean>
    ```

    3. 使用有参构造方式注入

2. 基于注解方式方式

### 2.4 IOC 操作Bean管理(基于注解)


## 3. Aop
## 4. JdbcTemplate
## 5. 事务管理
## 6. Spring 5 新特性
