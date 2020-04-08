# Guava 中文指南

![author](https://img.shields.io/badge/author-chariesgavin-blueviolet.svg)![last commit](https://img.shields.io/github/last-commit/guobinhit/guava-guide.svg)![issues](https://img.shields.io/github/issues/guobinhit/guava-guide.svg)![stars](https://img.shields.io/github/stars/guobinhit/guava-guide.svg)![forks](https://img.shields.io/github/forks/guobinhit/guava-guide.svg)![license](https://img.shields.io/github/license/guobinhit/guava-guide.svg)

 　　Guava 项目包含若干被 Google 的 Java 项目依赖的核心类库，例如：集合、缓存、原生类型支持、并发库、通用注解、字符串处理、I/O 等等。Google 的开发者们每天都在使用这些工具进行项目的开发。但是查阅 Javadoc 并不总是最有效的学习这些类库的方式。在这里，我们尝试为 Guava 中一些最受欢迎和最有用的功能提供更具可读性的说明。

 - **基础工具[Basic utilities]**：让我们更愉快的使用 Java 语言。
	 - 使用和避免 null[[Using and avoiding null](https://github.com/guobinhit/guava-guide/blob/master/articles/basic-utilities/using-and-avoiding-null.md)]：`null`的定义很模糊，可能导致令人疑惑的错误，有时会让我们很不爽。很多的 Guava 工具类对`null`都是快速失败的，拒绝使用`null`，，而不是盲目的接收它们。
	 - 前置条件[[Preconditons](https://github.com/guobinhit/guava-guide/blob/master/articles/basic-utilities/preconditions.md)]：让你的方法更容易进行前置条件的检查。
	 - 通用 object 方法[[Common object methods](https://github.com/guobinhit/guava-guide/blob/master/articles/basic-utilities/common-object-methods.md)]：简化`Object`方法的实现，例如`hashCode()`和`toString()`.
	 - 排序[[Ordering](https://github.com/google/guava/wiki/OrderingExplained)]：Guava 有强大且流畅的`Comparator`类。
	 - 可抛的[[Throwable](https://github.com/guobinhit/guava-guide/blob/master/articles/basic-utilities/throwable.md)]：简化了异常和错误的检查及传播机制。
 - **集合[Collections]**：Guava 扩展了 JDK 的集合体系，这是 Guava 最成熟且最受欢迎的部分。
   - 不可变集合[[Immutable Collections](https://github.com/google/guava/wiki/ImmutableCollectionsExplained)]：为了进行防御性编程、使用常量集合和提高效率。
   - 新集合类型[[New Collection Types]](https://github.com/google/guava/wiki/NewCollectionTypesExplained)]：提供了多集合、多 Map、多表、双向 Map 等。
   - 强大的集合工具类[[Powerful Collection Utilities]](https://github.com/google/guava/wiki/CollectionUtilitiesExplained)]：普通的操作并没有在`java.util.Collections`中提供。
   - 扩展工具类[[Extension Utilities]](https://github.com/google/guava/wiki/CollectionHelpersExplained)]：装饰`Collection`？实现`Iterator`？我们让类似的操作变的更简单。

 - **图[[Graphs](https://github.com/google/guava/wiki/GraphsExplained)]**：这是一个图结构数据的模型类库，它展现了实体以及图和实体之间的关系，主要的特点包括：
   - 图[[Graph](https://github.com/google/guava/wiki/GraphsExplained#graph)]：图的边缘是没有自己标识和信息的匿名实体。
   - 值图[[ValueGraph](https://github.com/google/guava/wiki/GraphsExplained#valuegraph)]：图的边缘关联着非唯一的值。
   - 网络[[Network](https://github.com/google/guava/wiki/GraphsExplained#network)]：图的边缘是唯一的对象。
   - 支持可变的、不可变的、定向的和无向的图以及其他一些属性。

 - **缓存[[Caches](https://github.com/google/guava/wiki/CachesExplained)]**：支持本地缓存，也支持多种缓存过期行为。

 - **函数风格[[Functional idioms](https://github.com/google/guava/wiki/FunctionalExplained)]**：Guava 的函数风格能够显著的简化代码，但请谨慎使用。

 - **并发[Concurrency]**：强大而简单的抽象，让编写正确的并发代码更简单。 
   - [ListenableFuture](https://github.com/google/guava/wiki/ListenableFutureExplained)： Future，结束时触发回调 。
   - [Service](https://github.com/google/guava/wiki/ServiceExplained)：开启和关闭服务，帮助我们处理困难的状态逻辑。

 - **字符串[[Strings](https://github.com/google/guava/wiki/StringsExplained)]**：非常有用的字符串处理工具，包括分割、拼接等等。

 - **原生类型[[Primitives](https://github.com/google/guava/wiki/PrimitivesExplained)]**：扩展了 JDK 没有提供的原生类型（像`int`和`char`）操作，包含了某些类型的无符号变量。

 - **区间[[Ranges](https://github.com/google/guava/wiki/RangesExplained)]**：Guava 强大的 API 提供了基于`Comparable`类型区间比较功能，包连续类型和离散类型。

 - **输入输出流[[I/O](https://github.com/google/guava/wiki/IOExplained)]**：针对 Java 5 和 Java 6 版本，简化了 I/O 操作，尤其是 I/O 流和文件操作。

 - **散列[[Hashing](https://github.com/google/guava/wiki/HashingExplained)]**：提供了比`Object.hashCode()`更负责的哈希实现，包含了 Bloom 过滤器。

 - **事件总线[[EventBus](https://github.com/google/guava/wiki/EventBusExplained)]**：在不需要组件之间显示注册的情况下，提供了组件之间的发布-订阅模式的通信。

 - **数学运算[[Math](https://github.com/google/guava/wiki/MathExplained)]**：优化了 JDK 已经提供的数学工具类，并彻底的测试了 JDK 没有提供的数学工具类。

 - **反射[[Reflection](https://github.com/google/guava/wiki/ReflectionExplained)]**：对应 Java 反射能力的 Guava 工具类。




## Guava 的使用方法：

如果我们使用 Maven 进行项目管理，那么我们只需要在`POM.xml`中添加如下依赖：

```
<dependency>
  <groupId>com.google.guava</groupId>
  <artifactId>guava</artifactId>
  <version>28.2-jre</version>
  <!-- or, for Android: -->
  <version>28.2-android</version>
</dependency>
```

而如果我们使用 Gradle 进行项目管理，那么我们则需要在`config.gradle`中添加如下依赖：

```
dependencies {
  // Pick one:

  // 1. Use Guava in your implementation only:
  implementation("com.google.guava:guava:28.2-jre")

  // 2. Use Guava types in your public API:
  api("com.google.guava:guava:28.2-jre")

  // 3. Android - Use Guava in your implementation only:
  implementation("com.google.guava:guava:28.2-android")

  // 4. Android - Use Guava types in your public API:
  api("com.google.guava:guava:28.2-android")
}
```

---------

English Original Editon: [Guava - User Guide](https://github.com/google/guava/wiki)
