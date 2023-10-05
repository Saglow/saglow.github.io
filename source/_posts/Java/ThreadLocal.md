---
title: java-agent
description: java代理
date: 2023-1-15
tags:	[实习项目]
toc: true
finished: true
comments: true
---

# ThreadLocal

多线程是Java实现多任务的基础，Thread对象代表一个线程，我们可以在代码中调用Thread.currentThread()获取当前线程。例如，打印日志时，可以同时打印出当前线程的名字：

```java
public class Main {
    public static void main(String[] args) throws Exception {
        log("start main...");
        new Thread(() -> {
            log("run task...");
        }).start();
        new Thread(() -> {
            log("print...");
        }).start();
        log("end main.");
    }

    static void log(String s) {
        System.out.println(Thread.currentThread().getName() + ": " + s);
    }
}
```

对于多任务，Java标准库提供的线程池可以方便地执行这些任务，同时复用线程。Web应用程序就是典型的多任务应用，每个用户请求页面时，我们都会创建一个任务，类似：

```java
public void process(User user) {
    checkPermission();
    doWork();
    saveStatus();
    sendResponse();
}
```

Java标准库提供了一个特殊的ThreadLocal，它可以在一个线程中传递同一个对象。

ThreadLocal实例通常总是以静态字段初始化如下：
```java
static ThreadLocal<User> threadLocalUser = new ThreadLocal<>();
```
它的典型使用方式如下：
```java
void processUser(user) {
    try {
        threadLocalUser.set(user);
        step1();
        step2();
    } finally {
        threadLocalUser.remove();
    }
}
```
ThreadLocal相当于给每个线程都开辟了一个独立的存储空间，各个线程的ThreadLocal关联的实例互不干扰。
