---
tags: [软考-架构师, 设计模式, 创建型, 结构型, 行为型, 错题记录]
date: 2025-10-02
---

## 题目
> 按照设计模式的目的进行划分，现有的设计模式可以分为三类。其中创建型模式通过采用抽象类所定义的接口，封装了系统中对象如何创建、组合等信息，其代表有( )模式等; ( )模式主要用于如何组合己有的类和对象以获得更大的结构，其代表有 Adapter 模式等; ( )模式主要用于对象之间的职责及其提供服务的分配方式，其代表有( )模式等。  
> 第一空选项：  
> A. Decorator  
> B. Flyweight  
> C. Command  
> D. Singleton

## 答案
第一空：**D. Singleton**

## 解析
- **创建型模式**：负责对象创建。代表有 Singleton、Factory Method、Abstract Factory 等。
- **结构型模式**：负责类与对象的组合。代表有 Adapter、Decorator、Flyweight 等。
- **行为型模式**：负责对象间职责分配与通信。代表有 Command、Observer、Strategy 等。

第一空选项分析：  
- A. Decorator → 结构型 ❌  
- B. Flyweight → 结构型 ❌  
- C. Command → 行为型 ❌  
- D. Singleton → 创建型 ✅

## 核心概念
**GoF 设计模式三类**：
1. **创建型**（5种）：Singleton、Factory Method、Abstract Factory、Builder、Prototype  
2. **结构型**（7种）：Adapter、Bridge、Composite、Decorator、Facade、Flyweight、Proxy  
3. **行为型**（11种）：Command、Iterator、Observer、Strategy、Template Method 等
某快餐厅主要制作并出售儿童套餐，一般包括主餐（各类比萨）、饮料和玩具，其餐品种类可能不同，但制作过程相同。前台服务员（Waiter）调度厨师制作套餐。欲开发一软件，实现该制作过程，设计如下所示类图。该设计采用（1）模式将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示。其中，（2）构造一个使用Builder接口的对象。该模式属于（3）模式，该模式适用于（4）的情况。
![[Pasted image 20251013213634.png]]
## 类图说明
**Waiter** (Director)  
- 控制构建过程 (`construct`)  
- 设置具体建造者 (`setPizzaBuilder`)  
- 获取最终产品 (`getPizza`)

**PizzaBuilder** (Abstract Builder)  
- `createNewPizza`：创建产品实例  
- `buildParts`：抽象构建方法  
- `getPizza`：返回构建好的产品

**HawaiianPizzaBuilder / SpicyPizzaBuilder** (Concrete Builder)  
- 实现 `buildParts`，构造特定类型 Pizza 的各个部分

**Pizza** (Product)  
- 复杂对象，由多个部分组成
问题1[单选题]

A.生成器（Builder）

B.抽象工厂（Abstract Factory）

C.原型（Prototype）

D.工厂方法（Factory Method）
## 设计模式
**建造者模式 (Builder Pattern)**  
- 用途：用于创建复杂对象，分离构建过程和表示，允许通过相同过程得到不同产品。  
- 适用场景：  
  1. 创建对象需要多个步骤  
  2. 需要创建不同的产品变体，但构建过程相似  
  3. 不想在 Product 类中包含太多构建逻辑

## 对比工厂模式
- **工厂模式**：一次性创建对象，不暴露构造细节。  
- **建造者模式**：分步骤构造，Director 控制流程，Builder 实现具体构造。
- 很好的问题！我来帮你详细解释为什么这里不是**抽象工厂**或**原型**模式，而是**建造者模式**。

---

## **一、为什么不是抽象工厂模式 (Abstract Factory)**

**抽象工厂模式的特点：**
- 创建**一组相关或依赖的对象家族**
- 每个具体工厂能生产完整的产品族
- 不关心构建过程，只关心"创建什么产品"

**与本图的对比：**
```java
// 抽象工厂的例子
interface PizzaFactory {
    Dough createDough();
    Sauce createSauce(); 
    Topping createTopping();
}

// 使用方式
Pizza pizza = new Pizza(factory.createDough(), factory.createSauce(), factory.createTopping());
```

**关键区别：**
- 图中 `Waiter` 有 `construct()` 方法 → 说明有**构建过程控制**
- `PizzaBuilder` 有 `buildParts()` → 说明是**分步骤构建**
- 抽象工厂没有这种"分步骤构建"的概念，它是一次性创建完整产品族

---

## **二、为什么不是原型模式 (Prototype)**

**原型模式的特点：**
- 通过**复制现有对象**来创建新对象
- 核心方法是 `clone()` 或 `copy()`
- 适用于创建成本较高的对象

**与本图的对比：**
```java
// 原型模式的例子
Pizza prototypePizza = new HawaiianPizza();
Pizza newPizza = prototypePizza.clone();
newPizza.customize(); // 修改克隆后的对象
```

**关键区别：**
- 图中完全没有 `clone()`、`copy()` 等方法
- 而是通过 `buildParts()` 来**从头构建**对象
- `Waiter` 控制构建流程，这不是原型的特征

---

## **三、为什么确定是建造者模式**

**建造者模式的标志性特征：**

1. **Director (Waiter)** - 控制构建过程
   ```java
   waiter.setPizzaBuilder(hawaiianBuilder);
   waiter.construct(); // 指导构建过程
   Pizza pizza = waiter.getPizza();
   ```

2. **Builder 接口 (PizzaBuilder)** - 定义构建步骤
   ```java
   interface PizzaBuilder {
       void createNewPizza();
       void buildParts(); // 构建各个部件
       Pizza getPizza();
   }
   ```

3. **具体建造者** - 实现不同的产品变体
   - `HawaiianPizzaBuilder`
   - `SpicyPizzaBuilder`

4. **分步骤构建** - `buildParts()` 方法明确表示分部件构建

---

## **四、快速记忆技巧**

| 模式 | 核心思想 | 是否有构建过程控制 |
|------|----------|------------------|
| **抽象工厂** | 创建产品族 | ❌ 没有 |
| **原型模式** | 克隆现有对象 | ❌ 没有 |
| **建造者模式** | 分步骤构建复杂对象 | ✅ 有(Director) |

**简单判断：**
- 看到 `construct()` + `buildParts()` + `getProduct()` = **建造者模式**
- 看到 `createProductA()` + `createProductB()` = **抽象工厂**
- 看到 `clone()` = **原型模式**

---

## **五、巩固练习**

**判断这个描述是什么模式：**
> 一个文档生成器，可以创建 PDF、HTML 等格式的文档。生成过程包括：设置标题、添加段落、插入图片、设置页脚等步骤，由 Director 控制这些步骤的顺序。

**答案：建造者模式**  
原因：有明确的构建步骤和 Director 控制过程。

---

现在你能理解为什么这道题选建造者模式而不是其他创建型模式了吗？