# 使用和避免`null`

> “`null`，糟糕透啦！” —— Doug Lea.

> “我称`null`为百亿美金的错误！” —— C. A. R. Hoare.

轻率地使用`null`可能导致很多令人惊愕的问题。通过研究谷歌的代码，我们发现：95% 的集合不接受`null`作为元素，因此相比于默默地接受`null`，使用快速失败的操作拒绝`null`值对开发者更有帮助。

此外，`null`的模糊性会让人很不爽。我们很难知道返回值是`null`代表着什么意思，例如当`Map.get(key)`返回`null`时，既可能是 Map 中对应`key`的值是`null`，也可能是 Map 中根本就没有对应`key`的值。`null`可以表示成功，也可以表示失败，几乎意味着任何事情。使用除`null`之外的某些其他值，可以让你表达的含义更清晰。

在某些场景下，使用`null`也确实是正确的。例如，在内存和速度方面，`null`就是廉价的，而且在对象数组中，出现`null`也是不可避免的。但是相对于库来说，在应用代码中，`null`往往是导致混乱、疑难问题和含义模糊的根源。就像我们上面谈到的，当`Map.get(key)`返回`null`时，既可能是 Map 中对应`key`的值是`null`，也可能是 Map 中根本就没有对应`key`的值。最关键的是，`null`根本就没有给出空值到底意味着什么。

正是由于这些原因，很多的 Guava 工具类都被设计为针对`null`是快速失败的，除非工具类本身对`null`是友好的。此外，Guava 提供了很多工具类，可以让我们在必须使用`null`时用起来更简单，也可以让我们避免使用`null`.

## 具体案例

不要在`Set`中使用`null`，也不要把`null`作为 Map 的键；在查询操作中，使用一个特殊值表示`null`，这会让我们的语言更加清晰。

如果你想使用`null`作为 Map 中某个键的值，最好不要这么做；单独的维护一个键为空或者非空的`Set`更好一些。毕竟 Map 中对应于某个键的值为空，或者根本就没有值，这是很容易混淆的情况。因此，最好的方法就是将这些键分开，并且仔细想想，在你的应用中，值为`null`的键到底有什么含义。

如果你在`List`中使用`null`，并且列表是稀疏的，那么使用`Map<Integer, E>`可能会更高效，并且可能更符合你潜在的需求。

此外，我们可以考虑一下使用自然的`null`对象的情况。虽然这样的情况并不多，但还是有的，例如有一个枚举类型，添加了一个常量来表示`null`。还例如，在`java.math.RoundingMode`里面有一个常量`UNNECESSARY`，它表示一种不做任何舍入操作的模式，如果用这种模式做舍入操作，则会抛出异常。

如果你确实需要使用`null`值，并且使用 Guava 的集合会有一些问题，那么你可以选择其他的实现。例如，使用 JDK 中的`Collections.unmodifiableList`代替 Guava 中的`ImmutableList`.

## Optional

一般情况下，我们使用`null`表示某种缺失的情况：或许在某个值应该存在的地方，没有值，或者根本就找不到对应的值。例如，通过 Map 的键来获取值的时候，如果对应于某个键的值不存在，`Map.get`就会返回`null`.

`Optional<T>`是一个用非空的值代替引用`T`有可能为空的方法。一个`Optional`可能包括非空的`T`引用（在这种情况下，我们称之为“引用存在”），也可能什么都不包含（在这种情况下，我们称之为“引用缺失”）。但无论如何，`Optional`绝不会说它包含`null`.

```
Optional<Integer> possible = Optional.of(5);
possible.isPresent(); // returns true
possible.get(); // returns 5
```

`Optional`不打算直接模拟其他编程环境中的`option` or `maybe`语义，尽管它们确实有些相似。

在这里，我们列出了一些最常见的`Optional`操作。

## 创建`Optional`实例

这里给出的都是`Optional`的静态方法。

| 方法 | 描述 | 
| ------------- |:-------------:| 
| [`Optional.of(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of%28T%29) | 创建值非空的`Optional`实例，如果值为空则快速失败 | 
| [`Optional.absent()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of%28T%29) | 返回某些类型引用缺失的`Optional`实例 |
| [`Optional.fromNullable(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of%28T%29) | 将可能为空的引用传入`Option`实例，如果引用非空则表示存在；引用为`null`，则表示缺失 |

## 查询方法

下面都是非静态的方法，因此需要特定的`Optional<T>`实例来调用。

| 方法 | 描述 | 
| ------------- |:-------------:| 
| [`boolean isPresent()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of%28T%29) | 如果`Optional`包含非`null`的引用，则返回`true` | 
| [`T get()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of%28T%29) | 返回`Optional`所包含的实例，若引用缺失，则抛出`java.lang.IllegalStateException`|
| [`T or(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of%28T%29) | 返回`Optional`所包含的引用，若引用缺失，返回指定的值 |
| [`T orNull()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of%28T%29) | 返回`Optional`所包含的引用，若引用缺失，返回`null`. 此为`fromNullable`的逆操作。 | 
| [`Set<T> asSet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of%28T%29) | 返回`Optional`所包含引用的单例不变集合，如果引用存在，返回一个只有单一元素的集合；如果引用缺失，返回一个空集合。|

除了上面给出的方法之外，`Optional`还提供了很多有用的工具方法，具体可以通过`Javadoc`来查看详细的资料。

## 使用`Optional`有什么意义？

除了增加`null`的可读性之外，`Optional`最大的优点就在于它是一种傻瓜式的防御机制。如果你想让你的程序编译通过，那么它就会强迫你去积极思考引用缺失的情况。使用`null`很容易让我们忽略某些情况，尽管`FindBugs`可以给我们提供帮助，但我们并不认为这种解决方法很好。

特别地，当你返回一个值的时候，既可以是引用存在也可以是引用缺失。你（或者其他人）更容易忘记`other.method(a, b)`可以返回一个空值，就像你在实现一个方法`other.method`的时候，你也可能忘记参数`a`可以是一个`null`值一样。而将方法的返回类型指定为`Optional`，也可以迫使调用者思考返回为引用缺失的情形。

## 便利的方法

当你想使用某些默认值代替一个`null`值的时候，可以使用`MoreObjects.firstNonNull(T, T)`方法。就像这个方法的名字提示的一样，如果输入的两个参数值都为`null`，则会抛出`NullPointerException`异常。如果你使用`Optional`的话，这里有一个更好的替换方案，例如`first.or(second)`。

在`Strings`类中，也提供了很多可以处理`String`值可能为空的方法。特别得，我们提供了恰当的名称：

| 方法签名 | 
| ------------- |
| [`emptyToNull(String)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#emptyToNull(java.lang.String)) | 
| [`isNullOrEmpty(String)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#emptyToNull(java.lang.String)) | 
| [`nullToEmpty(String)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#emptyToNull(java.lang.String)) | 

我们要强调的是，这些方法主要用来与一些不友好的 API 进行交互，例如`null`字符串和空字符串等等。每当你写下混淆`null`和空字符串的时候，Guava 团队的成员都泪流满面。正确的做法是将空字符串和`null`字符串区别对待，但如果把两者同等对待，这就是要出 bug 的节奏啊！

----------
**原文链接**：[Google Guava - UsingAndAvoidingNullExplained](https://github.com/google/guava/wiki/UsingAndAvoidingNullExplained).
