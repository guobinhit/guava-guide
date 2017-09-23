# Guava 中文指南

 　　Guava 项目包含若干被 Google 的 Java 项目依赖的核心类库，例如：集合、缓存、原生类型支持、并发库、通用注解、字符串处理、I/O 等等。Google 的开发者们每天都在使用这些工具进行项目的开发。但是查阅 Javadoc 并不总是最有效的学习这些类库的方式。在这里，我们尝试为 Guava 中一些最受欢迎和最有用的功能提供更具可读性的说明。

 - **基础工具[Basic utilities]**：让我们更愉快的使用 Java 语言。
	 - [使用和避免`null`](https://github.com/guobinhit/guava-guide/blob/master/articles/about-null.md)：`null`的定义很模糊，可能导致令人疑惑的错误，有时会让我们很不爽。很多的 Guava 工具类对`null`都是快速失败的，拒绝使用`null`，，而不是盲目的接收它们。
	 - [前置条件[Preconditons]](https://github.com/guobinhit/guava-guide/blob/master/articles/preconditions.md)：让你的方法更容易进行前置条件的检查。
	 - 通用`Object`方法：简化`Object`方法的实现，例如`hashCode()`和`toString()`.
	 - 排序：Guava 有强大且流畅的`Comparator`类。
	 - [可抛的[Throwable]](https://github.com/guobinhit/guava-guide/blob/master/articles/throwable.md)：简化了异常和错误的检查及传播机制。
 - **集合[Collections]**：Guava 扩展了 JDK 的集合体系，这是 Guava 最成熟且最受欢迎的部分。
   - 不可变集合：为了进行防御性编程、使用常量集合和提高效率。
   - 新集合类型：提供了多集合、多 Map、多表、双向 Map 等。
   - 强大的集合工具类：普通的操作并没有在`java.util.Collections`中提供。
   - 扩展工具类：装饰`Collection`？实现`Iterator`？我们让类似的操作变的更简单。

 - **图[Graphs]**：这是一个图结构数据的模型类库，它展现了实体以及图和实体之间的关系，主要的特点包括：
   - 图[Graph]：图的边缘是没有自己标识和信息的匿名实体。
   - 值图[ValueGraph]：图的边缘关联着非唯一的值。
   - 网络[Network]：图的边缘是唯一的对象。
   - 支持可变的、不可变的、定向的和无向的图以及其他一些属性。

 - **缓存[Caches]**：支持本地缓存，也支持多种缓存过期行为。

 - **函数风格[Functional idioms]**：Guava 的函数风格能够显著的简化代码，但请谨慎使用。

 - **并发[Concurrency]**：强大而简单的抽象，让编写正确的并发代码更简单。 
   - ListenableFuture： Future，结束时触发回调 。
   - Service：开启和关闭服务，帮助我们处理困难的状态逻辑。

 - **字符串[Strings]**：非常有用的字符串处理工具，包括分割、拼接等等。

 - **原生类型[Primitives]**：扩展了 JDK 没有提供的原生类型（像`int`和`char`）操作，包含了某些类型的无符号变量。

 - **区间[Ranges]**：Guava 强大的 API 提供了基于`Comparable`类型区间比较功能，包连续类型和离散类型。

 - **输入输出流[I/O]**：针对 Java 5 和 Java 6 版本，简化了 I/O 操作，尤其是 I/O 流和文件操作。

 - **散列[Hashing]**：提供了比`Object.hashCode()`更负责的哈希实现，包含了 Bloom 过滤器。

 - **事件总线[EventBus]**：在不需要组件之间显示注册的情况下，提供了组件之间的发布-订阅模式的通信。

 - **数学运算[Math]**：优化了 JDK 已经提供的数学工具类，并彻底的测试了 JDK 没有提供的数学工具类。

 - **反射[Reflection]**：对应 Java 反射能力的 Guava 工具类。




## Guava 的使用方法：

如果我们使用 Maven 进行项目管理，那么我们只需要在`POM.xml`中添加如下依赖：

```
<dependency>
  <groupId>com.google.guava</groupId>
  <artifactId>guava</artifactId>
  <version>23.0</version>
  <!-- or, for Android: -->
  <version>23.0-android</version>
</dependency>
```
而如果我们使用 Gradle 进行项目管理，那么我们则需要在`config.gradle`中添加如下依赖：
```
dependencies {
  compile 'com.google.guava:guava:23.0'
  // or, for Android:
  compile 'com.google.guava:guava:23.0-android'
}
```


