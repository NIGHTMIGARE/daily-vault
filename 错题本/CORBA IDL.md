---
tags: [软考-架构师, CORBA, IDL, 错题记录]
date: 2025-03-28
---

## 题目
> OMG 接口定义语言 IDL 文件包含了六种不同的元素，（**接口描述**）是一个 IDL 文件核心的内容，（**模块定义**）将映射为 Java 语言中的包 (package) 或 C++ 语言中的命名空间 (namespace)。

选项：  
A. 模块定义  
B. 消息结构  
C. 接口描述  
D. 值类型

## 答案
第一空：C  
第二空：A

## 解析
- **接口 (interface)** 是 CORBA IDL 的核心，定义远程对象的操作。
- **模块 (module)** 用于组织作用域，映射到 Java 的 package 或 C++ 的 namespace。
- 其他选项不符：  
  - B 消息结构 → 非 CORBA IDL 核心概念  
  - D 值类型 → 是 IDL 元素之一，但不是核心

## 核心概念
**CORBA IDL 主要元素**：
1. 模块 (module)  
2. 接口 (interface) ← 核心  
3. 类型 (struct, enum, union, sequence)  
4. 异常 (exception)  
5. 常量 (const)  
6. 值类型 (valuetype)

**映射规则**：  
- module → package (Java) / namespace (C++)  
- interface → interface (Java) / class (C++)  
- 基本类型 → 语言相关类型（大小可能不同）
- ---
tags: [设计模式, 分布式系统, Proxy模式, CORBA]
date: 2025-03-28
---

## 题目
> 分布性问题强调系统或系统中构件在一个分布的环境中相互通信的方式。解决分布性问题最普通的设计模式是（），CORBA是其一个范例。  
> A. Observer模式  
> B. Iterator模式  
> C. Proxy模式  
> D. Builder模式

## 答案
**C. Proxy模式**

## 解析
### 为什么是 Proxy 模式？
- **Proxy 模式** 在分布式系统中的形式是 **Remote Proxy**  
- 客户端持有本地代理对象（Stub），代理负责网络通信、序列化、调用远程服务  
- 对客户端来说，就像调用本地方法一样

### CORBA 中的 Proxy
- CORBA 使用 IDL 生成客户端 **Stub** 和服务端 **Skeleton**  
- Stub 就是 Remote Proxy，隐藏了 ORB 通信细节（如 IIOP 协议）  
- 使得分布式对象调用对程序员透明

### 其他模式不匹配
- **Observer**：事件通知，不直接解决远程通信  
- **Iterator**：集合遍历  
- **Builder**：对象构造

## 核心概念
**Proxy 模式在分布式的应用**：
1. 远程代理（Remote Proxy） — 用于分布式对象通信  
2. 虚拟代理（Virtual Proxy） — 延迟加载  
3. 保护代理（Protection Proxy） — 访问控制  
4. 智能引用（Smart Reference） — 额外操作