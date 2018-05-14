---
title: "Gradle Shadow插件"
date: 2018-05-14T12:43:26+08:00
draft: false
---
# 介绍
Shadow作为Gradle插件, 可以用来将dependency classes与resources打包成一单独Jar。此Jar包通常被称为fat-jar或uber-jar.
## 优势
使用shadow打包主要有以下两种用途:
1. 可执行jar打包
2. lib打包
## 开始使用
```
buildscript {
  repositories {
    jcenter()
  }
  dependencies {
      classpath 'com.github.jengelman.gradle.plguins:shadow:2.0.4'
  }
}

apply plugin: 'com.github.johnrengelman.shadow'
```
或者
```
plugins {
  id 'com.github.johnrengelman.shadow' version '2.0.4'
  id 'java'
}
```
## 默认Java/Groovy Tasks
Shadow将自加入以下动作到Project:
* 加入shadowJar任务
* 加入shadow配置
* 设置shadowJar任务加入所有sources到main sourceSet中
* 设置shadowJar任务打包所有dependencies到runtime configuration
* 设置shadowJar任务classifier属性为'all'
* 设置shadowJar任务生成Manifest
* 设置shadowJar任务排除任意JAR index或者cryptographic signature files, 匹配如下:
    * META-INF/INEX.LIST
    * META-INF/*.SF
    * META-INF/*.DSA
    * META-INF/*.RSA
* 创建并注册shadow组件(用于与maven-publish交互)
* 配置uploadShadow任务(作为maven插件), 并具有如下行为:
    * 从pom.xml中移除compile与runtime configurations
    * 加入shadow configuration到pom.xml中RUNTIME scope