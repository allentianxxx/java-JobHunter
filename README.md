# java-JobHunter



### 静态代码块，构造代码块，构造函数

**静态代码块：**用staitc声明，jvm加载类时执行，仅执行一次
**构造代码块：**类中直接用{}定义，每一次创建对象时执行。
**执行顺序优先级：**静态块 > main() >  函数 > 构造代码块 > 构造函数

> https://www.jianshu.com/p/8a3d0699a923



### 自动装箱和自动拆箱

```java
Integer i = 10;  //装箱 基本数据类型 -> 包装器类型
int n = i;   //拆箱 包装器类型 -> 基本数据类型
```

**装箱：**调用包装器的valueOf

**拆箱：**调用包装器的 xxxValue（xxx代表对应的基本数据类型）

基本数据类型对应的包装器类型

| int（4字节）    | Integer   |
| --------------- | --------- |
| byte（1字节）   | Byte      |
| short（2字节）  | Short     |
| long（8字节）   | Long      |
| float（4字节）  | Float     |
| double（8字节） | Double    |
| char（2字节）   | Character |
| boolean（未定） | Boolean   |

**Integer、Short、Byte、Character、Long这几个类的valueOf方法的实现是类似的（缓存）**

```java
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
```

**Double、Float的valueOf方法的实现是类似的（new 新对象）**

```java
public static Double valueOf(double d) {
    return new Double(d);
}
```

**为何？**因为在某个范围内的整型数值的个数是有限的，而浮点数却不是

**Boolean的valueOf实现比较特殊**

```java
public static Boolean valueOf(boolean b) {
    return (b ? TRUE : FALSE);
}
```

TRUE和FALSE是随Boolean类加载初始化的两个类静态变量

```java
public static final Boolean TRUE = new Boolean(true);
public static final Boolean FALSE = new Boolean(false);
```


> https://www.cnblogs.com/dolphin0520/p/3780005.html
>
> https://mp.weixin.qq.com/s/PWygd0Ro-B3yslm4de9KKA



### **hashCode、equals和“==**

**hashCode**

**1. 对象相等则hashCode一定相等**
**2. hashCode相等对象未必相等**

Object类的hashCode方法，调用c实现的

```java
public native int hashCode();
```

常用的类均已override hashCode方法

一般可以不需了解hashcode用法，但只要和哈希运算有关的地方HashMap，HashSet等**集合类时要注意下hashcode**

**HashMap原理：**是以hashCode作为key插入的，一般hashCode % 8得到所在的索引，如果所在索引处有元素了，则使用一个链表，把多的元素不断链接到该位置，所以hashCode的作用就是找到索引的位置，然后再用equals去比较元素是不是相等，**先用hashCode找到桶（bucket），然后再用equals在里面找东西**。

**equals**

是对象具体内容相等性比较，但Object的equals实现是 **==**

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

常用类均已override equals方法，实现了对象内容相等的比较

**==** 

对于基本类型，比较存储的实际值

对于对象，比较对象的内存地址

**总结：**从语法角度，也就是从强制性的角度来说，hashCode和equals是两个独立的，互不隶属，互不依赖的方法，equals成立与hashCode相等这两个命题之间，谁也不是谁的充分条件或者必要条件。 但是，为了让程序正常运行，应该如Effective   Java中所言，**重载equals的时候，一定要（正确）重载hashCode**  

**即为了保证逻辑上的程序正确运行**

> https://juejin.im/post/5a4379d4f265da432003874c