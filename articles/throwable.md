# 异常传播

有时候，当你捕获一个异常时，你可能想将它抛到下一个`try/catch`块。这样情况很常见，例如在出现`RuntimeException`和`Error`的情况下，不需要`try/catch`块，你也不想捕获它们，但是它们仍然被`try/catch`块捕获。

Guava 提供了一些工具类来简化异常传播。例如：

```
try {
     someMethodThatCouldThrowAnything();
} catch (IKnowWhatToDoWithThisException e) {
     handle(e);
} catch (Throwable t) {
     Throwables.propagateIfInstanceOf(t, IOException.class);
     Throwables.propagateIfInstanceOf(t, SQLException.class);
     throw Throwables.propagate(t);
}
```
每一个方法都抛了异常，而抛出的结果，例如`Throwables.propagate(t)`，可以证明编辑器抛出了一个很有用的异常。

下面是 Guava 提供的异常传播方法的摘要：

| 方法签名 | 解释 | 
| ------------- |-------------| 
| [RuntimeException propagate(Throwable)](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#propagate%28java.lang.Throwable%29) | 通过`RuntimeException`或者`Error`进行异常传播，或者将异常包装进`RuntimeException`，可以保证异常的传播性。由于其返回类型是一个`RuntimeException`，所以你可以通过`throw Throwables.propagate(t)`抛出异常，而且 Java 可以识别这样的语句，并保证抛出一个异常。| 
| [void propagateIfInstanceOf(Throwable, Class) throws X](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#propagateIfPossible%28java.lang.Throwable%29) | 当且仅当异常实例为`X`的时候，进行异常传播。  | 
| [void propagateIfPossible(Throwable)](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#propagateIfPossible%28java.lang.Throwable%29) |当出现`RuntimeException`或者`Error`时，抛出`throwable`  | 
| [void propagateIfPossible(Throwable)](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#propagateIfPossible%28java.lang.Throwable%29) | 当出现`RuntimeException`、`Error`或者`X`时，抛出`throwable` | 


## `Throwables.propagate`的使用

详见「[为什么我们不赞成使用 Throwables.propagate](https://github.com/google/guava/wiki/Why-we-deprecated-Throwables.propagate)」

## 异常原因链

Guava 提供了三个有用的方法，使得异常链的研究更加简单，通过这三个方法的签名就可以窥知一二：

|方法签名 | 
| ------------- |
|[Throwable getRootCause(Throwable)](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#getRootCause(java.lang.Throwable)) | 
| [List<<Throwable>Throwable> getCausalChain(Throwable)](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#getRootCause(java.lang.Throwable)) | 
| [String getStackTraceAsString(Throwable)](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#getRootCause(java.lang.Throwable)) | 


----------


**原文链接**：[Google Guava - ThrowablesExplained](https://github.com/google/guava/wiki/ThrowablesExplained).
