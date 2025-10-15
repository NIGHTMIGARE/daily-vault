---
tags: [软考-架构师, 持久化框架, ORM, MyBatis, 错题记录]
date: 2025-03-28
---

## 题目
> 在持久化技术框架中，需要程序员手写SQL的是 （ ） 。  
> A. MyBatis  
> B. Hibernate  
> C. JDO  
> D. Entity Framework

## 答案
**A. MyBatis**

## 解析
- **MyBatis** 是半自动化 ORM 框架，**需要程序员手动编写 SQL**（在 XML 或注解中），框架负责参数绑定和结果映射。
- **Hibernate**：全自动 ORM，主要通过 HQL 操作，不需要手写原生 SQL。
- **JDO**：使用 JDOQL 查询语言，不需要手写 SQL。
- **Entity Framework**：.NET ORM，使用 LINQ 查询，不需要手写 SQL。

## 核心概念
**ORM 框架分类**：

1. **全自动 ORM**
   - 框架自动生成 SQL
   - 示例：Hibernate、JDO、Entity Framework
   - 优点：开发效率高
   - 缺点：复杂 SQL 优化困难

2. **半自动 ORM**  
   - 程序员手写 SQL，框架做映射
   - 示例：MyBatis、iBATIS
   - 优点：SQL 控制灵活，性能优化方便
   - 缺点：需要编写 SQL，工作量大

3. **选择原则**
   - 需要快速开发、业务简单 → 全自动 ORM
   - 复杂查询、性能要求高 → 半自动 ORM
   - 跨数据库兼容性要求高 → 全自动 ORM

## 易混淆点
- Hibernate **支持**原生 SQL，但这不是其主要使用方式
- MyBatis 的 SQL 写在配置文件中，不是硬编码在 Java 代码中
- "手写 SQL" 指的是程序员需要显式定义 SQL 语句内容