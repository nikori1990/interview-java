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

## 1.2. 整型包装类值的比较

所有整型包装类对象的比较必须使用equals方法。

先看下面这个例子：

```java
Integer x = 3;
Integer y = 3;

System.out.println(x == y); //true

Integer a = new Integer(3);
Integer b = new Integer(3);

System.out.println(a == b); //false

System.out.println(a.equals(b)); //true
```

当使用自动装箱方式创建一个 Integer 对象时，当数值在 -128 ~ 127 时，会将创建的 Integer 对象缓存起来， 当下次再出现该值时，直接从缓存中取出对应的 Integer 对象。

**注意：** 如果你的IDE 上安装了阿里巴巴的p3c插件， 这个插件如果检测到你用==的话会报错误提示，推荐安装一个这个插件，很不错。

## 1.3. BigDecimal

### 1.3.1. BigDecimal的用处

《阿里巴巴Java开发手册》中提到： **浮点数之间的等值判断，基本数据类型不能用==比较，包装数据类型不能用equals来判断。** 具体原理和浮点数的编码方式有关，这里就不多提了，我们下面直接上实例：

```java
float a = 1.0f - 0.9f;
float b = 0.9f - 0.8f;

System.out.println(a); //0.100000024
System.out.println(b); //0.099999964

System.out.println(a == b); //false
```

具有基本数学只是的我们很清楚的知道输出并不是我们想要的结果（**精度丢失**）， 我们如何解决这个问题呢？一种很常用的方法是： **使用BigDecimal来定义浮点数的值，再进行浮点数的运算操作**。

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");
BigDecimal c = new BigDecimal("0.8");

BigDecimal x = a.subtract(b);
BigDecimal y = b.subtract(c);

System.out.println(x); /* 0.1 */
System.out.println(y); /* 0.1 */
System.out.println(Objects.equals(x, y)); /* true */
```

### 1.3.2. BigDecimal 的大小比较

`a.compareTo(b)` : 返回 -1 表示 `a` 小于 `b`, 0 表示 `a` 等于 `b`, 1 表示 `a` 大于 `b`。

```java
BigDecimal a = new BigDecimal("1.0"); 
BigDecimal b = new BigDecimal("0.9");

System.out.println(a.compareTo(b)); // 1;
```

### 1.3.3. BigDecimal 保留几位小数
通过 `setScale` 方法设置保留几位小数以及保留规则。保留规则有挺多种，不需要记，IDEA会提示。

```java
BigDecimal m = new BigDecimal("1.255433");
BigDecimal n = m.setScale(3, BigDecimal.ROUND_HALF_DOWN);

System.out.println(n); // 1.255
```

### 1.3.4. BigDecimal 的使用注意事项

注意：我们在使用BigDecimal时，为了防止精度丢失，推荐使用它的 **BigDecimal(String)** 构造方法来创建对象。 《阿里巴巴java开发手册》 对这部分内容也有提到。

![BigDecimal](images/BigDecimal.jpg)




