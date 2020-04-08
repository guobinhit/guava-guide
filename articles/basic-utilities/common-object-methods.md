# 通用 Object 方法

## equals

当你的对象含有的多个字段可能为`null`的时候，实现`Object.equals`会很痛苦，因为你不得不分别对它们进行`null`检查。使用[`Objects.equal`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Objects.html#equal%28java.lang.Object,%20java.lang.Object%29)能够帮助你用一个对`null`敏感的方式执行`equals`检查，而不必冒着抛出`NullPointerException`的风险。例如：

```
Objects.equal("a", "a"); 	// returns true
Objects.equal(null, "a"); 	// returns false
Objects.equal("a", null); 	// returns false
Objects.equal(null, null);	// returns true
```

*注意*：在 JDK 7 中提供了等效的[`Objects.equals`](http://docs.oracle.com/javase/7/docs/api/java/util/Objects.html#equals%28java.lang.Object,%20java.lang.Object%29)方法。

## hashCode

散列一个对象的所有字段应该更简单。Guava 的[`Objects.hashCode(Object...)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Objects.html#hashCode%28java.lang.Object...%29)会对指定的字段构建出一个合理的、顺序敏感的散列值。我们应该使用`Objects.hashCode(field1, field2, ..., fieldn)`来代替手工的构建散列值。

*注意*：在 JDK 7 中提供了等效的[`Objects.hash(Object...)`](http://docs.oracle.com/javase/7/docs/api/java/util/Objects.html#hash(java.lang.Object...))方法。

## toString

一个好的`toString`方法在调试时是无价之宝，不过编写`toString`方法却有些痛苦。使用[`MoreObjects.toStringHelper`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/MoreObjects.html#toStringHelper%28java.lang.Object%29)可以让你非常轻松的创建一个有用的`toString`方法。例如：

```
 // Returns "ClassName{x=1}"
   MoreObjects.toStringHelper(this)
       .add("x", 1)
       .toString();

   // Returns "MyObject{x=1}"
   MoreObjects.toStringHelper("MyObject")
       .add("x", 1)
       .toString();
```

## compare/compareTo

直接实现`Comparator`或者`Comparable`接口也让人头痛。考虑下面这种情况：

```
class Person implements Comparable<Person> {
	private String lastName;
	private String firstName;
	private int zipCode;
  
	public int compareTo(Person other) {
	    int cmp = lastName.compareTo(other.lastName);
	    if (cmp != 0) {
		    return cmp;
	    }
	    cmp = firstName.compareTo(other.firstName);
	    if (cmp != 0) {
		    return cmp;
	    }
	    return Integer.compare(zipCode, other.zipCode);
	}
}
```
这段代码冗长、混乱，而且不便调试。我们应该能够做的更好。为此，Guava 提供了[`ComparisonChain`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ComparisonChain.html)。`ComparisonChain`执行一种“懒惰”的比较策略：它执行比较操作直至发现非零的结果，在那之后的输入都将被忽略。例如：

```
public int compareTo(Foo that) {
	return ComparisonChain.start()
	.compare(this.aString, that.aString)
	.compare(this.anInt, that.anInt)
	.compare(this.anEnum, that.anEnum, Ordering.natural().nullsLast())
	.result();
}
```
这种流畅的风格更具可读性，发生错误的几率更小，并且足够聪明以避免不必要的工作。在 Guava 的“流畅比较器”类`Ordering`中，我们能够看到更多的比较器工具。

-------


**原文链接**：[Google Guava - CommonObjectUtilitiesExplained](https://github.com/google/guava/wiki/CommonObjectUtilitiesExplained).
