---
sidebar:
  nav: docs-zh
title: 5. IDEA 中使用 Maven
tags: Maven
categories: Maven
abbrlink: maven-idea
date: 2019-10-05 22:28:52
---

## 5. IDEA 中使用 Maven

不同于 Eclipse，IDEA 安装完成后，就可以直接使用 Maven 了。

<!--more-->

### 5.1 Maven 相关配置

IDEA 中，Maven 的配置在 `File->Settings->Build,Execution,Deployment->Build Tools->Maven`:

![](http://maven.javaboy.org/assets/images/img/5-1.png "5-1.png")

### 5.2 JavaSE 工程创建

首先在创建一个工程时，选择 Maven 工程：

![](http://maven.javaboy.org/assets/images/img/5-2.png "5-2.png")

如果勾选上 Create from archetype ，则表示可以根据一个项目骨架（项目模板）来创建一个新的工程，不过，如果只是创建 JavaSE 项目，则不用选择项目骨架。直接 Next 即可。然后填入项目的坐标，即 groupId 和 artifactId。

![](http://maven.javaboy.org/assets/images/img/5-3.png "5-3.png")

填完之后，直接 Next 即可。这样，我们就会获取一个 JavaSE 工程，项目结构和你用命令创建出来的项目一模一样。

![](http://maven.javaboy.org/assets/images/img/5-4.png "5-4.png")

### 5.3 JavaWeb 工程创建

在 IDEA 中，创建 Maven Web 项目，有两种思路：

- 首先创建一个 JavaSE 项目，然后手动将 JavaSE 项目改造成一个 JavaWeb 项目
- 创建项目时选择项目骨架，骨架就选择 webapp

两种方式中，推荐使用第一种方式。

#### 5.3.1 改造 JavaSE 项目

这种方式，首先创建一个 JavaSE 项目，创建步骤和上面的一致。

项目创建完成后，**首先修改 pom.xml ，配置项目的打包格式为 war 包。** 这样，IDEA 就知道当前项目是一个 Web 项目：

![](http://maven.javaboy.org/assets/images/img/5-5.png "5-5.png")

然后，选中 JavaSE 工程，右键单击，选择 Open Module Settings，或者直接按 F4，然后选择 Web，如下图：

![](http://maven.javaboy.org/assets/images/img/5-6.png "5-6.png")

接下来，在 webapp 目录中，添加 web.xml 文件。

![](http://maven.javaboy.org/assets/images/img/5-7.png "5-7.png")

**注意，一定要修改 web.xml 文件位置：**

![](http://maven.javaboy.org/assets/images/img/5-8.png "5-8.png")

配置完成后，点击 OK 退出。

项目创建完成后，接下来就是部署了。

部署，首先点击 IDEA 右上角的 Edit Configurations：

![](http://maven.javaboy.org/assets/images/img/5-9.png "5-9.png")

然后，配置 Tomcat：

![](http://maven.javaboy.org/assets/images/img/5-10.png "5-10.png")

![](http://maven.javaboy.org/assets/images/img/5-11.png "5-11.png")

接下来选择 Deployment 选项卡，配置要发布的项目：

![](http://maven.javaboy.org/assets/images/img/5-12.png "5-12.png")

![](http://maven.javaboy.org/assets/images/img/5-13.png "5-13.png")

最后，点击 IDEA 右上角的三角符号，启动项目。

![](http://maven.javaboy.org/assets/images/img/5-14.png "5-14.png")

#### 5.3.2 通过 webapp 骨架直接创建

这种方式比较简单，基本上不需要额外的配置，项目创建完成后，就是一个 web 项目。只需要我们在创建项目时，选择 webapp 骨架即可。

![](http://maven.javaboy.org/assets/images/img/5-15.png "5-15.png")

选择骨架之后，后面的步骤和前文一致。

项目创建成功后，只有 webapp 目录，这个时候，自己手动创建 java 和 resources 目录，创建完成后，右键单击，选择 Mark Directory As，将 java 目录标记为 sources root，将 resources 目录标记为 resources root 即可。

**凡是在 IDEA 右下角看到了 Enable Auto Import 按钮，一定点一下**