# 前置条件

Guava 提供了很多用于进行前置条件检查的工具，我们强烈建议静态导入这些方法。

每个方法都用三种形式：

 - 没有额外的参数。抛出的任何异常都没有错误信息。
 - 有一个额外的`Object`参数。抛出的任何异常都带有一个`object.toString()`的错误信息。
 - 有一个额外的`String`参数以及任意数量的附加`Object`参数。这些行为类似于`printf`，但是为了 GWT 兼容性和高效性仅允许`%s`，例如：

```
checkArgument(i >= 0, "Argument was %s but expected nonnegative", i);
checkArgument(i < j, "Expected i < j, but %s > %s", i, j);
```

| 签名（不包括额外参数） | 描述 | 失败时抛出的异常 |
| ------------- |:-------------:| -----:|
| [`checkArgument(boolean)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkState%28boolean%29) | 检查`boolean`型是否为`true`，用于校验传递给方法的参数 | `IllegalArgumentException` |
| [`checkNotNull(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkState%28boolean%29)| 检查值是否为`null`，直接返回参数值，所以你可以在代码中直接使用`checkNotNull(value)` | `NullPointerException` |
| [`checkState(boolean)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkState%28boolean%29) | 检查对象的某些状态，而不依赖于方法参数。例如，一个`Iterator `可能使用这个方法来检查在调用任何`remove`之前调用`next` | `IllegalStateException` |
| [`checkElementIndex(int index, int size)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkState%28boolean%29) | 在指定长度的列表、字符串和数组中检查`index`是否有效。一个有效的`index`应该是在`0`与指定长度之间的值。你不需要直接传递列表、字符串或者数组，只需传递指定的长度即可。此方法返回`index`| `IndexOutOfBoundsException` |
| [`checkPositionIndex(int index, int size)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkState%28boolean%29)| 检查`index`是否为指定大小的列表、字符串或数组的有效位置索引。一个有效的位置索引应该是在`0`与指定长度之间的值。你不需要直接传递列表、字符串或数组，只需传递它的大小即可。此方法返回`index` | `IndexOutOfBoundsException` |
| [`checkPositionIndexes(int start, int end, int size)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkState%28boolean%29) | 在指定长度的列表、字符串或数组中检查`[start, end)`的范围是否有效。此方法自带错误消息 | `IndexOutOfBoundsException` |

相比 Apache Commons 提供的类似方法，我们把 Guava 中的前置条件作为首选方法是有原因的，简要地：

 - 在静态导入后，Guava 的方法清晰明了。`checkNotNull`清楚地描述它能做了什么以及会抛出什么异常；
 - `checkNotNull`在校验之后直接返回参数，允许你在构造函数中保持字段的单行赋值风格，例如：`this.field = checkNotNull(field)`
 - 简单的、参数可变的`printf`风格异常信息。（正是基于这个优点，让我们为什么在 JDK 7 已经引入`Objects.requireNonNull`的情况下，仍然建议你使用`checkNotNull`.）

我们建议你将前置条件放在不同的行，这可以帮助你在调试期间找出到底是哪些前置件导致的失败。另外，你应该提供有用的错误消息，这让在每个前置条件都位于不同行时更容易定位错误。




-------


**翻译声明**：本文翻译自 GitHub，[Google Guava - PreconditionsExplained](https://github.com/google/guava/wiki/PreconditionsExplained).
