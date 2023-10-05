---
title: SQL监控
description: 通过java-agent面向切面编程找出慢SQL
date: 2023-10-5
tags:	[实习项目]
toc: true
finished: true
comments: true
---

* [项目源码]()

# Sql 监控项目
## 项目背景
项目人员比较多, 微服务有20+ 很多项目多出现了sql查询慢的问题.
技术总监希望在上线前就解决所有的sql查询慢的问题
1. mysql自带的监控, 不能做小于1s的
2. druid 自带慢sql的监控, 但是仅小部分项目使用
大部分项目还是使用HikariCP
3. 找出来, 大家也不看. 测试团队希望阻塞
4. 想仅部署在开发/测试环境上, 生产不需要.
5. 不想改代码
## 项目难点
1. 各个微服务的框架使用的比较凌乱. 整理后连接池的解决方案有
1. HikariCP
2. druid(阿里)
3. dbcp(apache)
2. 技术负责人和测试负责人希望慢sql出现, 就出现异常, 不要用日志/记录的方式. 这样开发人员能立即解决
3. 不能修改现在的项目的代码
4. 相关功能想仅部署在开发/测试环境上, 生产不需要
## 项目方案
### 使用`java agent`的方案来实现
1. 使用agent, 可以灵活配置. 仅配置在开发/测试环境, 生产环境无影响
2. 我们可以不用关注特定的框架, 可以对statement类来做整体监控. 仅需要判断class 是否继承statement.就可以对所有的sql监控
3. 无需项目调整和代码修改.
### java的字节码编程
java中有很多字节码编程工具`javassist`,`Byte Buddy`,`Cglib`. 要满足下面几个特点, 选用了`javassist`
1. 小, 可以将源码打入jar中
2. 简单, 学习曲线底
3. 可读性强
## 系统架构图
![1]
## 实施中的难点
### 保存执行开始时间
由于insertBefore的特定插入方式, 无法在insertAfter代码中使用. 所以只能使用threadlocal的方式保存
**错误**
```java
Long startTime = System.currentTime();
// 原始代码
...
Long runTime = System.currentTime() - startTime;
```
**正确**
```java
{
// startTime的作用域就是在这个{}之内
Long startTime = System.currentTime();
}
// 原始代码
...
// Long runTime = System.currentTime() - startTime;
```
### 重写需要的类
由于使用各种ORM的框架, 但是本质都是基于`statement`的操作. 所以需要判断是否继承`statement`的子类
[1]:http://www.plantuml.com/plantuml/png/jLNDJjj04BxlKwp2eHU2H8-M6W5LUw8I4jmuRUnDC7NiO2yet5fAb982eGKI1EA7jXGkX5HKj2H4l4nsRTwYun-iRe4q1-f3bEpCzpCpEywGmuZDPdC6UfA7Bxggvud9SABJRFAFMmbC74nGsYhWn3IP8xovuMwS972VeMUdMDOcyqX2ZSyOmrbgiW2NbcFF3U8uBtM3JjZ4T3AMdQDsaAVAUQ03YReJacXoS6BAfaGRjLHYXE51EJvcK_XDjN566CtTEg68cXg6AkHaiTaGAtNUN7yrxyo4V5c4q6GobLOmNplZvHDaMenYWsOOjZ9GKQTz3Gr8-Xw9N-YpGg4mC4riTtjHL2_vLGNT55VSTjtT-SMBvt3AAmiW4-ZxL8YeJ9y3Ry25uKa7MdcRveXk1YU1e3L7xIZ3byA15kvSRNkDTw0VvVDI6xY3h9W_8bMXWCzxl7o0HRK1DkvhVf0R-r4HZXvYCDmtwWzun9YbsAitU7iJ6YIMZht3PNxrXXz_4BMBczgF6FANyNwiIQ6mQ_5WnTuYRpML7fdbuk97nSaKzijy_rLKJztlBR5rnjU-mQTOBl7wDXGDXtSXcXBPuQSrhxpW7hmDxRXBbo6gq_e2Xn8mRf9SbfPCfhH1uBlUvQTR3zhN_7789_G1HZMOd6uwr6OZ5CP45ImgdtZnABO7rqoSRyOeQZWKzutfvciSTN5rN-mUnOczZYYyMCxjsW3-GI9f8h9vgaH4tS1nxJ9SDcXbxeQxLzZLN1X8fh9AH0AtJgwesv2et6vfEGxTUYsa14UFiHPIok10905-WJyKkaVbAUHT5BthKlZwYQtqOr7UuQNcYu9Ayqotp9x6-1zsn5lzoIlLS5E0uF7MP3Z3gFtFBJ4r507Je25pgmXUc9CATblhOdSV_H59eo50mf_ZRm00