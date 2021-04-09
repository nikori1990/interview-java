---
title: "Basis"
date: 2021-04-08T06:29:39+08:00
---


- [1. 基础](#1-基础)
    - [1.1. 正确使用 equals 方法](#11-正确使用-equals-方法)
    - [1.2. 整型包装类值的比较]
    - [1.3. BigDecimal]
        - [1.3.1. BigDecimal 的用处]
        - [1.3.2. BigDecimal 的大小比较]
        - [1.3.3. BigDecimal 保留几位小数]
        - [1.3.4. BigDecimal 的使用注意事项]
        - [1.3.5. 总结]



# 1. 基础

## 1.1. 正确使用 equals 方法

Object 的 equeals 方法容易抛空指针异常， 应使用常量或确定有值的对象来调用 equals 。

举个例子:

```java
// 不能使用一个值为null的引用类型变量来调用非静态方法， 否则会抛出异常
String str = null;

if(str.equals("nikori")) {
    ...
} else {
    ...
}
```

运行上面的程序会抛出空指针异常，但是我们把第二行的条件判断语句改为下面这样的花，就不会抛出空指针异常，  else 语句块得到执行。 

```java
"nikori".equals(str) // false
```

不过更推荐使用 `java.util.Objects#equals` (JDK7 引入的工具类)

```java
Objects.equeals(str, "nikori") // false
```

我们看一下 `java.util.Objects#equals` 的源码就知道原因了

```java
public static boolean equals(Object a, Object b) {
    // 可以避免空指针异常， 如果a == null 的话， 此时 a.equals(b) 就不会得到执行
    return (a == b) || (a != null && a.equals(b))
}
```

**注意：**

Refrence: [Java 中equals方法造成空指针异常的原因及解决方案]

  




