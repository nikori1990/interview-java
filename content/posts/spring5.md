---
title: "Spring5"
date: 2021-03-26T11:17:51+08:00
---

### Spring 框架概述

1. Spring 是轻量级的开源的 JavaEE 框架
2. Spring 可以解决企业应用开发的复杂性
3. Spring 有两个核心部分： IOC 和 AOP
    * IOC: 控制反转， 把创建对象的过程交给Spring进行管理
    * AOP: 面向切面， 不修改源代码进行功能增强
4. Spring 特点
    * 方便解耦
    * AOP编程支持
    * 方便程序测试
    * 方便和其他框架进行整合
    * 方便进行事物操作
    * 降低API开发难度


> IOC （概念和原理）
1. 什么是IOC
    * 控制反转， 把对象创建和对象之间的调用过程，交给Spring进行管理
    * 使用IOC目的， 为了耦合度降低

2. IOC底层原理
    * xml 解析
    * 工厂模式
    * 反射

> Spring 提供 IOC 容器实现两种方式： （两个接口）
1. BeanFactory 
```
IOC 容器基本实现，是Spring内部的使用接口，不提供开发人员进行使用
接口加载配置文件的时候不会创建对象，在获取（使用）对象时才会去创建对象
```
2. ApplicationContext
```
BeanFactory接口的子接口，提供更多更强大的功能，一般由开发人员进行使用
加载配置文件的时候创建对象
```
3. ApplicationContext 接口的实现类
    * FileSystemXmlApplicationContext 全路径
    * ClassPathXmlApplicationContext  相对项目路径

> IOC 操作 Bean 管理
1. 什么是Bean管理
    * Bean 管理指的是两个操作
        1. Spring 创建对象
        2. Spring 注入属性
    * Bean 管理操作有两种方式
        1. 基于xml配置文件方式实现
        2. 基于注解方式实现 

    > 基于 xml 方式创建对象 
    ```
        <bean id="user" class="cn.nikori.User"></bean>
    ```
 
    * bean 标签有很多属性，常用的属性： id 唯一标识， class 类全路径（包类路径）
    * 创建对象时候，默认也是执行无参构造方法完成对象创建

    > 基于 xml 方式注入属性
    1. DI: 依赖注入， 就是注入属性
    
