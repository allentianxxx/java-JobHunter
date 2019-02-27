# java-JobHunter



### 静态代码块，构造代码块，构造函数

**静态代码块：**用staitc声明，jvm加载类时执行，仅执行一次
**构造代码块：**类中直接用{}定义，每一次创建对象时执行。
**执行顺序优先级：**静态块 > main() > 实例变量初始化 > 构造代码块 > 构造函数

其实实际上 实例变量初始化和构造代码块 实际上是放在构造函数的超类构造函数之后，本类构造代码之前

> https://www.jianshu.com/p/8a3d0699a923



### 自动装箱和自动拆箱

```java
Integer i = 10;  //装箱 基本数据类型 -> 包装器类型
int n = i;   //拆箱 包装器类型 -> 基本数据类型
```

**自动装箱：**调用包装器的valueOf（**对于有些类的实现就会走缓存**）

**手动装箱：**new Integer(value)就是直接赋值，这样是避免了自动装箱走缓存的影响，因为缓存可能会被反射修改

**自动拆箱：**调用包装器的 xxxValue（xxx代表对应的基本数据类型）

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



### **hashCode、equals 和 ==**

**hashCode**

**1. 对象相等则hashCode一定相等**
**2. hashCode相等对象未必相等**

Object类的hashCode方法，调用c实现的，默认是根据**对象地址**计算hashCode

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

对于对象引用，比较对象引用的内存地址

**总结：**从语法角度，也就是从强制性的角度来说，hashCode和equals是两个独立的，互不隶属，互不依赖的方法，equals成立与hashCode相等这两个命题之间，谁也不是谁的充分条件或者必要条件。 但是，为了让程序正常运行，应该如Effective   Java中所言，**重写equals的时候，一定要（正确）重写hashCode**  

**重写equals不重写hashCode**

使用HashMap，HashSet时，逻辑上相等的两个元素被分到不同的bucket里，并且调用contains方法时即使已经存在逻辑上相等的元素也会返回false

#### 重写equals需要满足5个条件

**自反性**：对于任何非空引用值 x，x.equals(x) 都应返回 true。

**对称性**：对于任何非空引用值 x 和 y，当且仅当 y.equals(x) 返回 true 时，x.equals(y) 才应返回 true。

**传递性**：对于任何非空引用值 x、y 和 z，如果 x.equals(y) 返回 true， 并且 y.equals(z) 返回 true，那么 x.equals(z) 应返回 true。

**一致性**：对于任何非空引用值 x 和 y，多次调用 x.equals(y) 始终返回 true 或始终返回 false， 前提是对象上 equals 比较中所用的信息没有被修改。

**非空性**：对于任何非空引用值 x，x.equals(null) 都应返回 false。

**即为了保证逻辑上的程序正确运行**

> https://juejin.im/post/5a4379d4f265da432003874c



### POJO类中布尔值变量成员变量（Boolean和boolean区别）

POJO不要使用 **isXXX** 这种命名方式，否则部分框架解析会引起序列化错误

**boolean的自动生成的getter方法是 isXXX，而Boolean自动生成的getter和其他类型变量一致为 getXXX** 

boolean 默认值 false Boolean默认值null（**对于除boolean以外的POJO成员变量，最好都用包装类型，即用NPE来避免了默认值导致的逻辑错误，但没有报错难以发现**）

```java
public class IsSuccessTest {
    class Model1 {
        private boolean success;
        public boolean isSuccess() {
            return success;
        }
        public void setSuccess(boolean success) {
            this.success = success;
        }
    }
    class Model2 {
        private boolean isSuccess;
        public boolean isSuccess() {
            return isSuccess;
        }
        public void setSuccess(boolean success) {
            isSuccess = success;
        }
    }
    class Model3 {
        private Boolean succsee;
        public Boolean getSuccsee() {
            return succsee;
        }
        public void setSuccsee(Boolean succsee) {
            this.succsee = succsee;
        }
    }
    class Model4 {
        private Boolean isSuccess;
        public Boolean getSuccess() {
            return isSuccess;
        }
        public void setSuccess(Boolean success) {
            isSuccess = success;
        }
    }
}
```

**fastJson、jackson：**利用反射遍历POJO类中所有getter方法（包括boolean类型的 **isXXX()** 方法），会直接根据JavaBeans规则把方法 getXXX 和 isXXX 后的 XXX 当作属性名，把此方法的返回值当作属性值

**此处还会有一个问题，就是如果你自己写了个 getXXX 形式的方法，这两个框架也会把 XXX 作为属性，其返回值作为属性值**

**Gson：**利用反射遍历POJO类中的所有属性，并把其值序列化成json

> https://mp.weixin.qq.com/s/LTiN6800FbIPmG2UdWwqqg



### 静态导包

Java 5 加入的 

```java
import static com.xxx.xx;
```

静态导入包后，可以直接用方法名调用其静态方法

但滥用可能会导致程序难以维护，可读性变差



### Java计算时间为什么从1970 年 1 月 1 日开始？

Java, JavaScript, Python使用 Unix epoch (Midnight 1 January 1970)，时间戳的起始时间点即为距离此时间的毫秒数

**为什么Unix epoc 是 Midnight 1 January 1970 ？**

最初计算机操作系统是32 位，而时间也是用 32 位表示。 Integer在 JAVA 内用 32 位表 示，因此 32 位能表示的最大值是2147483647（ 范围是-2^31~2^31 - 1）。 另外1 年 365 天的总秒数是 3600 \* 24 \* 365 = 31536000，
2147483647/31536000 = 68.1。也就是说32 位能表示的最长时间是 68 年，而实际上到 2038年 01 月 19 日 03 时 14 分 07 秒，便会到达最大时间，过了这个时间点，所 有 32 位操作系统时间便会变 为 10000000 00000000 00000000 00000000也就是1901年 12月 13 日 20时 45 分 52 秒，这样便会出现时间回归的现象，很多软件便会运 行异常了。

至于时间回归的现象相信随着64 为操作系统 的产生逐渐得到解决，因为这个时间已经是千亿年以后了。

```java
Date date = new Date(0);
System.out.println(date);
```
```java
输出：Thu Jan 01 08:00:00 CST 1970
```

**为什么是8点而非0点？**

系统时间和本地时间问题，系统时间依然是0点，只不过电脑时区设置为东8区，故打印的结果是8点。



### 数组初始化尾随逗号会被忽略

```java
int[] b = {1, 2, 3, 4, 5, 6,}; //A trailing comma causes no compiler error
```

> A trailing comma may appear after the last expression in an array initializer and is ignored.



