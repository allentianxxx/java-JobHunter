# Thinking in Java

## 第1章 对象导论

### 抽象

“命令式”语言要求程序员建立 「解空间」（对问题建模处，计算机） 和「问题空间」（问题存在处，一项业务）的联系

OOP允许根据问题来描述问题，而不是根据运行解决方案的计算机来描述问题

对象具有状态、行为、标识

### 访问控制

public：所有人

private：类创建者和内部方法

protected：可以被子类访问的private

默认：包访问权限

### 继承

允许“声明多继承”，不允许“实现多继承”

只继承不做任何操作，那么子类和父类完全一样的行为和类型，没什么意义

### 多态

编译器默认**后期绑定**：编译时不确定要运行代码，只确保被调用方法存在，进行参数和返回值类型检查，运行时才根据实际类型执行对应方法（出现于父类形参，传入子类实参） 。将子类看作父类的行为：upcasting（向上转型）

### 容器

也称为集合，Java有各种类型不同容器主要是因为 **1.提供了不同类型接口和外部行为 2.对某些操作的不同效率**

如具有相同类型接口和外部行为的 ArrayList（适合随机访问）LinkedList（适合随机插入）

#### 参数化类型（范型）

Java SE 5 加入的，避免了容器在存储对象过程中的向上转型（变为Object）和取出时的向下转型（耗时且可能引发异常）

### 对象创建和生命周期

C语言为追求效率，必须显示指定对象存储空间、类型，对象存储在**堆栈**（**创建释放快**，但不灵活，必须知道存储在堆栈中数据确切生命周期，以便上下移动堆栈指针），编译器知道对象生命周期，**通过编程来确定何时销毁对象**

####完全采用动态内存分配

Java在运行时才知道，且在运行时在**堆（heap**）内为对象动态分配内存，通过**垃圾回收器**自动清理不使用的对象（得益于单根继承的特性）

**Java对象存储在堆，但对象引用和基本数据类型存储在堆栈**

### 异常处理不是面向对象独有特性

### 并发编程

Java的多线程指的是语言级别的，逻辑上的多线程，**虚拟机中的线程状态，不反映任何操作系统线程状态**

JDK 1.2 以前对操作系统来说是 用户级线程ULT（UserLevelThreads），操作系统认为还是只有一个Java进程

JDK1.2及以后通过系统调用，将程序的线程交给了操作系统内核进行调度，**现在的Java中线程的本质，其实就是操作系统中的线程**

CPU是工厂，车间是进程，车间里的工人是线程，车间里的厕所可以理解为共享内存

## 第二章 一切都是对象（但基本数据类型不是对象）

String s是对象引用，对象引用是遥控器，对象是电视机

### 存储

**寄存器：**在Java语言中不能进行操作 

**堆栈：**存在RAM中，是部分Java数据存储的地方——包括**对象引用**和**基本类型**

**堆（通用内存池）：**存在RAM中，存放Java对象（**相较于堆栈的好处**：编译器不需要知道存储数据的生命周期）

**常量存储：**存放在代码内部

**非RAM存储（程序结束后仍保持自己状态）：**流对象（字节流，发送给另一台机器）持久化对象（存放在磁盘）

### 作用域

变量（如对象引用）只作用于作用域结束之前

```java
{
    int x = 12;
    {
        int x = 12; //Illegal in Java, but legal in C/C++(“隐藏”较大作用域的变量)
    }
}
```

**但对象可以存活于作用域之外（只要需要用到的话）**

```java
{
    String s = new String("a String");
}//End of scope 作用域结束时，对象引用 s 消失，但对象还继续占用着内存空间
```

### 基本成员默认值

基本类型用作**类的成员**时会有默认值boolean=false，char='\u0000'，剩余数值类型默认值都为0

char的默认值 '\u0000' 是 Unicode 中的空字符。 **和Java中的 null 引用不是一个东西**

| 基本类型 |  默认值  |
| :------: | :------: |
| boolean  |  false   |
|   char   | '\u0000' |
|   byte   | (byte)0  |
|  short   | (short)0 |
|   int    |    0     |
|   long   |    0L    |
|  float   |   0.0f   |
|  double  |   0.0d   |



## 第三章 操作符

### 使用

**=，==，!=，可以操作所有对象，其他操作符只能操作基本类型**

**副作用**：赋值操作=，自动递增、递减 ++，-- 。操作符改变了操作数自身的值（一般操作符是用于操作数生成一个新值）

### 赋值

a=b，给对象赋值传递的是**对象引用**（**别名现象**：复制了一份b给a，此时<u>对象引用a和b同时指向b所指向的对象</u>，a引用被覆盖，其原本指向的对象会交给垃圾回收器处理）

给基本类型赋值就是直接复制了数值

### 算术操作符

+、-、*、/、%

操作符紧跟一个等号 +=，-=，此中形式适用于Java所有「二元」操作符，只要有实际意义即可

### 一元加、减操作符

一元减号用于转换数据符号

一元加号只是为了对应一元减号（**但唯一作用是把较小类型的操作数提升为int**）

```java
byte b = 1;
byte c = +b; // 会报错
int d = +b; // 正常运行
```

### 自动递增递减

++、--

### 关系操作符

<、>、<=、>=、==、!=

### 逻辑操作符

&&、||、!

### 短路

&&逻辑表达式产生了false值，后面部分都不进行计算

||逻辑表达式产生了true值，后面部分都不进行计算

### 直接常量

```java
int i = 0x2f; //16进制
int i2 = 0177; //8进制
```

### 指数计数法

e代表的不是我们常理解的自然对数的基数

从FORTRAN开始，到C/C++和Java延续了下来，e代表的是10

```java
float f4 = 1e-43f;
```

编译器默认将指数当作double处理，这里如果不加f就会报类型的错

### 按位操作符（按位执行布尔代数运算）

二元：&、|、^、

一元：~（按位“非”，取反）

**布尔值特殊情况**：**按位操作符和逻辑操作符同样的效果，但不会短路（即&产生了false还会计算后面部分）**！！！

###移位操作符

<<左移：低位补0

\>>带符号右移：高位补符号位

\>>>无符号右移：高位补0（C/C++都没有）

也可以加=号，a<<=b，a左移b次，最后值赋给a

**对char byte short移位时，会先转换为int再移位，对它们进行算术运算时也是一样**

### 类型转换

除布尔型之外的基本数据类型都可以进行强制类型转换

## 第四章 控制执行流程

### continue、break的label使用

label：和goto一个意思

continue label，跳转到label，但继续执行循环

break label，跳转到label，不执行循环

使用场景：嵌套循环想要从多层嵌套中break或continue

### switch语句

选择因子必须是整数值 （integral-selector）,如果是字符串或者浮点数，则必须用if-else

**但Java SE 5 的 enum削弱了这种限制**

## 第五章 初始化与清理（cleanup）

### 构造器

没有返回值，和void返回值都不同，就是没有

new 表达式倒是返回了一个对新建对象的引用

### 方法重载（overloading）

方法名相同，区分通过：参数类型列表

### this关键字（本质就是一个对象引用）

只出现在非static方法内部，对象引用，指向调用方法的那个对象

使用场景：将自身传递给外部方法、构造器中调用构造器

### finalize()：执行特殊清理工作

**使用场景：**

- 用于清理一种被特殊分配内存的对象，即调用非java代码分配了内存的对象
- 用于在验证程序终结条件，是否有未被清理的地方

在垃圾回收发生时，会首先调用对象finalize()方法，并在下一次垃圾回收时才真正收回此对象占用内存

**注意：**

1. 对象可能不被垃圾回收（**垃圾回收并不是一定发生的**）
2. 垃圾回收不等于“析构（C/C++）”
3. 垃圾回收只和内存相关

### JIT（just in time）

热点代码检测，JIT判断字节码中哪些是频繁执行的，编译成机器码。如果是用的很少，就解释执行

![](https://www.ibm.com/developerworks/cn/java/j-lo-just-in-time/img001.png)

**编译 Compile**：把整个程序源代码翻译成另外一种代码，然后等待被执行，发生在运行之前，产物是「另一份代码」。
**解释 Interpret**：把程序源代码一行一行的读懂然后执行，发生在运行时，产物是「运行结果」。

### 数组初始化

**1.基本数据类型数组**

int[] a = {};

int[] a = new int[n]; 运行时创建，**这时数组元素若是基本类型会自动初始化默认值**

**2.对象数组（本质上是一个引用数组）**

Integer[] a = {new Integer(1), new Integer(2), 3, };

Integer[] a = new Integer[]{new Integer(1), new Integer(2), 3, };

### 可变参数列表Varargs（Java SE 5添加）

**只能对最后一个形参使用**

**使用场景：**在不确定方法需要处理的对象的数量时可以使用可变长参数，会使得方法调用更简单，无需手动创建数组 new T[]{…}

**调用方式：**

```java
public class Varargs {
    public static void test(String... args) {
        for(String arg : args) {
            System.out.println(arg);
        }
    }
    public static void main(String[] args) {
        test();//0个参数
        test("a");//1个参数
        test("a","b");//多个参数
        test(new String[] {"a", "b", "c"});//直接传递数组
    }
}
```

### 枚举enum（Java SE 5添加）

对象是有限且固定的类，其地位与 class、interface 相同；

枚举类是一种特殊的类，有自己的成员变量、成员方法、构造器 (只能使用 **private** 访问修饰符，**构造器只在构造枚举值时被调用**)；

使用 enum 定义的枚举类默认继承了 java.lang.Enum 类，并实现了 java.lang.Seriablizable 和 java.lang.Comparable 两个接口;

所有的**枚举值都是 public static final** 的，且非抽象的枚举类不能再派生子类；

枚举类的所有实例(枚举值)**必须在枚举类的第一行显式地列出**，否则这个枚举类将永远不能产生实例

```java
public enum WeekEnum {
    // 因为已经定义了带参数的构造器，所以在列出枚举值时必须传入对应的参数
    SUNDAY("星期日"), MONDAY("星期一"), TUESDAY("星期二"), WEDNESDAY("星期三"),
    THURSDAY("星期四"), FRIDAY("星期五"), SATURDAY("星期六");
    // 定义一个 private 修饰的实例变量
    private String date;
    // 定义一个带参数的构造器，枚举类的构造器只能使用 private 修饰
    private WeekEnum(String date) {
        this.date = date;
    }
    // 定义 get set 方法
    public String getDate() {
        return date;
    }
    public void setDate(String date) {
        this.date = date;
    }
}
```

**枚举类对象两个默认的字段：name:String和ordinal:int**，分别存放枚举值、枚举值对应的int（0开始）

枚举类的每个枚举值就是该枚举类的一个对象

**和其他非抽象类不同，枚举类可以定义抽象方法，但其所有枚举值必须实现该方法**

```java
public enum Operation {
    // 用于执行加法运算
    PLUS { // 花括号部分其实是一个匿名内部子类
        @Override
        public double calculate(double x, double y) {
            return x + y;
        }
    },
    // 用于执行减法运算
    MINUS { // 花括号部分其实是一个匿名内部子类
        @Override
        public double calculate(double x, double y) {
            // TODO Auto-generated method stub
            return x - y;
        }
    },
    // 用于执行乘法运算
    TIMES { // 花括号部分其实是一个匿名内部子类
        @Override
        public double calculate(double x, double y) {
            return x * y;
        }
    },
    // 用于执行除法运算
    DIVIDE { // 花括号部分其实是一个匿名内部子类
        @Override
        public double calculate(double x, double y) {
            return x / y;
        }
    };
    //为该枚举类定义一个抽象方法，枚举类中所有的枚举值都必须实现这个方法
    public abstract double calculate(double x, double y);

}
```

## 第六章 访问权限控制

public：所有人

private：类创建者和内部方法

protected：修饰的成员对于本包和其子类可见

- 基类的protected成员是包内可见的，并且对子类可见；
- 若子类与基类不在同一包中，那么在子类中，子类实例可以访问其从基类继承而来的protected方法，而不能访问基类实例的protected方法。

默认：包访问权限（有时也表示成friendly）

```
            │ Class │ Package │ Subclass │ Subclass │ World
            │       │         │(same pkg)│(diff pkg)│ 
────────────┼───────┼─────────┼──────────┼──────────┼────────
public      │   +   │    +    │    +     │     +    │   +     
────────────┼───────┼─────────┼──────────┼──────────┼────────
protected   │   +   │    +    │    +     │     +    │         
────────────┼───────┼─────────┼──────────┼──────────┼────────
no modifier │   +   │    +    │    +     │          │    
────────────┼───────┼─────────┼──────────┼──────────┼────────
private     │   +   │         │          │          │    

 + : accessible         blank : not accessible
```

### 类访问权限

如果不加默认是包访问权限：只有同一包下的类可以创建该类对象，但如果此类有一个public static的字段，则包外的类仍可以使用此字段

## 第七章 复用类

**相比于继承，我们更优先使用组合**

###组合

类字段里包含其他类的对象引用（显示的用到其他类的行为）

###继承

子类对象里都有一个隐藏的基类对象：初始化子类之前必须初始化基类（隐式的用到其他类的行为）

### 代理

主要作用，还是在不修改被代理对象的源码上，进行功能的增强。这在 AOP 面向切面编程领域经常见。

https://blog.csdn.net/briblue/article/details/73928350

### final关键字

**编译器常量**：staic和final同时修饰的基本数据类型，定义时必须赋值

final可以用来修饰对象引用，但是这个意义仅在于对象引用只能永远指向这个对象，**但对象本身仍然可以被更改**

**final字段必须在定义时赋值，或者是在构造函数中赋值**

**final方法**：为了防止被子类覆盖，**private方法隐含就是final方法**

**final类**：禁止继承，其所有方法都默认是final方法

### 类的加载

**类是在其任何static成员第一次被访问时加载的，构造函数也是（static）**

**静态代码块：**用staitc声明，jvm加载类时执行，仅执行一次
**构造代码块：**类中直接用{}定义，每一次创建对象时执行。
**执行顺序优先级：**静态块 > main() > 实例变量初始化 > 构造代码块 > 构造函数

其实实际上 实例变量初始化和构造代码块（实例代码块） 实际上是放在构造函数的超类构造函数之后，本类构造代码之前

## 第八章 多态（又名动态或后期或运行时绑定）

**绑定**：将方法的调用和方法主体关联起来

**前期绑定**：在程序执行前绑定（面向过程语言默认）

**后期绑定**：运行时根据对象的类型进行绑定

**向上转型的使用场景**：在要求基类对象的地方，传入子类方法，这样就不用为每一个子类都单独写一个实现的方法（**多态去耦合**）

**Java中除类static和final方法（private属于final方法）之外，其他方法都是后期绑定**

**协变返回类型**：子类重写的基类方法可以返回基类方法返回类型的子类类型

### 纯粹继承与扩展

**纯粹继承（is-a关系）**：导出类只覆盖基类已有的方法，导出类和基类之间可以相互替换

**扩展（is-like-a关系）**：导出类有额外的新方法，向上转型后这些方法就无法调用

**向下转型是不安全的**：**java对所有转型都会进行检查**

**状态模式(State Pattern)**。利用多态，状态模式可以在runtime改变内部组件的类型，从而完全改变类的行为，因此比继承更灵活。

**继承来表现行为间的差异，字段来表现状态上的变化**

## 第九章 接口

**优先使用类而不是接口**

**接口和内部类提供了一种将接口和实现分离的更加结构化的方法**

### 抽象类（类和接口的折中）

**有抽象方法的类是抽象类，抽象类不一定有抽象方法**（**禁止一个类创建对象**，**但它又不需要抽象方法**）

```java
abstract void f();//抽象方法没有方法体
```

**继承抽象类的导出类必须实现所有抽象方法，否则其本身也需要加上abstract关键字，成为抽象类**

相比于接口，抽象类还可以有具体实现

### 接口

**完全抽象的类**

**使用接口的核心原因**：为了能够向上转型为多个基类型（以及由此带来的灵活性）

**接口的域**：**默认就是public static final**

**接口方法**：**默认就是public abstract的**

**接口没有构造器**

接口的多态性是指实现接口的类重写接口的抽象方法

接口可以通过extends接口来扩展接口

接口最常用场景：**策略设计模式**，体现在，一个方法提供一个接口类型的参数，让调用者传入有接口具体实现的类的对象，即不同类型的对象来得到了不同的实现。

jdk 1.5之前（没有enum关键字），接口被用来创建常量组

**接口可以嵌套在类或接口里**：但实现接口时，不需要实现其内部嵌套的接口。且private接口只能在其定义类里被实现

**接口与工厂**：https://www.zhihu.com/question/30351872

## 第十章 内部类（不同于组合）

### 普通内部类（成员内部类）

**自动拥有一个指向外部类对象的“秘密”引用**

要从外部类的非静态方法创建内部类对象，则需要使用OuterClass.InnerClass

**不能有static成员**

**内部类具有外部类所有元素的访问权**

**内部类使用其外部类的对象**:**OuterClass.this**

**其他类直接创建内部类对象**(**.new**)：先创建一个外部类对象 outer ，OuterClass.InnerClass inner = outer.new InnerClass();

**静态内部类（嵌套类）其实就相当于成为了一个顶级类**

### private 内部类

完全阻止依赖于类型的编码、隐藏了实现细节、无法访问不属于公共接口的方法

**内部类向上转型**：内部类实现了一个外部接口，但调用者访问其外部类提供的方法，得到一个内部类提供的向上转型的接口类型的引用，隐藏了实现细节

### 局部内部类（方法和任意作用域里的内部类）

**为什么需要？**

- 实现接口，创建并返回对其的引用
- 创建类，不希望其公共可用

作用域和普通变量一样

**不能有public、protected、private以及static修饰符的。**

**什么时候用局部不用匿名内部类？**：需要一个命名的构造器，需要不止一个该内部类对象

### 匿名内部类

**说明：**返回值的生成，与表示这个返回值的类的定义结合在一起

通过new表达式返回的引用自动向上转型

**只能访问外部final对象**

**特点：1.扩展or实现接口，只能做一样 2.只能实现一个接口**

**工厂方法：**不必再单独实现一个具体的工厂类，直接在不同类型的实现类里定义一个工厂类型的static字段即可，直接用匿名内部类来给这个字段返回具体的工厂对象

###嵌套类（静态内部类）

**特点：**

- 创建嵌套类对象时，不需要外部类对象.new
- 嵌套类不能访问外部类非静态成员
- 可以有static成员

**用途：**

- 接口嵌套类，**成为接口的一部分**。用于创建公共代码，供接口的不同实现共同使用
- 嵌套类用做测试类，写测试代码

### 为什么需要内部类

**内部类拥有外围类的所有元素的访问权限**

**最吸引人的原因：**每个内部类可以单独实现一个接口，无论外部类是否已经继承了某个接口的实现，对于内部类都没有影响

**内部类可以很好的实现隐藏。**一般的非内部类，是不允许有 private 与protected权限的，但内部类可以

**多重继承**：不同内部类继承多个不同**非接口类型（类和抽象类）**，或者内部类和外部类继承了不同**非接口类型（类和抽象类）**，因为接口本身就允许多继承

多个内部类可以对应同一个接口的不同实现（控制框架）

内部类没有is-a关系的困扰，是一个独立实体

### 闭包与回调

**闭包**：是一个**可调用对象**，记录了**来自于创建它的作用域的信息**，内部类是面向对象的闭包

**回调**：对象携带信息，在某一时刻调用初始对象

**JAVA并不能显式地支持闭包，但是在JAVA中，闭包可以通过“接口+内部类”来实现。**

（内部类实现外部的一个接口，这样外部就可以接受内部类）

### 控制框架

解决响应事件的需求，常见于GUI，事件驱动系统

抽象出控制Event的共有行为成接口

由不同内部类来继承该同一个接口，完成不同的具体实现

### 内部类的继承

内部类的导出类，必须实现一个带参数的构造方法，传入的是外部类的对象

**因为这个导出类的基类，也就是内部类是有一个“秘密”的指向其导出类对象的引用的**

**必须在此构造函数第一行使用enclosingClassReference.super()**

**注意：一般导出类里使用super是获取一个指向基类对象的引用**

```java
//WithInner外部类，Inner内部类，test3继承Inner
class test3 extends WithInner.Inner{
    test3(WithInner wi){
        wi.super();//enclosingClassReference.super(),这里和一般导出类的super不一样
    }
}
```

**至此这个导出类在创建对象时才具有基本的环境**

### 内部类不能被覆盖

继承一个外部类时，其非private的内部类是不会被导出类中的同名内部类覆盖的，他们独立于不同的命名空间

### 内部类标识符（Class文件）

外部类**$**内部类，如果是匿名内部类，那么内部类名是一个数字

## 第十一章 持有对象

**使用场景：**用于**保存对象引用**，但不知道具体会有多少对象，而**数组又有固定的尺寸**，此时用到**容器类（集合类）**

**预定义范型**

```java
List<Apple> apples = new ArrayList<>(); //这里使用List接收是因为，修改不同类型List只用在定义处修改
Arrays.<Apple>asList()//这里是 显式类型参数说明
```

尖括号里是**类型参数（支持向上转型）**

![image-20190224132228623](https://ws2.sinaimg.cn/large/006tKfTcgy1g0hg1s3zvvj31220mmah6.jpg)

### Collection（集合， 最高层接口，公共基类，继承自Iterable）

**Collection对象初始化方法**

```java
Arrays.asList() //接收数组或一组泛型类型的可变参数的元素列表,此种情况下，底层为数组，改变List长度就会报UnsupportedOperationException错
Collections.addAll(Collection c, T... list) //接收需要初始化的Collection对象，以及数组或可变参数元素列表
Collection.addAll(Cllection c) //这个是由已经定义的Collection对象调用，往自身添加另一个Collection的全部元素，没有Collections.addAll灵活
```

独立元素的**序列**，槽内只有一个元素，Collection包含List、Set、Queue

#### 1.List（接口）

**允许重复元素，按插入顺序分为：**

**ArrayList（实体类）**：**动态数组实现**，适合随机访问

**Vector（实体类）** ：和 ArrayList 类似，但它是线程安全的，过时的，**不要使用**

**LinkedList（实体类，实现了Queue和List接口）**：**链表实现**，适合随机存储，<u>包含的操作也多于ArrayList</u>

添加了作为Stack（栈）、Queue（队列）、double-ended queue（双端队列）的**方法**

**Stack（实体类，Java 1.0实现，已过时）**：先进后出（FILO）

**LinkedList支持的方法可以产生更好的Stack**

```java
public class Stack<T>{
    private LinkedList<T> storage = new LinkedList<>();
    public void push(T v) {storage.addFirst(v);}
    public T peek() {return storage.getFirst();}
    public pop() {return storage.removeFirst();}
    public boolean empty() {return storage.isEmpty();}
    public String toString {return storage.toString();}
}
```

#### 2.Set（接口，All Set is a Collection except TreeSet）

**不允许重复元素，查找是Set最重要的操作**

**HashSet：**散列函数->查找最快**O(1)**，**不考虑存储顺序**

**TreeSet：** **红黑树**->按照比较结果的升序保存对象（可以传入**Comparator**），查找**O(logN)**

**LinkedHashSet(实体类，继承自HashSet)：** **链表维护插入顺序**，具有HashSet查找效率

#### 3.Queue（接口，FIFO）

只允许在容器一端插入对象，并从另一端一移除对象

**可靠的将对象从程序某个区域传输到另一个区域的途径**

```java
Queue.offer() //将元素插入队尾，或返回false
Queue.peek()和Queue.element() //返回队头，若不存在，返回null 和 NoSuchElementExcpetion
Queue.poll()和Queue.remove() //移除并返回队头，若不存在，返回null 和 NoSuchElementExcpetion
```

**LinkedList（实体类，实现了Queue和List接口）**：

getFirst() 等于 element()：返回列表第一个元素

removeFirst ()等于 remove()：移除并返回列表第一个元素

addFirst() 等于 add() 等于 addLast()：都将元素插入列表尾端

removeLast()：移除并返回列表最后一个元素

**PriorityQueue（实体类，优先队列）：** **基于堆结构实现**，可以传入**Comparator**来自定义优先级（默认使用**自然排序**），peek、poll和removce是获取队列优先级最高的元素

---

###Map（又名映射，关联数组，最高层接口，公共基类）

**除了用另一个Map，未提供自动初始化的方式**

每个槽内保存了两个对象，键值对

####1.HashMap（实体类）

哈希实现，提供了最快的查找速度

#### 2.Hashtable（实体类）

和 HashMap 类似，但它是线程安全的，这意味着同一时刻多个线程可以同时写入 HashTable 并且不会导致数据不一致。它是遗留类，**不应该去使用它**

####3.TreeMap（实体类）

**红黑树**实现

####4.LinkedHashMap（实体类，继承自HashMap）

 **链表维护插入顺序**，保留了HashMap的查询速度。**顺序为插入顺序或者最近最少使用（LRU）顺序**

---

###容器中的设计模式

### 迭代器模式

#### Iterator（接口）

- 统一了容器的访问方式
- **只能单向移动**
- **foreach隐式包含了Iterator！！！！！！**

```java
Iterator.next() //获取下一元素
Iterator.hasNext() //检查是否还有元素
Iterator.remove() //从列表中删除迭代器新近返回的元素
```

**调用remove之前必须调用next，并且调用next后还只能调用一次remove**

https://blog.csdn.net/qq_34115899/article/details/81978660（？？？但这和我测试的不一样，Java 8 foreach list.remove并没有报错）

#### ListIterator(接口，仅用于List)

- 更强大的Iterator子类型

- **可以向前移动**

- 可以产生当前位置的前一个和后一个元素索引

#### Colleciton和Iterator

在C++中，没有提供容器的公共基类，C++仅通过迭代器来达成容器之间的共性。

**Java把这两种达成容器共性的方式绑定在一起：**公共基类（Collection），提供统一访问模式迭代器（Iterator）

同时实现Collection就必须实现其iterator()

Java提供了**AbstactCollection（抽象类）**作为**Collection的默认实现**

**而当实现一个不是Collection的外部类时**，实现Collection接口约束很多（要实现所有方法），继承AbstactCollection也不是一个很好的选择（因为可能已经继承了其他类），这时为这个类**构建一个返回Iterator类型对象的方法（这个方法的返回利用了匿名内部类P243）**则是将队列和消费队列的方法连接在一起耦合度最小的方式。

#### Foreach和迭代器

foreach主要用于数组，但是也可以用于**所有Collection对象**

因为Java SE 5引入的**Iterable接口**，其包含了一个产生Iterator类型对象的iterator()方法

如果实现了**Iterable接口**，就可以使用foreach方法

**Collection接口继承自Iterable接口**（接口可以继承多个接口）

**数组不是Iterable类型，也不存在自动转换**

### 适配器模式

希望构造一个自己的ArrayList，并且在拥有默认的前向Iterator的同时，也拥有一个逆序的Iterator

这个时候如果直接继承ArrayList并改写其iterator方法，只能实现一个功能的Iterator

适配器模式：继承ArrayList，保留原有的iterator方法不变，新写一个返回逆序Iterator类型对象的方法**（这个方法的返回利用了匿名内部类P243）**

java.util.Arrays#asList()把数组类型转换为List类型，接收数组或一组**泛型类型的可变参数的元素列表**

由于是**泛型类型**可变参数列表，这里不能使用基本数据类型，只能使用相应的包装类型数组

**注意：** **Arrays.asList()方法产生的List是使用的底层数组作为其实现**，如果执行的操作不想修改这个底层数组就必须在外面再包一层，创建一个副本进行操作，如 new ArrayList(Arrays.asList())。

这也是为什么直接修改Arrays.asList()返回List的长度会报**UnsupportedOperationException**错的原因

---

### 总结

数组和Collection都是建立了**数字索引和对象**之间的关联

**数组：**支持基本数据类型，只能存放同一类型，长度不变

**Collection：**不支持基本数据类型，可以存放不同类型（一般不这么做），长度可变

**Map：**建立**对象和对象**之间的关联

**Map和Collection之间唯一的重叠：**Collection\<V> Map.values()，Set\<K> keySet()

不要使用过时的**Vector，Hashtable，Stack**

## 第十二章 通过异常处理错误

**异常的重要目标：**把错误处理代码和错误发生地点相分离

粉色是**checked exceptions**，其必须被 try{}catch语句块所捕获,或者在方法签名里通过throws子句声明

**Java编译器要进行检查,Java虚拟机也要进行检查,以确保这个规则得到遵守.**

**runtime exceptions**：需要程序员自己分析代码决定是否捕获和处理,比如 空指针,被0除...
而声明为Error的，则属于严重错误,需要根据业务信息进行特殊处理,Error不需要捕捉。

![1383051170_4167](https://ws2.sinaimg.cn/large/006tKfTcgy1g0hl1t2ru2j30oj1ee77i.jpg)

### 异常参数

标准异常类有两个构造器

- 默认构造器
- 接受字符串参数的构造器

**Throwbale**是异常类型的根类

### 捕获异常

监控区域（guarded region）：一段可能产生异常的代码，并且后面跟着处理这些异常的代码

异常处理程序（catch块）

**终止与恢复模型**：Java与C++都是用终止模型。即异常发生后不会在处理后尝试再次执行异常程序，好处是不需要了解异常抛出的地点，相比恢复模型降低了耦合

e.printStackTrace()方法打印**从方法调用处直到异常抛出处的方法调用序列**，默认打印到标准错误流

e.printStackTrace(System.out)打印到控制台

### 异常说明

**跟在方法名后的throws关键字描述的异常**

这样做的好处是，不用暴露源码也能提醒使用者处理异常

这种在编译时被强制检查的异常成为**被检查的异常（checked exceptions）**

### 捕获所有异常

printStacTrace()打印的信息可以通过getStackTrace()得到

getStackTrace()返回的是一个由**Java虚拟机栈（VM Stack，JVM运行时数据区之一）**返回的栈轨迹

####重新抛出异常

如果在catch块里重新抛出当前异常对象，则异常抛出点不会变，异常抛给上一级程序

如果是在catch块里调用，**fillInStackTrace()**方法返回了一个Throwable对象，则调用此方法的这一行变成了一场抛出点（**这和在catch块里发生了一个新的异常是同样的效果**）

#### 异常链

把原始异常信息传递给新的异常

Java 5之后，Throwable的子类在**构造器**中可以接收一个**cause对象（表示原始异常）**作为参数，用于传递给新异常

但只有**Error，Exception，RuntimException**三个子类提供带cause参数的构造器，链接**其他类型异常**需要使用**initCause()方法**

### 使用finally进行清理

finally处理**内存回收之外（内存由GC处理）的清理**：已打开的文件和网络连接，屏幕上图形等

**finally永远会执行：**

- 即使try块中抛出了catch块无法catch的异常
- 即使try块中有break和continue
- 即使try块中有return

#### 异常丢失

- 在finally块中return：没有任何输出
- 在finally块中抛出新异常：只会存在finally块中的异常

### 异常的限制

当继承类或实现接口时，**至多只允许抛出基类方法异常说明中包含的异常类型**（即派生类override的基类方法最少可以不抛出任何异常，但最多只能抛出基类方法包含的异常，**或者是这些异常的派生类异常**）

**这个限制的原因：**保证派生类对象向上转型的时候，对基类对象的方法调用能够正常运行

1. **派生类override方法异常说明 <= 基类对应方法异常说明**

以上限制和构造器无关

但由于派生类构造器会调用基类构造器，所以

2. **派生类构造器异常说明 >= 基类构造器异常说明**

### 构造器

构造器中异常，用finally来清理，可能**在异常抛出时清理对象还没初始化**，而finally却对其清理。

**最安全的处理方式：使用嵌套的try catch子句**

### 异常匹配

catch 基类异常可以捕获其所有派生类异常

### 其他

harmful if swallowed（吞噬则有害）

即catch块里不做任何操作，这样会让异常消失。

**一种处理方式是，直接在catch 块里throw RunTimeException(e)**

## 第十三章 字符串

### 不可变String（只读）

任何会修改String值的方法，都是创建了一个全新的String对象

**参数就本应是给方法提供信息的，而不是让方法改变自己的**

### 重载 + 和 StringBuilder（Java SE 5引入，之前 StringBuffer 线程安全）

重载：一个操作符在应用于特定的类时，被赋予特殊的意义（String的+和+=是Java仅有的重载过的操作符）

Java不允许程序员重载任何操作符，C++允许

如下，编译器会优化操作符，自动引入StringBuilder，使用其append，避免多次new String带来的开销

```java
String s = "a" + "b" + 47;
```

但当在循环里使用重载操作符的时候，**StringBuilder是在循环体内部构造的，每一次都会new一个，效率低**

```java
String s = "";
for(String field : fields){
    s += field;
}
```

所以应该在循环内部显示的使用StringBuilder

### 无意识的递归

重写类的toString方法时，如果要打印此类对象内存地址，使用了this，那么会引发递归调用

```java
public String toString(){
    return this;
}
```

这里this返回的是本类的一个对象引用，但返回值是String，那么会调用此对象的toString，导致了递归调用

应该使用Object.toString()，即**用super.toString()**

### 格式化输出（Java SE 5）

来源于C语言的printf()方法

#### System.out.format() <=> System.out.printf()

可用于**PrintStream**和**PrintWriter**对象

#### Formatter类

构造器可以接受多种输出目的地，常用**PrintStream**， **OutputStream**和**File**

- 提供对空格和对齐的强大控制力
- 类型转换

**String.format：**String类的静态方法，接收和Formatter.format一样的参数，返回格式化的String，内部实现也是用一个**Formatter对象**

### 正则表达式

**注意Java String中的转义字符和正则表达式转义字符的区别**

Java String中的 “\\\\\\\” = \\\\(正则中的\\)

####String中的正则表达式

- String.matches(String regex)：检查String是否和正则表达式匹配，返回true or false
- String.split(String regex )：就是将字符串从正则表达式匹配的地方切开
- String.replaceAll，String.replaceFirst()

**如果不是只用一次，String以外的正则表达式具有更佳的性能**

####Pattern（java.util.regex）

Pattern.compile功能更强大的正则表达式对象