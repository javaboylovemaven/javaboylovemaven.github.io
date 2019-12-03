---
sidebar:
  nav: docs-zh
title: 6. Maven 依赖管理
tags: Maven
categories: Maven
abbrlink: maven-dependency
date: 2019-10-06 22:28:52
---

## 6. Maven 依赖管理

Maven 项目，如果需要使用第三方的控件，都是通过依赖管理来完成的。这里用到的一个东西就是 pom.xml 文件，概念叫做项目对象模型（POM，Project Object Model），我们在 pom.xml 中定义了 Maven 项目的形式，所以，pom.xml 相当于是 Maven 项目的一个地图。就类似于 web.xml 文件用来描述三大 web 组件一样。

<!--more-->

这个地图中都涉及到哪些东西呢？

### 6.1 Maven 坐标

```xml
<dependencies>
  <dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.11</version>
    <scope>test</scope>
  </dependency>
</dependencies>
```

- dependencies

在 dependencies 标签中，添加项目需要的 jar 所对应的 maven 坐标。

- dependency

一个 dependency 标签表示一个坐标

- groupId

团体、公司、组织机构等等的唯一标识。团体标识的约定是它以创建这个项目的组织名称的逆向域名（例如 org.javaboy）开头。一个 Maven 坐标必须要包含 groupId。一些典型的 groupId 如 apache 的 groupId 是 org.apache.

- artifactId

artifactId 相当于在一个组织中项目的唯一标识符。

- version

一个项目的版本。一个项目的话，可能会有多个版本。如果是正在开发的项目，我们可以给版本号加上一个 SNAPSHOT，表示这是一个快照版（新建项目的默认版本号就是快照版）

- scope

表示依赖范围。

![](http://maven.javaboy.org/assets/images/img/6-1.png "6-1.png")

我们添加了很多依赖，但是不同依赖的使用范围是不一样的。最典型的有两个，一个是数据库驱动，另一个是单元测试。

数据库驱动，在使用的过程中，我们自己写代码，写的是 JDBC 代码，只有在项目运行时，才需要执行 MySQL 驱动中的代码。所以，MySQL 驱动这个依赖在添加到项目中之后，可以设置它的 scope 为 runtime，编译的时候不生效。

单元测试，只在测试的时候生效，所以可以设置它的 scope 为 test，这样，当项目打包发布时，单元测试的依赖就不会跟着发布。

### 6.2 依赖冲突


- 依赖冲突产生的原因

![](http://maven.javaboy.org/assets/images/img/6-2.png "6-2.png")

在图中，a.jar 依赖 b.jar，同时 a.jar 依赖 d.jar，这个时候，a 和 b、d 的关系是直接依赖的关系，a 和 c 的关系是间接依赖的关系。

#### 6.2.1 冲突解决

1. 先定义先使用
2. 路径最近原则（直接声明使用）

以 spring-context 为例，下图中 x 表示失效的依赖（优先级低的依赖，即路径近的依赖优先使用）：

![](http://maven.javaboy.org/assets/images/img/6-3.png "6-3.png")

上面这两条是默认行为。

我们也可以手动控制。手动控制主要是通过排除依赖来实现，如下：


```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.1.9.RELEASE</version>
    <exclusions>
        <exclusion>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

这个表示从 spring-context 中排除 spring-core 依赖。