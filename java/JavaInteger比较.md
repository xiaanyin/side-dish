# **Java Integer 比较**
---

## **知识背景**
- Integer是不可变对象，因为里面的value是final的private final int value; 。
- 在Java中==是比较的两个对象所指向的内存地址是否相等，而equals方法比较的是值。
- -128到127之间的数据放在IntegerCache中，IntegerCache是static的，因此将会放到常量池中作为缓存使用。

## **测试代码**

```java
// Part 1
Integer a = 2;
Integer b = 2;
System.out.println("Part 1:");
System.out.println("a == b  " + (a == b));
System.out.println("a.equals(b)  " + (a.equals(b)));
System.out.println("a.intValue() == b.intValue()  " + (a.intValue() == b.intValue()));
System.out.println("a.compareTo(b)  " + (a.compareTo(b)));

// Part 2
a = new Integer(6);
b = new Integer(6);
System.out.println("Part 2:");
System.out.println("a == b  " + (a == b));
System.out.println("a.equals(b)  " + (a.equals(b)));
System.out.println("a.intValue() == b.intValue()  " + (a.intValue() == b.intValue()));
System.out.println("a.compareTo(b)  " + (a.compareTo(b)));

// Part 3
a = 155;
b = 155;
System.out.println("Part 3:");
System.out.println("a == b  " + (a == b));
System.out.println("a.equals(b)  " + (a.equals(b)));
System.out.println("a.intValue() == b.intValue()  " + (a.intValue() == b.intValue()));
System.out.println("a.compareTo(b)  " + (a.compareTo(b)));

```

## **输出结果**
```
Part 1:
a == b  true
a.equals(b)  true
a.intValue() == b.intValue()  true
a.compareTo(b)  0

Part 2:
a == b  false
a.equals(b)  true
a.intValue() == b.intValue()  true
a.compareTo(b)  0

Part 3:
a == b  false
a.equals(b)  true
a.intValue() == b.intValue()  true
a.compareTo(b)  0
```

## **分析**
- equals、intValue和compareTo都是比较值的大小。

- ==比较的是地址<br/>
    > <Part 1>的值是从IntegerCache缓存取的，所以两个相同；<br/>
    > <Part 2>两个Integer都是new出来的，地址不同，所以是false；<br/>
    > <Part 3>的值虽然没有关键字new，但是大于IntegerCache的默认最大值，导致地址不同，所以结果是false。

## **知识补充**
- 通常IntegerCache的范围是-128到127，然而这个范围的最大值是可变的，可以通过-XX:AutoBoxCacheMax=<size>参数去修改这个值，在JVM初始化的时候，这个值被写入sun.misc.VM class系统私有配置文件中，并加载。

<br/><br/>

[<p align="center">返 回 首 页</p>](../README.md)
