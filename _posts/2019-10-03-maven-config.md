---
sidebar:
  nav: docs-zh
title: 3. Maven 配置
tags: Maven
categories: Maven
abbrlink: maven-config
date: 2019-10-03 22:28:52
---

## 3. Maven 配置

实际上，没有特殊需求的话，安装好之后直接就可以用了。一般来说，还是需要稍微配置一下，比如中央仓库的问题。默认使用 Maven 自己的中央仓库，使用起来网速比较慢，这个时候，可以通过修改配置文件，将仓库改成国内的镜像仓库，国内仓库使用较多的是阿里巴巴的仓库。

<!--more-->


### 3.1 仓库类型

|仓库类型|说明|
|:---|:---|
|本地仓库|就是你自己电脑上的仓库，每个人电脑上都有一个仓库，默认位置在 `当前用户名\.m2\repository`|
|私服仓库|一般来说是公司内部搭建的 Maven 私服，处于局域网中，访问速度较快，这个仓库中存放的 jar 一般就是公司内部自己开发的 jar|
|中央仓库|有 Apache 团队来维护，包含了大部分的 jar，早期不包含 Oracle 数据库驱动，从 2019 年 8 月开始，包含了 Oracle 驱动|

现在存在 3 个仓库，那么 jar 包如何查找呢？

![](http://maven.springboot.org/assets/images/img/3-1.png "3-1.png")

### 3.2 本地仓库配置

本地仓库默认位置在 `当前用户名\.m2\repository`，这个位置可以自定义，但是不建议大家自定义这个地址，有几个原因：

1. 虽然所有的本地的 jar 都放在这个仓库中，但是并不会占用很大的空间。
2. 默认的位置比较隐蔽，不容易碰到

技术上来说，当然是可以自定义本地仓库位置的，在 conf/settings.xml 中自定义本地仓库位置：

![](http://maven.springboot.org/assets/images/img/3-2.png "3-2.png")

### 3.3 远程镜像配置

由于默认的中央仓库下载较慢，因此，也可以将远程仓库地址改为阿里巴巴的仓库地址：

```xml
<mirror>
        <id>nexus-aliyun</id>
        <mirrorOf>central</mirrorOf>
        <name>Nexus aliyun</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```

这段配置，加在 settings.xml 中的 mirrors 节点中：

![](http://maven.springboot.org/assets/images/img/3-3.png "3-3.png")
