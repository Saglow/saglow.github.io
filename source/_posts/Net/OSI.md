---
title: OSI模型
description: 网络传输七层协议，通常称为 OSI 模型（Open Systems Interconnection model），是一种网络通信的参考模型，用于描述和组织网络通信协议的不同层次。这个模型将网络通信划分为七个不同的层次，每个层次都有其特定的功能和任务。
date: 2022-12-26
tags:	[知识积累]
toc: true
finished: true
comments: true
---

网络传输七层协议，通常称为 OSI 模型（Open Systems Interconnection model），是一种网络通信的参考模型，用于描述和组织网络通信协议的不同层次。这个模型将网络通信划分为七个不同的层次，每个层次都有其特定的功能和任务。下面是对每个层次的详细介绍：

1. **物理层（Physical Layer）**：
   - 功能：物理层负责定义物理媒体的传输方式，如电压、电流、光信号等，以及传输数据的物理接口标准。
   - 示例：Ethernet、USB、光纤等。

2. **数据链路层（Data Link Layer）**：
   - 功能：数据链路层负责在物理媒体上可靠地传输数据帧。它提供错误检测和纠正，以及地址分配和流量控制。
   - 示例：以太网、Wi-Fi、PPP（Point-to-Point Protocol）等。

3. **网络层（Network Layer）**：
   - 功能：网络层负责在不同的网络之间路由数据包，实现端到端的数据传输。它定义了数据包的格式和路由算法。
   - 示例：IP（Internet Protocol）、IPv4、IPv6、路由器等。

4. **传输层（Transport Layer）**：
   - 功能：传输层负责端到端的通信，提供数据传输的可靠性和错误检测。它还负责多路复用和分解数据流。
   - 示例：TCP（Transmission Control Protocol）、UDP（User Datagram Protocol）。

5. **会话层（Session Layer）**：
   - 功能：会话层负责建立、管理和终止通信会话，以确保数据传输的顺序和完整性。它处理会话层面的错误和恢复。
   - 示例：NetBIOS、RPC（Remote Procedure Call）。

6. **表示层（Presentation Layer）**：
   - 功能：表示层负责数据的编码、解码和加密，以确保数据在不同系统之间的互操作性。它还负责数据的压缩和解压缩。
   - 示例：TLS/SSL、JPEG、ASCII等。

7. **应用层（Application Layer）**：
   - 功能：应用层是最高层，负责定义网络应用程序和用户之间的通信。它包括各种应用协议，如HTTP、FTP、SMTP等。
   - 示例：HTTP、FTP、SMTP、DNS等。

每个层次都构建在下一层的基础之上，并通过使用下一层提供的服务来完成其功能。这种分层结构使得网络通信的设计和维护更加模块化和可扩展，不同层次的协议可以独立地进行开发和更新，而不会影响其他层次。此外，它还提供了一种通用的参考框架，以便不同供应商和开发者之间更好地协作和实现互操作性的网络通信。