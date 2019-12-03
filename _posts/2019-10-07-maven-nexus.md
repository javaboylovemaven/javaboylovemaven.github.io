---
sidebar:
  nav: docs-zh
title: 7. Maven 私服
tags: Maven
categories: Maven
abbrlink: maven-nexus
date: 2019-10-07 22:28:52
---

## 7. Maven 私服

Maven 仓库管理也叫 Maven 私服或者代理仓库。使用 Maven 私服有两个目的：

1. 私服是一个介于开发者和远程仓库之间的代理
2. 私服可以用来部署公司自己的 jar

<!--more-->

### 7.1 Nexus 介绍

Nexus 是一个强大的 Maven 仓库管理工具，使用 Nexus 可以方便的管理内部仓库同时简化外部仓库的访问。官网是：https://www.sonatype.com/

### 7.2 安装

- 下载

下载地址：https://www.sonatype.com/download-oss-sonatype

- 解压

将下载下来的压缩包，拷贝到一个没有中文的路径下，然后解压。

- 启动

解压之后，打开 cmd 窗口（以管理员身份打开 cmd 窗口），然后定位了 nexus 解压目录，执行 nexus.exe/run 命令启动服务。

![](http://maven.javaboy.org/assets/images/img/7-1.png "7-1.png")

> 这个启动稍微有点慢，大概有 1 两分钟的样子

启动成功后，浏览器输入 http://lcoalhost:8081 打开管理页面。

打开管理页面后，点击右上角上的登录按钮进行登录，默认的用户名/密码是 admin/admin123。当然，用户也可以点击设置按钮，手动配置其他用户。

![](http://maven.javaboy.org/assets/images/img/7-2.png "7-2.png")

点击 Repositories 可以查看仓库详细信息：

![](http://maven.javaboy.org/assets/images/img/7-3.png "7-3.png")

#### 7.2.1 仓库类型

|名称|说明|
|:----|:-----|
|proxy|表示这个仓库是一个远程仓库的代理，最典型的就是代理 Maven 中央仓库|
|hosted|宿主仓库，公司自己开发的一些 jar 存放在宿主仓库中，以及一些在 Maven 中央仓库上没有的 jar|
|group|仓库组，包含代理仓库和宿主仓库|
|virtual|虚拟仓库|


#### 7.2.2 上传 jar

上传 jar，配置两个地方：

- Maven 的 conf/settings.xml 文件配置：

```xml
<server>
  <id>releases</id>
  <username>admin</username>
  <password>admin123</password>
</server>
<server>
  <id>snapshots</id>
  <username>admin</username>
  <password>admin123</password>
</server>
```

在要上传 jar 的项目的 pom.xml 文件中，配置上传路径：

```xml
<distributionManagement>
    <repository>
        <id>releases</id>
        <url>http://localhost:8081/repository/maven-releases/</url>
    </repository>
    <snapshotRepository>
        <id>snapshots</id>
        <url>http://localhost:8081/repository/maven-snapshots/</url>
    </snapshotRepository>
</distributionManagement>
```

配置完成后，点击 deploy 按钮，或者执行 mvn deploy 命令就可以将 jar 上传到私服上。

#### 7.2.3 下载私服上的 jar

直接在项目中添加依赖，添加完成后，额外增加私服地址即可：

```xml
<repositories>
    <repository>
        <id>local-repository</id>
        <url>http://localhost:8081/repository/maven-public/</url>
        <releases>
            <enabled>true</enabled>
        </releases>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </repository>
</repositories>
```