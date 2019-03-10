# ****Thinking**** in Java

## 第1章 对象导论

### 面向对象

1. **封装**： 把描述一个对象的属性和行为的代码封装在一个模块中，也就是一个类中，属性用变量定义，行为用方法进行定义，方法可以直接访问同一个对象中的属性。
2. **抽象**： 把现实生活中的对象抽象为类。分为 过程抽象 和 数据抽象

- 数据抽象 -->鸟有翅膀,羽毛等(类的属性)
- 过程抽象 -->鸟会飞,会叫(类的方法)

1. **继承**：子类继承父类的特征和行为。子类可以有父类的方法，属性（非private）。子类也可以对父类进行扩展，也可以重写父类的方法。<u>缺点就是提高代码之间的耦合性</u>。
2. **多态**： 多态是指程序中定义的引用变量所指向的 <u>具体类型</u> 和通过该引用变量 <u>发出的方法调用</u> 在编程时并不确定
- 编译时多态：方法重载
- 运行时多态：与重写有关，子类向上转型

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

**编译期常量**：staic和final同时修饰的基本数据类型，定义时必须赋值（**不需要对类进行初始化就可以读取**）

final可以用来修饰对象引用，但是这个意义仅在于对象引用只能永远指向这个对象，**但对象本身仍然可以被更改**

**final字段必须在定义时赋值，或者是在构造函数中赋值**

**final方法**：为了防止被子类覆盖，**private方法隐含就是final方法**

**final类**：禁止继承，其所有方法都默认是final方法

### 类的加载

**类是在其任何static成员第一次被访问时加载的，构造函数也是（static）**

**静态代码块：**用staitc声明，jvm加载类时执行，仅执行一次

**构造代码块：**类中直接用{}定义，每一次创建对象时执行

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

接口**可以通过extends接口来扩展接口**

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
    public T pop() {return storage.removeFirst();}
    public boolean empty() {return storage.isEmpty();}
    public String toString() {return storage.toString();}
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

**PriorityQueue（实体类，优先队列）：** **基于堆结构实现**，可以传入**Comparator**来自定义优先级（默认使用**自然排序**），peek、poll和remove是获取队列优先级最高的元素

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

不要使用Java 1.0过时的**Vector，Hashtable，Stack**

## 第十二章 通过异常处理错误

**异常的重要目标：**把错误处理代码和错误发生地点相分离

粉色是**checked exceptions**，其必须被 try{}catch语句块所捕获,或者在方法签名里通过throws子句声明

**Java编译器要进行检查,Java虚拟机也要进行检查,以确保这个规则得到遵守.**

### Error和Exception的区别

**Error类**：一般是指与JVM相关的问题，如系统崩溃，虚拟机错误，内存空间不足，方法调用栈溢等。对于这类错误的导致的应用程序中断，仅靠程序本身无法恢复和预防，遇到这样的错误，建议让程序终止。

 **Exception类**：表示**程序可以处理的异常**，可以捕获且可能恢复。遇到这类异常，应该尽可能处理异常，使程序恢复运行，而不应该随意终止异常

**runtime exceptions**：需要程序员自己分析代码决定是否捕获和处理,比如 空指针,被0除...
而声明为**Error的，则属于严重错误,需要根据业务信息进行特殊处理,Error不需要捕捉**。

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

#### unchecked and checked exceptions

**未检查的异常（unchecked exceptions）**：Error和RuntimeException 及其子类

**检查了的异常（checked exceptions）**：所有其他的Exception类都是，通常是从一个可以恢复的程序中抛出来的，并且最好能够从这种异常中使用程序恢复。

### 捕获所有异常

printStackTrace()打印的信息可以通过getStackTrace()得到

getStackTrace()返回的是一个由**Java虚拟机栈（VM Stack，JVM运行时数据区之一）**返回的栈轨迹

####重新抛出异常

如果在catch块里重新抛出当前异常对象，则异常抛出点不会变，异常抛给上一级程序

如果是在catch块里调用，**fillInStackTrace()**方法返回了一个Throwable对象，则调用此方法的这一行变成了一场抛出点（**这和在catch块里发生了一个新的异常是同样的效果**）

#### 异常链

把原始异常信息传递给新的异常

Java 5之后，Throwable的子类在**构造器**中可以接收一个**cause对象（表示原始异常）**作为参数，用于传递给新异常

但只有**Error，Exception，RuntimeException**三个子类提供带cause参数的构造器，链接**其他类型异常**需要使用**initCause()方法**

### 使用finally进行清理

finally处理**内存回收之外（内存由GC处理）的清理**：已打开的文件和网络连接，屏幕上图形等

**finally永远会执行（除非这是dameon线程run方法里的finally，那么有可能无法执行）：**

- 即使try块中抛出了catch块无法catch的异常
- 即使try块中有break和continue
- 即使try块中有return

#### 异常丢失

- 在finally块中return：没有任何输出
- 在finally块中抛出新异常：只会存在finally块中的异常

### 异常的限制（为满足里氏代换原则）

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

**catch 基类异常可以捕获其所有派生类异常**

### 其他

harmful if swallowed（吞噬则有害）

即catch块里不做任何操作，这样会让异常消失。

**一种处理方式是，直接在catch 块里throw RunTimeException(e)**

## 第十三章 字符串

### 不可变String（只读）

任何会修改String值的方法，都是创建了一个全新的String对象

**注意字符串常量池的概念，代码里所有“test”字符串都会在编译期确定，放入字符串常量池**

```java
 String s1 = “first”;
 String s2 = new String(“second”);
s1:中的”first” 是字符串常量，在编译期就被确定了，先检查字符串常量池中是否含有”first”字符串,若没有则添加”first”到字符串常量池中，并且直接指向它。所以s1直接指向字符串常量池的”first”对象。
s2:用new String() 创建的字符串不是常量，不能在编译期就确定，所以new String() 创建的字符串不放入常量池中，它们在堆里有自己的地址空间,然后堆里的这个String对象指向常量池的”second“。 但是”second”字符串常量在编译期也会被加入到字符串常量池
```

#### 参数就本应是给方法提供信息的，而不是让方法改变自己的

### 重载 + 和 StringBuilder（Java SE 5引入，之前 StringBuffer 线程安全）

重载：一个操作符在应用于特定的类时，被赋予特殊的意义（String的+和+=是**Java仅有的重载过的操作符**）

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

重写类的toString方法时，如果要**打印此类对象内存地址**，使用了this，那么会引发递归调用

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

## 第十四章 类型信息

**RTTI（Run-time type identification）运行时状态识别**

#### 多态

使用基类引用调用基类方法，但此方法在所有派生类里都有不同实现，并且是动态绑定的，所以都能产生正确的行为，这就是多态。

### Class对象（运行时类型信息的表示，Java依赖其完成RTTI）

每编译一个新类就会为其生成Class对象，保存在.class文件

**无论我们对引用进行怎样的类型转换，对象本身所对应的Class对象都是同一个**。由于Class对象的存在，Java不会因为类型的向上转换而迷失。这就是**多态的原理**。

**Class类（所有Class对象都属于这个类）的静态方法**

**Class.forName("全限定ClassName")** 获得该Class对象的引用，但**返回值通常被忽略**，相当于手动加载此类

Object.getClass()获取当前类的Class对象

Class.newInstance()实现**虚拟构造器**的一种方式

为了使用类做的准备工作

**加载：**类加载器执行。查找字节码.class，并创建一个Class对象

**链接：**验证类中的字节码，为静态域分配空间，有必要的话解析这个类创建的对其他类的引用

**初始化：**如果有超类，对其初始化，执行静态初始化器和静态初始化块

#### 类字面常量（也是获得Class对象的引用，但不会初始化类）

**ClassName.class**，可以用于普通类，接口，数组以及基本数据类型（**等价于基本类型包装器的TYPE字段**）

**！！不同于Class.forName()，使用类字面常量的时候不会自动初始化Class对象！！**，被延迟到了对静态域首次引用时才执行

如果一个域是staic非final，那么读取前必须要进行**链接和初始化**

#### 泛化的Class引用

Java SE 5加入的泛型

```java
Class<Integer> intClass = int.class; //泛型使得编译器强制执行了额外的类型检查
Class<Number> numberClass = int.class;//报错，即使Integer继承于Number，但Integer Class不是 Number Class的子类
```

**泛型通配符 ?，搭配extends使用**

```java
Class<? extends Number> numberClass = int.class;//正确，使得Class引用nuberClass可以接受Number类和其所有导出类的Class对象
```

#### 新的转型语法

**转型多指向下转型，编译器检查向下转型正确性，**向上转型不需要检查（编译器允许自由的向上转型）

Java SE 5添加的转型语法，**用于普通转型无法使用的情况**

Class对象引用的方法

**Class.cast(Object obj)**：将参数obj对象转换成Class引用的类型

**普通转型：**(ClassName)obj

### RTTI三种形式

1. 传统类型转换，如（Shape）
2. 代表对象类型的Class对象
3. 关键字instance of（等价于Object.isInstance()）

### instanceof和Class的等价性

查询类型信息时，instanceOf()和直接比较Class对象有区别

equals和==直接比较Class对象是否相等，比较的是**是否为确切的这个类型**

而instanceof指的是，**你是这个类吗，或者你是这个类的派生类吗**

### 反射（Class类和java.lang.reflect共同支持）

**产生背景：**RTTI的限制，类型必须在编译时已知，才能够通过RTTI来识别

JavaBeans，RMI

**但如果我们想要在运行时，获取编译时不知道的类（未知类）的信息，需要用到反射**

**RTTI：**在编译时获取.class文件

**反射：**在运行时获取.class文件

**java.lang.reflect（类库）：**包含Field、Method、Constructor

### 动态代理（P338）

### 空对象（没太看懂）

## 第十五章 泛型（Java SE 5引入的重大变化）

**产生背景：**要编写可以应用于多种类型的代码

实现了**参数化**类型的概念

#### 元组（数据传送对象，信使）

```java
public class TwoTuple<A,B>(){
    public final A a;
    public final B b;
    public TwoTuple(A a, B b){
        this.a = a;
        this.b = b;
    }
    public String toString(){
        return "(" + a + ", " + b + ")";
    }
}
```

### 生成器（P358）

**工厂设计模式的一种应用**：只是工厂方法需要提供参数，但生成器不需要

###泛型方法（泛型参数置于返回值前）

**泛型方法和其所属类是否为泛型类没有关系**，**优先使用泛型方法**而不是泛化整个类

**static方法无法访问泛型类的类型参数**（因为泛型类的类型是在创建对象时指定的，而static方法在此之前就可以被调用）

```java
    public static <T> ArrayList<T> f(T a){}
```

#### 泛型方法的显示类型参数说明（很少用）

在点操作符与方法名之间插入尖括号说明类型 Arrays.\<Apple>asList()

### 擦除

**在泛型代码内部，无法获得任何有关泛型参数类型的信息**

**泛型→具体类型信息→被擦除**

### 边界（泛型的参数类型→设置限制条件）

**无界通配符<?>**

**超类型通配符（参数是下界）<? super T>**：某个特定类的任何基类

**\<T extends HasF>：**限制为HasF的类型子集

### 泛型最大的价值

使用容器类的地方

Java SE 5之前容器类里对象都是Object，放入时会丢失类型信息，取出时必须向下转型

## 第十六章 数组

在使用时，除非能确定效率和数组有关，否则，**优先使用容器而不是数组**

**和其他种类容器区别：**效率、类型、保存基本类型的能力

**效率最高**的**存储**和**随机访问对象引用序列**的方式

泛型出现后，数组最大的优点就是**效率**

对象数组元素**默认值为null**，基本类型数组默认值为其**作为类成员时的默认值**一样

### 数组是第一级对象

数组标识符是一个**引用**，指向**堆**中创建的一个**真实数组对象**，这个数组对象保存指向其他对象的引用

**length：**数组对象唯一一个可以访问的域

### 多维数组

**粗糙数组：**数组中构成矩阵的每个向量长度可以不一致

Arrays.deepToString()：将多维数组转换成多个String

### 数组与泛型

**不能实例化**具有参数化类型的数组（但可以创建一个参数化类型数组的引用，并实例化一个具体类型的数组转型赋值给该引用）

```java
List<String>[] ls = new ArrayList<>()[] //错误

List<String>[] ls；	//正确
List[] la = new List[10];
ls = (List<String>[])la;
```

**可以**参数化数组本身的类型，如 T []

### 创建测试数据

#### Arrays.fill()

用单一数据填充数组

#### 数据生成器（P443）

Generator中**嵌套多个不同类**，实现不同的生成器逻辑

**嵌套类使得可以使用和其要生成类型相同的名字，如嵌套类Integer，不会和外部的Integer冲突**

可以为不同的类型数据选择不同的生成器类型（**策略设计模式的实例**，每个不同生成器都是一个策略）

如为基本数据类型的包装器类型构造的CountingGenerator，内部用不同嵌套类实现不同类型生成器

调用时就可以 **new CountingGenerator.Integer()**

### Arrays实用功能

**equals()：**比较数组是否相等

**sort()：**对数组排序，**基本类型：快速排序，引用类型：稳定归并排序**

**binarySearch()：**对排序后数组查找元素（只能用于**已排序数组**）

**toString：**产生数组的String表示

**hashCode：**产生数组的哈希值

**asList()：**接收一个可变参数列表，生成List（但是此List的长度不能改变）

#### System.arraycopy()（复制数组，比for循环快很多）

复制数组，**支持基本类型数组和对象数组**，但不进行自动装箱和拆箱

### 数组排序

**Arrays.sort()默认只支持基本类型数组排序**

若要对对象数组排序，要求该类型**实现了Comparable接口或者有相关联的Comparator**

Arrays.sort(a)，要求对象数组a实现了Comparable接口

Arrays.sort(b, String.CASE_INSENSATIVE)，b是一个String数组，传入了String的一个Comparator

## 第十七章 容器深入研究

![Jietu20190227-133346@2x](https://ws4.sinaimg.cn/large/006tKfTcly1g0kx9cl2ohj30lm0kudjg.jpg)

### 填充容器

**所有的Collection子类都有一个构造器，接收一个Collection对象**，用接受的Collection对象来填充

**Collections.fill()：**类似Arrays对应方法，用单一数据**填充List容器（仅适用List容器）**

**Collections.nCopies(int n, T o)**：创建一个List, 里面包含n个T类型的对象o

**Generator**：可以编写一个适配器，将Gnerator适配到Collection 的构造器上

#### Map生成器

**需要一个二元组类**，因为Map构造器每次生成的应该是一个<K,V>对

#### 使用抽象类

**每个java.util容器都有自己的Abstract类**

### 可选操作和UnsupportedMethodException

Collection接口的添加和移除都是可选操作，意味着实现类不需要为这些方法提供实现

**为什么需要可选操作？**：防止出现接口爆炸的情况

- 因为在接口的有些实现类里，可选方法可能是完全没有意义的，调用该方法会抛出UnsupportedMethodException
- 如果创建了一个新的Collection类，但没有实现所有方法，它仍然适合现有的类库
- 从设计的角度来说，如果一个接口方法为可选的，表明这个方法只为某类特定的实现而设计的

比如Arrays.asList()产生了一个基于固定大小的数组的List，那么它的add，addAll，retain，retianAll方法都是没有意义的，调用则会引发UnsupportedMethodException异常

### Set和存储顺序

#### Set（接口）

存入元素必须唯一，**必须定义equals()方法**，不保证维护元素的次序

####HsahSet（默认使用，对速度进行了优化）

必须定义**hashCode()，equals()**

#### TreeSet（按对象的比较函数保持次序的Set，是SortedSet接口的唯一实现）

元素必须实现**Comparable接口，equals()**

```java
Comparator comparator() //返回当前Set使用的comparator，null则为自然排序
Object first() //返回第一个元素
Object last() //返回末尾元素
SortedSet subSet(fromElement, toElement) //获取子集
SortedSet headSet(toElement)	//获取小于toElement的子集
SortedSet tailSet(fromElement) //获取大于等于fromElement的子集 前闭后开
```

####LinkedHashSet（**保持次序的HashSet**）

必须定义**hashCode()，equals()**，内部用链表维护插入元素的顺序

### 队列（Queue）

Queue在Java SE 5中仅有两个实现**LinkedList**和**PriorityQueue**，两者**差异在于排序行为**而不是性能

**优先级队列（PriorityQueue）**基于堆实现

**双向队列（Double-ended queue）**：ArrayDeque（JDK 8），LinkedList也包含支持双向队列的方法

### 理解Map（又名映射表，关联数组）

**任何插入Map的对象都必须有equals方法**，如果用于HashMap，则要求有**恰当的hashCode**方法

#### HashMap（不关心顺序）

插入和查询键值对的开销是固定的

构造器设置**容量**和**负载因子**调整性能

**容量**：哈希表中的桶位数

**初始容量**：创建表时的桶位数

**尺寸**：当前存储项数

**负载因子**：尺寸/容量（默认0.75的时候会进行**再哈希**，如果知道自己要存多少数据，可以设置合理尺寸来避免再哈希）

#### LinkedHashMap（有序的，继承自HashMap）

插入和查询比HashMap慢一点点，但**迭代访问时反而更快**

**取出顺序是插入顺序，或者是LRU次序**

#### TreeMap（有序的，由Comparable或Comparator决定）

唯一有**subMap()方法**的Map，可以返回一个子树

#### WeakHashMap

保存**WeakReference**

value只保存一份实例，节省存储空间

允许释放映射所指的对象

如果映射之外，没有引用指向某个”键“，那么此”键“可以被GC回收（**不管内存是否够用**）

#### ConcurrentHashMap（线程安全）

不涉及同步加锁

#### IdentityHashMap（无序，key值可以重复，因为是==比较）

使用==代替equals对”键“进行比较的HashMap。专为解决特殊问题

1. IdentityHashMap有其特殊用途，比如序列化或者深度复制。或者记录对象代理。
2. 举个例子，jvm中的所有对象都是独一无二的，哪怕两个对象是同一个class的对象，而且两个对象的数据完全相同，对于jvm来说，他们也是完全不同的，如果要用一个map来记录这样jvm中的对象，你就需要用IdentityHashMap，而不能使用其他Map实现。

### 哈希和hashCode

哈希的目的：使用一个对象来查找另一个对象

哈希的价值：**用空间换时间**，维护了一个固定大小的哈希表（通常是个数组），通过计算的hashCode作为数组下标，然后用不同的策略解决冲突，**开放定址法**：线行探查法，平方探查法， **链地址法**，**再哈希法**，**建立公共溢出区**

哈希表中的每一个位置通常称为**桶（bucket）**，桶的数量用2的整数次方，可以减少求余的操作

#### String的hashCode

如果两个String对象的字符串相同，那么他们指向的是同一块内存区域（**字符串常量池某个位置**），**hashCode也相同**

#### 重写hashCode

1. 同一个对象调用hashCode必须产生相同的值
2. 速度快，且必须有意义
3. 能够产生均匀分布的hashCode

**Effective Java中的推荐做法：**

初始化一个非零常量值，如17

为对象内每个有意义的域都计算出一个int哈希码，然后全部相加，得到最后的哈希值

### 选择接口的不同实现

#### 对List的选择

需要注意，List的**LinkedList和LinkedHashSet、LinkedHashMap很不一样**

背后用数组支撑的**List和ArrayList**，随机访问不受列表大小影响

**LinkedList**访问速度受列表大小影响

**但随机插入的表现则正好相反**

#### 对Set的选择

HashSet性能基本上总比TreeSet好，特别是在**添加和查询**元素

**<u>TreeSet迭代比HashSet快</u>**

**！！！LinkedHashSet插入比HashSet慢，这是由于维护链表的开销造成的（这和List不一样）**

#### 对Map的选择

**除了IdentityHashMap**，**所有Map的插入都会随着容量增大而变慢**，但查找比插入代价少的多

Hashtable和HashMap性能相当

TreeMap通常比HashMap要慢

**！！！LinkedHashMap插入比HashMap慢一点，但是  <u>迭代要快</u> **

### Collection和Map的同步控制

####Collections自动同步整个容器（synchronized多线程中重要部分）

Collections.synchronizedList

Collections.synchronizedLMap

Collections.synchronizedSet

...

#### 快速报错（ConcurrentModificationException）

保护机制，防止**多个进程**同时修改同一个容器的内容

### 持有引用

Java.lang.ref类库，这些类为垃圾回收提供更大的灵活性，当**存在可能用尽内存的大对象的时候**，这些类会很有用

**继承自抽象类Reference**

当GC考察的对象，**只能通过某个Reference对象才能获得的时候**，以下类提供了不同级别的指示

以下三种引用对应的**“可获得性”**级别**由强到弱**

####SoftReference（内存不足就回收）

实现内存敏感的高速缓存，**在 JVM 报告内存不足情况之前将清除所有的软引用**。注意：对象是否被释放取决于垃圾收集器的算法以及垃圾收集器运行时可用的内存数量。

####WeakReference（GC看见就回收，不管内存是否充足）

为实现**规范映射**（canonicalized mapping）而设计，它**不妨碍GC回收映射的键**（或值）。规范映射的对象实例可以在程序中多处被使用，以节省存储空间。**如果对象只剩下一个weak引用，那GC的时候就会回收**（不管内存是否够用）。和`SoftReference`都可以用来实现cache

####PhantomReference（**必须与 `ReferenceQueue` 类一起使用，可用来替换finalize**）

**get方法永远返回null**

用于**调度回收前的清理工作**，比Java finalize更灵活

SoftReference、WeakReference放入**ReferenceQueue（用作回收前清理）**是**可选的**

但PhantomReference**必须依赖ReferenceQueue**

#### Java 中的`finalize`有哪些问题？

1. 影响 GC 性能，可能会引发`OutOfMemoryException`
2. `finalize`方法中对异常处理不当会影响 GC
3. 子类中未调用`super.finalize`会导致父类的`finalize`得不到执行

总结一下就是：实现`finalize`对代码的质量要求非常高，一旦使用不当，就容易引发各种问题。


### Java 1.0/1.1 的容器

Vector：Java 1.0/1.1中唯一可扩展序列

Enumeration（接口）：迭代器

Hashtable：类似HashMap

Stack：继承自Vector

BitSet：最小长度是long 64，用于存储大对象

## 第十八章 Java I/O系统

#### File 类

特定文件的名称

一个目录下一组文件的名称

**目录过滤器**：File.list(FilenameFilter f)，参数是FilenameFilter接口的一个实现（可以用匿名内部类）

### 输入和输出

#### 流

有能力产出数据的数据源对象

有能力接收数据的数据源对象

**Java输入**：InputStream（**字节**）或Reader（**Unicode字符**）派生 read()

**Java输出**：OutputStream（**字节**）或Writer（**Unicode字符**）派生 writer()

**产生“流”（装饰器模式）**：通过叠合多个对象来提供期望的功能

### 装饰器模式（Decorator Pattern，Wrapper）

> http://www.cnblogs.com/zuoxiaolong/p/pattern11.html

**定义**：装饰模式是在不必改变原类文件和使用继承的情况下，动态的扩展一个对象的功能。它是通过创建一个包装对象，也就是装饰来包裹真实的对象。

1. **不改变原类文件**
2. **不使用继承**
3. **动态扩展**

**优点**：灵活，动态扩展，用组合的方式取代了继承

**缺点**：增加了代码复杂性

![20130627214940437](https://ws3.sinaimg.cn/large/006tKfTcgy1g0n89z4vlsj310k0exad8.jpg)

### Java 1.0

#### InputStream（字节输入的超级父类，抽象类）

InputStream的**实体子类！**！！，**特别注意FilterInputStream（装饰器父类）**

| FilterInputStream                             | InputStream体系的装饰器父类          |
| --------------------------------------------- | ------------------------------------ |
| ByteArrayInputStream                          | 内存缓冲区                           |
| ~~StringBufferInputStream~~（**Deprecated**） | 字符串转换成InputStream              |
| FileInputStream                               | 从文件中读取信息                     |
| PipedInputStream                              | 多线程中数据源                       |
| SequenceInputStream                           | 多个InputStream转换成一个InputStream |

FilterInputStream的子类（**InputStream的所有装饰器**）

| DataInputStream（装饰器）                 | 按照可移植方式从流读取 <u>基本数据类型 和 String 对象</u> |
| ----------------------------------------- | --------------------------------------------------------- |
| BufferedInputStream（装饰器）             | 使用缓冲区读取数据                                        |
| ~~LineNumberInputStream~~(**Deprecated**) | 跟踪输入流的行号                                          |
| PushbackInputStream（装饰器）             | 弹出最后一个字节的缓冲区，可以将最后一个读到字符回退      |

#### OutputStream（字节输出的超级父类）

OutputStream的**实体子类**！！！，**特别注意FilterOutputStream（装饰器父类）**

| FilterOutputStream      | OutputStream体系的装饰器父类         |
| ----------------------- | ------------------------------------ |
| ByteArrayOutputStream   | 内存缓冲区                           |
| FileOututStream         | 写入文件                     |
| PipedOutputStream        | 写入其中数据都会作为PipedInputStream输入                       |

FilterOutputStream的子类（**OutputStream的所有装饰器**）

| DataOutputStream（装饰器）     | 按照可移植方式向流写入 <u>基本数据类型</u>                   |
| ------------------------------ | ------------------------------------------------------------ |
| BufferedOutputStream（装饰器） | 使用缓冲区写数据                                             |
| PrintStream（装饰器）          | **产生格式化输出**（DataOutputStream处理数据存储，PrintStream处理**显示**） |

----

Java 1.1，**新增Reader和Writer体系**，新类库也比旧类库**更快**

InputStream -> **InputStreamReader（适配器）**-> Reader

OutputStream -> **OutputStreamWriter（适配器）** -> Writer

**以下在Java 1.1没有对应的类**：

- DataOutputStream
- File
- RandomAccessFile
- SequenceInputStream

---

### Java 1.1

####Reader（字符输入的超级父类）

Reader的子类

| FilterReader              | Reader体系的装饰器父类（抽象类）                             |
| ------------------------- | ------------------------------------------------------------ |
| InputStreamReader         | InputStream转换为Reader的**适配器**                          |
| StringReader（装饰器）    | **注意：**这里没继承装饰器父类FilterReader！！！             |
| BufferedReader（装饰器）  | **注意：**这里没继承装饰器父类FilterReader！！！**只有在需要readLine的时候使用，此外优先使用DataInputStream** |
| CharArrayReader（装饰器） | **注意：**这里没继承装饰器父类FilterReader！！！             |
| PipedReader（装饰器） | **注意：**这里没继承装饰器父类FilterReader！！！             |


FilterReader的子类（**Reader装饰器**）

```
PushbackReader(装饰器)     |    注意：这和FilterInputStream很不一样
```

**其他装饰器：**

FileReader（装饰器） (继承自**InputStreamReader（适配器）**)

LineNumberReader（装饰器）（继承自**BufferedReader（装饰器）**）

####Writer（字符输入的超级父类）

Writer的子类

| FilterWriter              | Writer体系的装饰器父类（抽象类），没有任何子类！！！！！！！   |
| ------------------------- | ------------------------------------------------ |
| OutputStreamReader        | OutputStream转换为Writer的**适配器**             |
| StringWriter（装饰器）    | **注意：**这里没继承装饰器父类FilterWriter！！！ |
| BufferedWriter（装饰器）  | **注意：**这里没继承装饰器父类FilterWriter！！！ |
| CharArrayWriter（装饰器） | **注意：**这里没继承装饰器父类FilterWriter！！！ |
| PipedWriter（装饰器） | **注意：**这里没继承装饰器父类FilterWriter！！！ |
| **PrintWriter（装饰器，适配器）** | 1.为了从**PrintStream**过渡，提供了接收PrintStream对象接口                                 2.默认使用**BufferedWriter**，构造器可以提供一个Boolean**是否自动flush** |

**其他装饰器：**

FileWriter（装饰器）（继承自**OutputStreamWriter（适配器）**）

### 自我独立的RandomAccessFile

适用于大小已知的记录组成的文件

**可以在一个文件内向前向后移动**，类似于把DataInputStream和DataOutputStream组合使用（因为使用了相同的接口：DataInput和DataOutput）

**JDK 1.4后大多数功能被NIO中的内存映射文件替代**

### 标准I/O

**概念来自**：Unix中“程序所使用的单一信息流”

System.out（**包装好的PrintStream对象**）

System.err（**包装好的PrintStream对象**）

System.in（**未包装的InputStream对象**）：读取前必须进行包装

```java
BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
```

#### 标准I/O重定向（重定向的是@字节流@）

**System的静态方法：**

**setIn(InputStream)**

**setOut(PrintStream)**

**setErr(PrintStream)**

### 进程控制

使用java.lang.ProcessBuilder执行命令，然后返回一个Process

**获取命令执行时的标准输出流：**Process.getInputStream()

注意：这里不是获取OutputStream，因为**InputStream是唯一能够从里面获取数据的**

**获取命令执行时的标准错误流：**Process.getErrorStream()

如果要在InputStream里获取标准错误流，先调用**Process.redirectErrorStream(true)**再去获取InputStream

### 新I/O（NIO，**同步非阻塞**）

Java NIO 是 java 1.4, 之后新出的一套IO接口NIO中的N可以理解为Non-blocking，不单纯是New。

速度的提高来自于更接近操作系统执行I/O的方法：**通道和缓冲区**

### 通道分类

- **网络读写（SelectableChannel）**
- **文件操作（FileChannel）**

**唯一直接与通道交互的缓冲器就是ByteBuffer**

**NIO的特性/NIO与IO区别:**

- 1)IO是**面向流**的，NIO是**面向缓冲区（Buffer）**的
- 2)IO流是阻塞的，NIO流是不阻塞的
- 3)NIO有选择器，而IO没有。

**NIO核心组件简单介绍**

- **Channels**

- **Buffers**

- **Selectors**（方法选择集，用于以原始的**字节形式**或**基本数据类型**输出和读取数据，无法读取或输出对象）

**读数据和写数据方式:**（通道像煤矿，缓冲器是卡车）

  - 从通道进行数据读取 ：创建一个缓冲区，然后请求通道读取数据。
  - 从通道进行数据写入 ：创建一个缓冲区，填充数据，并要求通道写入数据。

**旧I/O类修改以产生FileChannel（注意：都是面向字节）**

- **FileInputStream**
- **FileOutputStream**
- **RandomAccessFile（即读又写）**

Reader和Writer这种**字符操作不能产生Channel**，但java.nio.channel.Channels提供了在通道中产生Reader和Writer 的方法 new Reader, new Writer

```java
FileChannel fc = new FileOutputStream("data.txt").getChannel();
fc.write(ByteBuffer.wrap("some text".getBytes()));	//这里是把ByteBuffer里的值写入通道
fc.close();
fc = new RandomAccessFile("data.txt","rw").getChannel();
fc.position(fc.size()); //移动到最后
fc.write(ByteBuffer.wrap("some more".getBytes()));
fc.close();
fc = new FileInputStream("data.txt").getChannel();
ByteBuffer buff = ByteBuffer.allcote(1024);	//对于只读访问，必须静态分配ByteBuffer
fc.read(buff);	//把通道里的值读到ByteBuffer里
buff.flip(); //准备缓冲器，以便从中读取信息，每次read后都要调用flip
while(buff.hasRemaining()){
    System.out.println((char)buff.get());
}
// 输出
//some text some more
```

#### 转换数据

缓冲器容纳的是普通字节，为了转换成有意义字符，要么在输入缓冲器时**编码**，要么在缓冲期输出时**解码**

```java
String encoding = System.getProperty("file.encoding");	//获取系统编码
System.out.println(CharSet.forName(encoding).decode(buff))； //用系统编码去解码buff直接输出
fc.write(ByteBuffer.wrap("some text").getBytes("UTF-16BE"));//写入buff的时候编码
fc.clear();
fc.read(buff);
fc.flip();
System.out.println(buff.asCharBuffer()); //直接转换成CharBuffer输出，调用了CharBuffer的toString()，由于写入fc时进行了编码，所以读出时直接转换成CharBuffer输出也不会乱码
```

#### 视图缓冲器

ByteBuffer只能保存字节数据，但是可以用不同的**基本类型视图去查看底层ByteBuffer**

通过ByteBuffer的不同视图，可以通过**put()方法为其添加不同的基本类型数据**，但**添加short数据时必须强制类型转换**

### 字节存放顺序

**big endian**：高位字节放在低地址存储单元（**默认**）

**little endian**：高位字节放在高存储单元

#### 缓冲器细节

![image-20190302165147490](https://ws1.sinaimg.cn/large/006tKfTcgy1g0ojtisc9ij31bu0lg11k.jpg)

#### 内存映射文件

允许创建和修改因为太大而不能放入内存的文件

FileChannel.map(FileChannel.MapMode.READ_WRITE, 0, length)

产生的**MapByteBuffer（特殊类型的直接缓冲器，继承自ByteBuffer，具有其所有方法）**

**建立映射的开销很大，但是整体收益比I/O流好**

#### 文件加锁（只能是通道上的，不能是缓冲器）

JDK1.4引入的文件加锁，允许**同步**访问某个作为共享资源的文件。

文件锁对于其他的操作系统进程是可见的，Java的文件锁**映射到了本地操作系统的加锁工具**

**FileLock fl = FileChannel.lock()**：阻塞

**FileLock fl = FileChannel.tryLock()**：非阻塞

**使用共享锁必须由操作系统底层支持，不支持则默认独占锁**

可以对**内存映射文件部分加锁**，例如，数据库就是这样，所以可以多个用户同时访问

**JVM会自动释放锁**，或者关闭加锁的通道，也可以显示的关闭 FileLock.release()

### 压缩

Java I/O中类库支持压缩的类从InputStream和OutputStream继承而来

**压缩按字节方式而不是字符方式**

**GZIP**：对单个数据流进行压缩

**Zip**：保存多个文件，用了Checksum类（Adler32，快，CRC32，准）来计算校验文件的校验和

**Java档案文件（JAR）**：包含一组压缩文件，和描述这些文件的文件清单

### 对象序列化

产生背景：在程序不运行的情况下仍能保存对象信息，再重新运行程序的时候就可以恢复到之前运行状态。

主要为了支持两种特性：RMI，Java Beans

**Java 默认的对象序列化**：**实现了Serializable接口**的对象转换成一个**字节**序列（跨平台）

**Serializable接口是一个标记接口，没有任何方法声明**

要从字节序列恢复一个对象，**必须保证JVM能找到对应的.class文件**

如下，写入序列化对象，和恢复序列化对象的方法

- **ObjectOutputStream.writeObject()**
- **ObjectInputStream.readObject()**

```java
ObjectOutputStream out  = new ObjectOputputStream(new FileOutputStream("worm.out"));
out.writeObject(new Worm(6, 'a')); //将对象自动序列化之后的字节序列写入文件
ObjectInputStream in = new ObjectInputStream(new FileInputStream("worm.out"));
Worm w = (Worm)in.readObject();
```

**注意**：对一个Serializable对象进行还原的时候，是直接从字节序列中还原的，**没有调用任何构造器，包括默认无参构造器**

### 序列化的控制

#### 实现Externalizable接口（继承自Serializable接口，必须要有无参构造器）

新增了两个方法，**会在序列化和反序列化过程自动调用**

- **public** void **writeExternal(ObjectOutput out)** throws IOException
- **public** void **readExternal(OubjectInput in)** throws IOException

**和Serializable区别**：

- **会调用字段定义时初始化（在调用默认构造器之前调用）**
- **调用所有普通默认构造器**
- 没有在writeExternal和readExternal保存恢复的域就会用**默认构造器里的初始化值**或**字段初始化定义值（如果默认构造器里没有初始化对应字段值）**

#### transient关键字（用于Serializable对象）

表示此字段不需要被序列化时保存，也不会在反序列化时被尝试恢复（**注意：仅对于自动序列化机制**）

**但是如果在添加的readObject方法和writeObject方法中显示保存和恢复transient字段是可以的**

**注意：**也可以继承Externalizable接口，那么没有东西可以自动序列化

**static字段也不能被序列化**

#### Externalizable的替代实现（但并不会像其一样调用默认构造器）

在Serializable接口的实现类中**添加** （并不是覆盖或实现）

- **private** void **writeObject(ObjectOutputStream stream)** throws IOException
- **private** void **readObject(ObjectInputStream stream)** throws IOException

注意这里和ObjectOutputStream，和ObjectInputStream的方法同名了，这里其实是一个**混乱的设计**，在序列化的过程中会**反射调用**添加的这两个方法**而不是去使用默认序列化机制**

### 如何正确序列化Class类

Class类是Serializable的，但是想要通过序列化Class对象保存static值，必须手动显示的去writeObject和readObject，不然会有问题

### 常见的序列化协议有哪些

- COM主要用于Windows平台，并没有真正实现跨平台，另外COM的序列化的原理利用了编译器中虚表，使得其学习成本巨大。

- CORBA是早期比较好的实现了跨平台，跨语言的序列化协议。COBRA的主要问题是参与方过多带来的版本过多，版本之间兼容性较差，以及使用复杂晦涩。

- XML & SOAP

  - XML是一种常用的序列化和反序列化协议，具有跨机器，跨语言等优点。
  - SOAP（Simple Object Access protocol） 是一种被广泛应用的，基于XML为序列化和反序列化协议的结构化消息传递协议。SOAP具有安全、可扩展、跨语言、跨平台并支持多种传输层协议。

- JSON（JavaScript Object Notation）

  - 这种Associative array格式非常符合工程师对对象的理解。
  - 它保持了XML的人眼可读（Human-readable）的优点。
  - 相对于XML而言，序列化后的数据更加简洁。
  - 它具备javascript的先天性支持，所以被广泛应用于Web browser的应用常景中，是Ajax的事实标准协议。
  - 与XML相比，其协议比较简单，解析速度比较快。
  - 松散的Associative array使得其具有良好的可扩展性和兼容性。

- Thrift是Facebook开源提供的一个高性能，轻量级RPC服务框架，其产生正是为了满足当前大数据量、分布式、跨语言、跨平台数据通讯的需求。

- Avro的产生解决了JSON的冗长和没有IDL的问题，Avro属于Apache Hadoop的一个子项目。 Avro提供两种序列化格式：JSON格式或者Binary格式。Binary格式在空间开销和解析性能方面可以和Protobuf媲美，JSON格式方便测试阶段的调试。适合于高性能的序列化服务。

### Preferences API（相比对象序列化，它和对象持久性更密切）

**键值对**

用于小的、受限的数据集合（只能存储**基本类型和字符串，每个字符串不超过8K**）

存储用户偏好以及程序配置项

**利用系统资源存储，如Windows里就是注册表**

通常是以类名命名的单一节点

##第二十一章 并发

**并发解决的问题**：

- 速度
- 设计可管理性

多核处理器可以实现真正意义上的并行，但**并发针对的是单核处理器上的程序性能**

**单核处理器的并发**：实际是在切换多个不同任务**线程**，增加了上下文切换的开销

**并发对于单核处理器的意义**：程序存在阻塞（通常是I/O）

**多线程最基本的难题**：保证共享资源（如内存、I/O）的独立访问

**Java中多线程**：在执行程序的单一进程中实现的多线程，这也保证了并发程序可移植性

**Java线程机制**：抢占式，调度机制会周期性的中断线程，将上下文切换到另一个线程

Java对线程数量的限制依赖于Java版本

**协作多线程**：每个线程都自动地放弃控制权，要求编写某种类型让步语句。其优势在于（1.上下文切换开销比抢占式低 2.理论上不限制线程的数量）

### 基本的线程机制

####Runable接口（可以看作是一个独立的任务，实际上Runable这个名字并不恰当）

每个任务都需要附着到一个线程上来执行

**Thread是实现了Runable接口的实体类（都位于java.lang包）**

虽然new Thread().start时并未保存其引用，但它也会开启一个独立的线程执行附着在其上的任务，在其run方法结束前，GC都无法回收该Thread对象

**线程的调度机制是非确定性的**：在不同机器、不同JDk版本上的执行情况都可能不同

####Executor（执行器，java.util.concurrent）

使用执行器，不必显示创建Thread对象

```java
ExecutorService exec = Executors.newCachedThreadPool(); //Executors 创建的ThreadPoolExecutor实例，在线程可用时，重用之前构造好的池中线程
exec.execute(new Runable(){
    @Override
    public void run(){
        System.out.println("Test Executor");
	}
});
exec.shutdown(); //拒绝提交新任务，待已提交任务执行完后尽快退出
```

#### 线程池

**什么是线程池**：  java.util.concurrent.Executors提供了一个 java.util.concurrent.Executor接口的实现用于创建线程池

**什么时候使用线程池**：假设一个服务器完成一项任务所需时间为：T1 创建线程时间，T2 在线程中执行任务的时间，T3 销毁线程时间。如果：T1 + T3 远大于 T2，则可以采用线程池，以提高服务器性能。

**一个线程池包括以下四个基本组成部分**：

- 线程池管理器（ThreadPool）：用于创建并管理线程池，包括 创建线程池，销毁线程池，添加新任务；
- 工作线程（PoolWorker）：线程池中线程，在没有任务时处于等待状态，可以循环的执行任务；
- 任务接口（Task）：每个任务必须实现的接口，以供工作线程调度任务的执行，它主要规定了任务的入口，任务执行完后的收尾工作，任务的执行状态等；
- 任务队列（taskQueue）：用于存放没有处理的任务。提供一种缓冲机制。

**常见线程池（线程池都会自动复用，即先看有无空闲线程可以执行任务，没有再新建线程）**：

- **newSingleThreadExecutor** 适用于保证顺序执行各个任务，且不会有多线程场景

单个工作线程来执行一个**无边界队列**，即线程池中每次只有一个线程工作，单线程串行执行任务。

- **newFixedThreadPool(n)** 适用于可以预测线程数量的业务中

固定数量的线程池，复用 **固定数量的线程** 处理一个 **无边界队列** 。每提交一个任务就使用一个线程，直到达到线程池的最大数量，然后后面进入等待队列直到前面的任务完成才继续执行

- **newCacheThreadPool（会自动销毁空闲线程，但最大线程数是Integer.MAX_VALUE）**

可缓存线程池，**当线程池大小超过了处理任务所需的线程，那么就会回收部分空闲（一般是60秒无执行）的线程**，当有任务来时，会根据需要，在线程可用时，重用之前构造好的池中线程。这个线程池在执行 **大量短生命周期的异步任务时（many short-lived asynchronous task）**，可以显著提高程序性能

- **newScheduleThreadPool**

大小无限制的线程池，支持定时和周期性的执行线程

- **newWorkStealingPool**

创建一个拥有多个任务队列的线程池，通过使用多个队列减少竞争，不传参数，则默认设定为cpu的数量，适用于大耗时的操作，可以并行来执行。

**线程池存在的问题：**FixedThreadPool 和 CachedThreadPool 两者对高负载的应用都不是特别友好。

无边界队列会导致高延迟甚至OOM，长时间运行会导致CachedThreadPool在创建线程上失控，导致OOM

#### 线程池最佳实践

推荐使用 `ThreadPoolExecutor` 手动创建线程池，它提供了很多参数可以进行细粒度的控制。

1. 将任务队列设置成**有边界的队列**

2. 使用合适的 `RejectionHandler` - 自定义的 `RejectionHandler` 或 JDK 提供的默认 handler 。

3. 如果在任务完成前后需要执行某些操作，可以重载

   ```java
    beforeExecute(Thread, Runnable)
    afterExecute(Runnable, Throwable)
   ```

4. 重载 ThreadFactory ，**如果有线程定制化的需求（如设置为后台线程）**

5. 在运行时动态控制线程池的大小（[Dynamic Thread Pool]

####ExecutorService（接口，继承扩展了Executor接口）的各个方法

**submit(Callable<T> task)**：提交一个线程任务，可以接受回调函数的返回值，适用于需要处理返回值或者异常的业务场景

**execute()**：执行一个任务，没有返回值

**shutdown()**：表示不再接受新任务，但**不会强行终止**已经提交或者正在执行中的任务

**shutdownNow()**：对于尚未执行的任务全部取消，**正在执行的任务全部发出interrupt()**，停止执行

#### Callable接口（Java 1.5 concurrent）和Runable接口（Java 1.1 lang）

都代表一个需要被其他线程执行的任务，但Callable接口中只有一个call方法声明，并且使用了**类型参数规定call方法返回值类型**

Callable接口适用需要返回值的任务，并且可以抛出checked exception

运行Callable任务可以拿到一个**Future对象**，表示异步计算的结果。它提供了检查计算是否完成的方法，以等待计算的完成，并检索计算的结果

#### Future接口（concurrent）

提供了三种功能：

　　1）判断任务是否完成；

　　2）能够中断任务；

　　3）能够获取任务执行结果。

```java
Future<?> f = exec.submit(new Callable or Runable);
f.cancel(true);
```

相当于调用了线程的interrupt方法，因为**Executor执行任务无法获得线程引用**，所以可以用Future来中断线程

#### FutureTask（实现了RunableFuture接口，是Future的唯一实现类）

```java
public interface RunnableFuture<V> extends Runnable, Future<V> {
    void run();
}
public class FutureTask<V> implements RunnableFuture<V> {
    /*...*/
}
```

#### 异常不能跨线程传播

对**Thread.sleep(TimeUnit.Seconds.sleep(1))**调用可以抛出InterruptedException，并且必须在run（实现的Runable接口）方法中处理任务内部产生的异常

在创建该线程的main函数里用try catch块无法捕获线程 run() 方法里抛出的Exception

Thread.UncaughtExceptionHandler：可以实现Thread的这个内部接口，并通过

Thread.setDefaultExceptionHandler(YourHandler)，设置该线程的异常处理逻辑为自己的实现

####线程优先级（优先级不导致死锁）

线程调度器倾向于优先执行高优先级线程（但并不是意味着低优先级线程不执行），低优先级线程仅仅是执行频率较低

```java
    Thread.setPriority(Thread.MIN_PRIORITY); // 最低优先级 1，最高 10， 普通 5
```

#### 让步（yield，建议有相同优先级的线程可以运行）

这只是对线程调度器的一个暗示，说明我已经做完一轮迭代要做的工作，现在正式切换时间片的好时机，**但没有任何机制保证它会被采纳**。

#### 后台线程（dameon）

**如果所有非后台线程都结束了，那么所有后台线程会立即终止，finally都不会执行**

```java
Thread.setDameon(true);	//设置成后台线程
Thread.isDameon(); //返回该线程是否为后台线程
```
**后台线程创建的所有线程都是后台线程**

**在构造器中启动线程可能存在的问题**：另一个任务在构造器结束前就启动了，那么这个任务可以访问处于不稳定状态的对象

**在方法内部创建线程**：如果该线程只是辅助操作，那么这比在类的构造器里启动更合适

```java
public void runTask(){
    t = new Thread(){	//匿名内部类继承了Thread类并Override其run方法
        @Override
        public void run(){
            while(true){
                print(this);
            }
        }
    };
    t.start();
}
```

#### 一些术语

Java中，Thread类自身不执行任何操作，它只驱动赋予它的任务（Runable）

Runable更好的理解是把它当成要执行的一个任务

#### join

在一个线程t上调用join()，那么本线程将会被挂起并等待t线程结束(t.isAlive() == false)才恢复

#### 共享受限资源

解决访问共享资源冲突的方式，就是**加锁**，因为锁语句产生了一种互相排斥的效果，所以这也种机制也称为**互斥量**

#### 对象锁（monitor，也称监视器）

- 所有对象都含有**单一的锁**
- 对象的所有synchronized方法共享同一个锁
- **一个任务可以多次获得对象锁**：一个任务调用该对象的synchronized方法，此方法又调用了此对象另一个synchronized方法，那么加锁次数会变成2，只有当加锁次数为0的时候，说明该对象被完全释放

#### 类锁（属于类的Class对象的一部分）

所以**synchronized static**可以在类的范围内防止对static数据的并发访问，即把这些临界的static域设置成private，只能通过synchronized static方法访问

#### CAS操作

使用锁时，线程获取锁是一种**悲观锁策略**，即假设每一次执行临界区代码都会产生冲突，所以当前线程获取到锁的时候同时也会**阻塞**其他线程获取该锁。

CAS操作（又称为无锁操作）是一种**乐观锁策略**，它假设所有线程访问共享资源的时候不会出现冲突，既然不会出现冲突自然而然就不会阻塞其他线程的操作。如果出现冲突了怎么办？无锁操作是使用**CAS(compare and swap)**又叫做比较交换来鉴别线程是否出现冲突，**出现冲突就重试当前操作直到没有冲突为止（自旋）**。

CAS(V,O,N)，**V 内存地址存放的实际值；O 预期的值（旧值）；N 更新的新值**

CAS的实现需要硬件指令集的支撑，在JDK1.5后虚拟机才可以使用处理器提供的**CMPXCHG**指令实现。

> Synchronized VS CAS

Synchronized(**未优化前**)最主要的问题是：在存在线程竞争的情况下会出现线程阻塞和唤醒锁带来的性能问题，因为这是一种互斥同步（**阻塞同步**）

CAS操作失败后会进行一定的尝试，而非进行耗时的挂起唤醒的操作，因此也叫做**非阻塞同步**。这是两者主要的区别。

#### CAS存在的问题

**1. ABA问题** 

因为CAS会检查旧值有没有变化，这里存在这样一个有意思的问题。比如一个旧值A变为了成B，然后再变成A，刚好在做CAS时检查发现旧值并没有变化依然为A，但是实际上的确发生了变化。解决方案可以沿袭数据库中常用的乐观锁方式，添加一个版本号可以解决。原来的变化路径A->B->A就变成了1A->2B->3C。java这么优秀的语言，当然在java 1.5后的atomic包中提供了AtomicStampedReference来解决ABA问题，解决思路就是这样的。

**2. 自旋时间过长**

使用CAS时**非阻塞同步**，也就是说不会将线程挂起，会自旋（无非就是一个死循环）进行下一次尝试，如果这里自旋时间过长对性能是很大的消耗。如果JVM能支持处理器提供的pause指令，那么在效率上会有一定的提升。

**3. 只能保证一个共享变量的原子操作**

当对一个共享变量执行操作时CAS能保证其原子性，如果对多个共享变量进行操作,CAS就不能保证其原子性。有一个解决方案是利用对象整合多个共享变量，即一个类中的成员变量就是这几个共享变量。然后将这个对象做CAS操作就可以保证其原子性。atomic中提供了AtomicReference来保证**引用对象**之间的原子性。

### 并发关键字

#### synchronized 关键字（也直接称为同步，JVM提供支持，JVM负责加锁和释放）

**不属于方法特征签名的一部分**

任务访问synchronized关键字代码片段或方法的时候，会检查当前对象的锁是否可获得，如果可以获得锁，那么才会访问此段代码，在执行结束后释放对象锁。

当一个任务持有某个对象锁的时候，其他**访问该对象的任何synchronized代码的线程都会被阻塞**，访问**非synchronized方法不受影响**

synchronized代码块在实际上在**字节码**多了**monitorenter和monitorexit**两条指令，类似**操作系统PV操作**

**synchronized的正确使用**

- 所有共享的数据资源都设置为**private**，只能通过方法访问
- **所有访问临界共享资源的方法都必须被同步**（synchronized）

#### final关键字

final可以修饰**变量，方法和类**，所修饰的内容一旦赋值之后就不会再被改变

**final在多线程中存在的重排序问题**也很容易忽略

####final变量

**final成员变量**

1. **类变量**：必须要在**静态初始化块**中指定初始值或者**声明该类变量时**指定初始值
2. **实例变量**：必要要在**非静态初始化块**，**声明该实例变量**或者在**构造器中**指定初始值

**final局部变量**

> **final基本数据类型 VS final引用数据类型**

基本数据类型保证数据不变

引用类型保证指向地址不变，但指向的对象属性可以改变

> 宏变量

1. 使用final修饰符修饰；
2. 在定义该final变量时就指定了初始值；
3. 该初始值在编译时就能够唯一指定。

#### final方法

1. 父类的final方法是不能够被子类重写的

2. final方法是可以被重载的

#### final类

不能被继承

#### 不变类

- 使用private和final修饰符来修饰该类的成员变量
- 提供带参的构造器用于初始化类的成员变量；
- 仅为该类的成员变量提供getter方法，不提供setter方法，因为**普通方法无法修改fina修饰的成员变量**；
- 如果有必要就重写Object类 的hashCode()和equals()方法，应该保证用equals()判断相同的两个对象其Hashcode值也是相等的。

String的value就是final

```java
/** The value is used for character storage. */
 private final char value[];
```

#### final 多线程

> **写final域重排序规则**

1. JMM禁止编译器把final域的写重排序到构造函数之外；
2. 编译器会在final域写之后，构造函数return之前，插入一个storestore屏障。这个屏障可以禁止处理器把final域的写重排序到构造函数之外。

> **读final域重排序规则**

**在一个线程中，初次读对象引用和初次读该对象包含的final域，JMM会禁止这两个操作的重排序。**实际上，读对象的引用和读该对象的final域存在间接依赖性，一般处理器不会重排序这两个操作。但是有一些处理器会重排序，因此，这条禁止重排序规则就是针对这些处理器而设定的。

> **对final修饰的对象的成员域写操作**

**增加了这样的约束**：在构造函数内对**一个final修饰的对象的成员域的写入，与随后在构造函数之外把这个被构造的对象的引用赋给一个引用变量**，这两个操作是不能被重排序的。

#### final 的实现原理

以X86处理为例，X86不会对写-写重排序，所以**StoreStore屏障可以省略**。由于**不会对有间接依赖性的操作重排序**，所以在X86处理器中，读final域需要的**LoadLoad屏障也会被省略掉**。也就是说，**以X86为例的话，对final域的读/写的内存屏障都会被省略**！具体是否插入还是得看是什么处理器

### volatile关键字解析

#### 内存模型

![212219343783699](https://ws4.sinaimg.cn/large/006tKfTcgy1g0szokh9ghj30l909rgme.jpg)

对应到JMM就是，

**每个线程的工作内存：其所在CPU的Cache**

**缓存不一致性解决办法（硬件层面）**：

- 通过在总线加LOCK#锁的方式
- 通过缓存一致性协议，Intel 的MESI协议，当CPU写数据时，如果发现操作的变量是共享变量，即在其他CPU中也存在该变量的副本，会发出信号通知其他CPU将该变量的缓存行置为无效状态

#### 并发编程的三个概念

**原子性**

原子性：即一个操作或者多个操作 要么全部执行并且执行的过程不会被任何因素打断，要么就都不执行。

**可视性**

当多个线程访问同一个变量时，一个线程修改了这个变量的值，其他线程能够立即看得到修改的值

**有序性**

即程序执行的顺序按照代码的先后顺序执行

**指令重排序**：程序的实际执行顺序和代码的顺序不一定相同，但处理器保证最后程序结果和代码执行结果是一致的（处理器在重排时会考虑指令之间的依赖性）

**指令重排序不会影响单个线程的执行，但是会影响到线程并发执行的正确性**

```java
//线程1:
context = loadContext();   //语句1
inited = true;             //语句2
 
//线程2:
while(!inited ){
  sleep()
}
doSomethingwithconfig(context);
```

线程1中两个指令没有依赖关系，处理器重排，语句2先执行。但线程2中认为初始化已完成！！！

并发程序正确地执行，必须要同时保证**原子性、可见性以及有序性**。只要有一个没有被保证，就有可能会导致程序运行不正确

#### Java内存模型

JVM specification 里定义了一种（Java Memory Model，JMM）），JMM 是抽象化了硬件的内存模型（使用了多级缓存导致出现缓存一致性协议），屏蔽了各个 CPU 和操作系统的差异。

**它定义了什么？**

它定义了程序中变量的访问规则，往大一点说是定义了程序执行的次序

**所有的变量都是存在主存**当中（类似于前面说的物理内存），每个线程都有自己的工作内存（类似于前面的高速缓存）。**线程对变量的所有操作都必须在工作内存中进行，而不能直接对主存进行操作**。并且每个线程不能访问其他线程的工作内存。

**存在主存中的**：包括实例字段，静态字段，和构成数据对象的元素，但**不包括**局部变量和方法参数，因为后者是线程私有的

**它没有规定的东西有？**

JMM并没有限制执行引擎使用处理器的寄存器或者**高速缓存**来提升指令执行速度，也没有限制编译器**对指令进行重排序**，也就是说Java中同样存在**缓存一致性问题**和**指令重排序的问题**

**1.Java中原子性**

在Java中除了long和double之外所有**基本类型**上的“简单操作”都是原子操作

**简单操作**：只有简单的读取、赋值（而且必须是将数字赋值给某个变量，变量之间的相互赋值不是原子操作，因为需要读取再赋值）才是原子操作。

32位JVM读写64位的long和double时会产生**字撕裂**，会当成两个分离的32位操作

但如果**使用volatile关键字修饰long或者double**，就会获得简单赋值与返回操作的原子性

**Java保证原子性的手段**：

**synchronized和Lock**能够保证任一时刻只有一个线程执行该代码块，那么自然就**不存在原子性问题了**，从而保证了原子性

**CAS**（compare and swap），位于java.util.concurrent.atomic原子操作类，如AtomicInteger，利用处理器提供的CMPXCHG指令实现的，而处理器执行CMPXCHG指令是一个原子性操作

**2.Java中可见性**

**Java保证可见性的手段**：volatile关键字、synchronized和Lock

**volatile关键字**：被修改的值会立即被更新到主存，并且使其他CPU的缓存行无效

**synchronized和Lock**：保证同一时刻只有一个线程获取锁执行同步代码，并且在**释放锁之前会把修改变量刷新到主存！！！**

**3.Java中的有序性**

JMM具备一些“先天的”有序性，即不需要任何手段就可以获得的，也称为 happens-before 原则

**如果两个操作次序无法从happens-before原则推断出来，那么虚拟机就可以随意重排**

**happens-before 原则**：

- 传递规则：如果操作1在操作2前面，而操作2在操作3前面，则操作1肯定会在操作3前发生。该规则说明了happens-before原则具有传递性
- 锁定规则：一个unlock操作肯定会在后面对同一个锁的lock操作前发生。这个很好理解，锁只有被释放了才会被再次获取
- **volatile变量规则**：对一个被volatile修饰的**写操作先发生于后面对该变量的读操作**
- 程序次序规则：一个线程内，按照代码顺序执行（但是注意，**这只保证了单线程的有序性**）
- 线程启动规则：Thread对象的start()方法先发生于此线程的其它动作
- 线程终结原则：线程中其它的所有操作先于线程的终止检测（isAlive() == false or join()）
- 线程中断规则： 对线程interrupt()方法的调用先发生于对该中断异常的获取（isInterrupted()）
- 对象终结规则：一个对象构造先于它的finalize发生

**Java保证有序性的手段（除了happens-before）**：volatile关键字、synchronized和Lock

**synchronized和Lock**：很显然相当于是让一个线程顺序执行同步代码，保证了有序性（相当于利用了happens before里对单线程提供的程序次序原则）

#### volatile（保证可见性，无法保证原子性，一定程度保证有序性）

- 保证了不同线程对这个变量进行操作时的**可见性**
- **禁止进行指令重排序**

**volatile保证可见性：**

1. 使用volatile关键字会强制将修改的值立即写入主存
2. 如果是写操作，它会导致其他CPU中对应的缓存行无效
3. 由于缓存行无效，所以该线程再次读取变量的值时会去主存读取。

**volatile禁止指令重排：**

volatile关键字时，汇编代码里会多出一个**lock前缀指令（CPU指令）**

lock前缀指令实际上相当于一个**内存屏障（也称内存栅栏）**，内存屏障会提供3个功能：

　　1）它确保指令重排序时不会把其后面的指令排到内存屏障之前的位置，也不会把前面的指令排到内存屏障的后面；即在执行到内存屏障这句指令时，在它前面的操作已经全部完成；

**但是栅栏前后部分语句之间的顺序不保证**

　　2）它会强制将对缓存的修改操作立即写入主存（属于保证可见性）

　　3）如果是写操作，它会导致其他CPU中对应的缓存行无效（属于保证可见性）

**volatile使用条件**：

　1）对变量的写操作不依赖于当前值

　2）该变量没有包含在具有其他变量的不变式中

### Lock体系

显示的Lock（也被直接称为加锁，锁，JDK提供支持，必须在编码时注意维护锁的释放）

#### concurrent包结构

![image-20190309160707670](https://ws2.sinaimg.cn/large/006tKfTcgy1g0wlv5htynj30zw0kgjwr.jpg)

#### Lock简介

**优点**：如果抛出了异常，有机会去做清理工作，并且提供了更多的功能

**正确使用方式**：对Lock.lock()的调用后面紧跟**try-finally**，finally块中Lock.release()，确保任何情况下都能释放锁

```java
Lock lock = new ReentrantLock();
public int next(){
    lock.lock();
    try{
        //what you are going to do
    }finally{
        lock.unlock();
    }
}
```

####ReentrantLock（Lock接口的唯一实现）

**基本上所有的方法的实现实际上都是调用了其`抽象静态内部类Sync（lock()方法抽象）`中的方法，而Sync类继承了`AbstractQueuedSynchronizer（AQS）`**

- 具有重入性 关键方法 `ReentrantLock$Sync.nonfairTryAcquire(int acquires)`
- 在获取ReentrantLock上阻塞的任务**可以被中断**（Lock.lockInterruptibly()可中断加锁方式）
- 同时支持公平（嵌套类FairSync继承自Sync）与非公平锁（嵌套类NonfairSync继承自Sync）
- 允许tryLock()，尝试获取锁失败不阻塞，可以继续做后序工作

#### 重入性

**synchronized隐式支持重入性**

表示能够对共享资源能够重复加锁，即当前线程获取该锁再次获取不会被阻塞。

#### 公平锁与非公平锁

是对于获取锁而言的

**公平锁**（**核心方法`hasQueuedPredecessors`**，判断了当前节点在AQS的同步队列中是否有前驱节点）

- 锁的获取顺序就应该符合请求上的绝对时间顺序，**满足FIFO**
- 保证时间上的绝对顺序，需要频繁的上下文切换

**非公平锁**

- 可能刚释放锁的线程下次继续获取该锁，**造成“饿死”现象**
- 非公平锁会降低一定的上下文切换，**降低性能开销，保证了系统更大的吞吐量**

#### AbstractQueuedSynchronizer（抽象模板类，AQS，简称同步器）

AbstractQueuedLongSynchronizer 类提供相同的功能但扩展了对同步状态的 64 位的支持。两者都扩展了类 

**AbstractOwnableSynchronizer**（一个帮助记录当前保持独占同步的线程的简单类）.

AQS是构造同步组件的**基础框架**，有一个int成员变量state表示同步状态，一个**FIFO队列**构成等待队列。

**AQS已经实现的功能**：

- 同步状态的管理（**getState,setState以及compareAndSetState**）
- 对阻塞线程进行排队
- 等待通知

**AQS提供的模板方法**：

**独占锁**

`void acquire(int arg)`：独占式获取同步状态，如果获取失败则插入同步队列进行等待； 

`void acquireInterruptibly(int arg)`：与acquire方法相同，但在同步队列中进行等待的时候可以检测中断；

`boolean tryAcquireNanos(int arg, long nanosTimeout)`：在`acquireInterruptibly`基础上增加了超时等待功能，在超时时间内没有获得同步状态返回false;

`boolean release(int arg)`：释放同步状态，该方法会唤醒在同步队列中的下一个节点

**共享锁（带Shared后缀的方法）**

`void acquireShared(int arg)`：共享式获取同步状态，与独占式的区别在于同一时刻有多个线程获取同步状态；

`void acquireSharedInterruptibly(int arg)`：在acquireShared方法基础上增加了能响应中断的功能；

`boolean tryAcquireSharedNanos(int arg, long nanosTimeout)`：在acquireSharedInterruptibly基础上增加了超时等待的功能；

`boolean releaseShared(int arg)`：共享式释放同步状态

**AQS需要被继承用来实现具体同步语义的方法：**

具有独占锁功能的子类：它必须实现`tryAcquire`、`tryRelease`、`isHeldExclusively`等；

共享锁功能的子类：必须实现`tryAcquireShared`和`tryReleaseShared`等方法

带**Shared后缀**的方法都是支持共享锁加锁的语义。Semaphore、ReentrantReadWriteLock是**共享锁**，ReentrantLock是**独占锁**。

**AQS中的同步队列（存放请求共享资源而阻塞的任务，FIFO）**

1. 节点的数据结构是什么样的？
2. 是单向还是双向？
3. 是带头结点的还是不带头节点的？

**实现**：**链式结构的双向队列**（通过AQS的static final内部类Node实现）

AQS通过成员变量head:Node，tail:Node（**队列头尾指针，有头节点的队列**）来管理

![image-20190309210736802](https://ws1.sinaimg.cn/large/006tKfTcgy1g0wujqx9coj30ya0dygof.jpg)

**1.acquire方法**

- 当线程获取独占式锁失败后就会将当前线程加入同步队列，那么加入队列的方式是怎样的？
- 在同步队列中的节点（线程）会做什么事情了来保证自己能够有机会获得独占式锁了？

**获取锁失败：入队列**，**尾插法**`addWaiter(Node mode)`，**如果tail为null**，调用`endq(node)`，如果是第一个节点`compareAndSetHead(new Node())`，否则自旋不断尝试CAS `compareAndSetTail`尾插入节点直至成功为止

**在同步队列中竞争锁**：排队获取锁`acquireQueued()`方法，acquireQueued()在自旋过程中主要完成了两件事情：

1. **如果当前节点的前驱节点是头节点，并且能够获得同步状态的话，当前线程能够获得锁该方法执行结束退出**；
2. **获取锁失败的话，先将节点状态由INITIAL设置成SIGNAL，然后调用`LookSupport.park`方法使得当前线程阻塞**。

 ![image-20190310101411141](https://ws3.sinaimg.cn/large/006tKfTcgy1g0xha6e8aqj30vk0u01c2.jpg)

**2.release方法**

释放锁：关键方法**唤醒后继节点 `unparkSuccessor(Node node)`**，**每一次锁释放后就会唤醒队列中该节点的后继节点所引用的线程，从而进一步可以佐证获得锁的过程是一个FIFO（先进先出）的过程。**

**独占锁获取和释放总结**：

- 线程获取锁失败，线程被封装成`Node`进行入队操作，核心方法在于`addWaiter()`和`enq()`，同时`enq()`完成对同步队列的头结点初始化工作以及CAS操作失败的重试;
- 线程获取锁是一个自旋的过程，**当且仅当 当前节点的前驱节点是头结点并且成功获得同步状态时，节点出队**即该节点引用的线程获得锁，否则，当不满足条件时就会调用**`LockSupport.park()`**方法使得线程阻塞
- 释放锁的时候会唤醒后继节点**FIFO**

**推荐使用**：使用AQS构造同步组件，用同步组件类的一个**静态内部类继承AQS**，AQS的**子类必须重写AQS的几**

**个protected修饰的用来改变同步状态的方法**

**其模版方法设计模式**：

将**一些方法开放给子类进行重写，而同步器给同步组件所提供模板方法又会重新调用被子类所重写的方法**

```java
//AQS中需要重写的方法
protected boolean tryAcquire(int arg) {
        throw new UnsupportedOperationException();
}
//而AQS中的模板方法acquire()，这里面定义了调用逻辑:
 public final void acquire(int arg) {
        if (!tryAcquire(arg) &&
            acquireQueued(addWaiter(Node.EXCLUSIVE), arg))
            selfInterrupt();
 }
```

ReentrantLock的内部类NonfairSync（继承自内部类Sync，Sync继承自AQS）会重写该方法为：

```java
protected final boolean tryAcquire(int acquires) {
    return nonfairTryAcquire(acquires);
}
```

AQS中模版方法acquire是**供子类同步组件调用的**，而其中又调用了**专用于子类重写的tryAcquire方法**，这样实际

调用的实现就是子类重写过后的方法，但是**整体的调用的逻辑又是在AQS中就写好的模板**

1. 同步组件（这里不仅仅值锁，还包括CountDownLatch等）的实现依赖于同步器AQS，在同步组件实现中，使用**AQS的方式被推荐定义继承AQS的静态内部类**；
2. AQS采用模板方法进行设计，AQS的protected修饰的方法需要由继承AQS的子类进行重写实现，当调用AQS的子类的方法时就会调用被重写的方法；
3. AQS负责同步状态的管理，线程的排队，等待和唤醒这些底层操作，而Lock等同步组件主要专注于**实现同步语义**；
4. 在重写AQS的方式时，使用AQS提供的`getState(),setState(),compareAndSetState()`方法进行修改同步状态

#### Lock（同步组件）和同步器(AQS)的关系

**锁是面向使用者**，它定义了使用者与锁交互的接口，隐藏了实现细节；

**同步器是面向锁的实现者**，它简化了锁的实现方式，屏蔽了同步状态的管理，线程的排队，等待和唤醒等底层操作。

总的来说，同步组件通过重写AQS的方法**实现自己想要表达的同步语义**，而AQS**只需要同步组件表达的true和false即可**，AQS会针对true和false不同的情况做不同的处理

#### ReadWriteLock（接口）

只有两个方法，目的是为了把文件的读写分开加锁，**为了支持多线程同时读**

- Lock readLock()，获取读文件锁
- Lock writeLock()，获取写文件锁

#### ReentrantReadWriteLock（共享锁，ReadWriteLock唯一实现）

1. 读写锁是怎样实现分别记录读写状态的？
2. 写锁是怎样获取和释放的？
3. 读锁是怎样获取和释放的？

提供了很多丰富的方法，最主要的有两个方法：Lock readLock()和Lock writeLock()用来获取读锁和写锁

内部其实包含了**读锁**和**写锁**

**静态内部类`WriteLock`写锁（独占锁）**

获取：重写AQS的**`tryAcquire`**方法来实现其语义

其中有个关键方法，**`exclusiveCount()`**

释放：重写AQS的**`tryRelease`**方法

**同步状态的低16位用来表示写锁的获取次数**

**静态内部类`ReadLock`读锁（共享锁）**

重写`tryAcquireShared`方法和`tryReleaseShared`方法

**锁降级**

**遵循按照获取写锁，获取读锁再释放写锁的次序，写锁能够降级成为读锁**

`processCachedData()`方法，但是在`ReentrantReadWriteLock`中是被注释的

**同步状态的高16位用来表示读锁被获取的次数**

- 已经有线程在写时，申请**读/写锁都会被阻塞**
- 已经有线程在读时，申请写锁会被阻塞
- 已经有线程在读时，申请**读锁不阻塞**

#### Lock和synchronized的选择

- Lock是一个接口（JDK），而synchronized是Java中的关键字（JVM）
- synchronized在发生异常时，会自动释放线程占有的锁，Lock在发生异常时不会自动释放，所以需要finally块
- Lock可以让等待锁而被阻塞的线程响应中断，而synchronized却不行
- Lock**相应方法返回值可以知道有没有成功获取锁**，而synchronized却无法办到
- Lock可以提高多个线程进行读操作的效率

#### 线程本地存储ThreadLocal（java.lang.ThreadLocal）

和线程同步没关系，其实是线程间数据隔离了

**Thread对象中都有一个成员变量threadLocals：ThreadLocalMap对象**

 <ThreadLocal.threadLocalHashCode，本地线程变量值>K-V对

**注意**：ThreadLocalMap是属于Thread的，但里面的key是**ThreadLocal**.threadLocalHashCode

**每一个ThreadLocal对象**都包含了一个独一无二的**threadLocalHashCode值**

**适用场景**：

- ThreadLocal 适用于变量**在线程间隔离且在方法间共享的场景**（解决 数据库连接、Session管理等）

### 终结任务

#### 线程状态

- 新建（new）：已经被分配了必须的系统资源，并执行了初始化，有资格获得CPU时间。这个状态很短暂，调度器会把这个线程转变成就绪状态或者阻塞状态
- 就绪（Runable）：只要分配CPU时间片，就可以运行。**不同于死亡和阻塞状态**
- 阻塞（Blocked）：线程可以运行，但被某个条件阻止，此状态不会分配CPU时间，知道线程重新进入就绪状态才能执行操作
- 死亡（dead）：不可再调度，通常的死亡方式是从run()方法返回，但是**任务的线程还可以被中断！！！**

#### 线程阻塞的5种情况

- sleep(miliseconds)，不会**释放锁**
- wait()，**释放锁**，直到得到notify()或notifyAll()（或者是Java 5加入的singal() signalAll()）
- join，**释放锁**，使调用此方法的线程wait()，直到调用此方法的线程对象所在的线程执行完毕后被唤醒。
- 任务在等待某个输入/输出（I/O）完成（**无法中断（nio除外）**，**但可以通过close Stream结束任务**）
- 任务调用某个对象的synchronized方法，但是对象锁不可用（**无法中断，但获取ReentrantLock阻塞可以中断**）

#### 中断（Thread.interrupt()）

两种情况线程终止的情况

​    （1）线程**处于阻塞状态**，如使用了sleep方法。 （但是如果线程不在阻塞，那么这个调用无效，**但会使中断标志位为true**）

​    （2）线程**非阻塞状态**使用while（！isInterrupted（））{……}来判断线程是否被中断。 

第一种必须要在**部分阻塞状态下**才能成功终止线程，并抛出**InterruptedException，并且置中断标志为false**

第二种是在**非阻塞状态**调用interrupt后会置中断标志位为true

#### 如何正确终止线程

1. **使用退出标志**，使线程正常退出，也就是当 run 方法完成后线程终止
```java
public class MyThread implements Runnable {
    private volatile boolean isCancelled;	//要用volatile保证其他线程对标志的修改能立即可见
    public void run() {
        while (!isCancelled) {
            //do something
        }
    }
    public void cancel() { isCancelled=true; }
}
```

2. **使用 interrupt 方法中断线程**（用于**线程会阻塞**的情况）

- **调用中断：void interrupt()**，如果线程处于被阻塞状态（例如处于 **sleep, wait, join** 等状态），那么线程将立即退出被阻塞状态，并抛出一个 **InterruptedException** 异常，同时会将**中断状态置为false**

如果线程处于正常活动状态，那么会将该线程的中断标志设置为 true。被设置中断标志的线程将继续正常运行

- **查询中断标志：static boolean interrupted()**，测试当前线程（正在执行这一命令的线程）是否被中断。这一调用会将当前线程的**中断状态重置为 false**！！！

- **查询中断标志：boolean isInterrupted()**，测试线程是否被终止。不像静态的中断方法，这一调用**不改变线程的中断状态**

也就是说，<u>interrupt()不能真的终止线程，需要线程自身的配合响应中断！！！</u>

使用**静态查询中断标志方法响应中断（静态方法会清除中断状态位）**

<u>什么时候如此使用？</u>是为了不结束线程，**响应中断后还能够继续执行接下来的任务**，所以清除中断状态

```java
Thread thread = new Thread(() -> {
    while (!Thread.interrupted()) {	
        // do more work
    }
    // return or throw InterruptedException
});
```

**在阻塞方法中正确响应中断，阻塞方法中的中断会清除中断状态！！！**

比较好的做法就是**在catch块中恢复中断状态**

```java
public void run() {
            while (!Thread.currentThread().isInterrupted()) {//这里调用的是非静态查询中断状态方法
                try {
                    System.out.println("test");
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    System.out.println("interrupt");
                    // 抛出InterruptedException后中断标志被清除，标准做法是再次调用interrupt恢复中断
                    Thread.currentThread().interrupt();//恢复中断状态，让其他线程了解此线程被中断过
                }
            }
            System.out.println("stop");
        }
```

### 线程间协作（要协作肯定就要释放锁，等待/通知 机制）

####Object类里提供的 等待/通知 机制（和对象锁monitor配合实现，JVM级别）

**忙等待：**不释放锁，一直执行空循环

wait()，notify()，notifyAll()，都是**！！！Object里的native方法！！！**，只能在**同步块里调用**（因为要操作锁）

**wait()**

**释放锁**，可以接受时间参数，也可以无参（一直等待）

**正确使用方法：**

```java
while(感兴趣的条件满足 == false){
    wait();
}
```

这样做是避免wait被唤醒时，等待的条件（或资源）突然不满足了（如被其他线程占有了），这时此线程应该继续回到wait()中

**错失的信号**

```java
T1:
synchronized (shareMonitor){
    //setup condition for T2
    sharedMonitor.notify();
}
T2:
while(someCondition == false){
    //Ponit 1
    synchronized (ssharedMonitor){
    	sharedMonitor.wait();
	}
}
```

T1执行到Point1时，someCondition并未满足，所以T1准备wait()，但此时发生了线程调度，切换到了T2，T2设置好someCondition后发出了notify()，但切换到T1时，T1由于已经判断过了someCondition，所以会错误的进行wait()，导致永远无法收到T2发出的notify()，**产生死锁**。

那么要求就是：**wait()感兴趣条件的判断必须也放在同步块里**

**notify和notifyAll到底唤醒了什么？**

由于都只能在同步块中使用，所以notify和notifyAll**唤醒的是等待此同步块对应的锁的任务**

#### Lock体系下提供的 等待/通知 机制（和Lock配合实现，JDK级别）

**Condition（接口，具体实现在AQS中的内部类`ConditionObject`）简介**

1. Condition能够支持**不响应中断`condition.awaitUninterruptibly()`！！**，而通过使用Object方式不支持；
2. Condition能够支持**多个等待队列**（new 多个Condition对象），而Object方式只能支持一个；
3. Condition能够支持**超时时间的设置**，而Object不支持

参照Object的wait和notify/notifyAll方法，Condition也提供了同样的方法：

> **针对Object的wait方法**

1. `void await() throws InterruptedException`:当前线程进入等待状态，如果其他线程调用condition的signal或者signalAll方法并且当前线程获取Lock从await方法返回，如果在等待状态中被中断会抛出被中断异常；
2. `long awaitNanos(long nanosTimeout)`：当前线程进入等待状态直到被通知，中断或者**超时**；
3. `boolean await(long time, TimeUnit unit)throws InterruptedException`：同第二种，支持自定义时间单位
4. `boolean awaitUntil(Date deadline) throws InterruptedException`：当前线程进入等待状态直到被通知，中断或者**到了某个时间**

> **针对Object的notify/notifyAll方法**

1. `void signal()`：唤醒一个等待在condition上的线程，将该线程从**等待队列**中转移到**同步队列**中，如果**在同步队列中能够竞争到Lock**则可以从等待方法中返回。
2. `void signalAll()`：与1的区别在于能够唤醒所有等待在condition上的线程

 #### Condition等待队列

AQS的内部类`ConditionObject`是Condition的实现，其**维护等待队列的做法和AQS维护同步队列**相似，还复

用了AQS的`Node`来构造**单向等待队列（无头节点）！！！，不同于同步队列**	

可以多次调用lock.newCondition()方法创建多个condition对象，**一个lock可以持有多个等待队列**

**对象Object对象监视器（monitor）上只能拥有一个同步队列和一个等待队列，而并发包中的Lock拥有一个同步队列和多个等待队列**。

![image-20190309210136916](https://ws1.sinaimg.cn/large/006tKfTcgy1g0wudjnmd9j310m0kmqcr.jpg)

#### await实现原理

```java
public final void await() throws InterruptedException {
    if (Thread.interrupted())
        throw new InterruptedException();
	// 1. 将当前线程包装成Node，尾插入到等待队列中
    Node node = addConditionWaiter();
	// 2. 释放当前线程所占用的lock，在释放的过程中会唤醒同步队列中的下一个节点
    int savedState = fullyRelease(node);
    int interruptMode = 0;
    while (!isOnSyncQueue(node)) {//判断是否被移到了同步队列中（signal or signalAll），是则退出循环
		// 3. 当前线程进入到等待状态
        LockSupport.park(this);
        if ((interruptMode = checkInterruptWhileWaiting(node)) != 0)
            break;	//如果被中断则退出循环
    }
	// 4. 自旋等待获取到同步状态（即获取到lock），获取到lock后才能退出await方法
    if (acquireQueued(node, savedState) && interruptMode != THROW_IE)
        interruptMode = REINTERRUPT;
    if (node.nextWaiter != null) // clean up if cancelled
        unlinkCancelledWaiters();
	// 5. 处理被中断的情况
    if (interruptMode != 0)
        reportInterruptAfterWait(interruptMode);
}
```

1. 是怎样将当前线程添加到等待队列中去的？
2. 释放锁的过程？
3. 怎样才能从await方法退出？

 `addConditionWaiter()` 尾插法进入等待队列（**同步队列头节点**->**等待队列**）

通过`fullRelease()`调用AQS的模板方法`release`（而模版方法调用的`tryRelease`就是由new 这个ConditionObject的Lock实现的）**释放锁**，**并且唤醒在同步队列中头节点的后继节点**

####从await中退出

**1.前提条件（满足以下两种情况中一种）**

- 当前线程被**中断**
- 调用condition.signal/condition.signalAll（**等待队列**->**同步队列**）

**2.关键步骤**

**同步队列中竞争锁**`acquireQueued(node, savedState)`，**直至成功（线程获取到lock）**这里和<u>AQS中的队列中竞争锁是一个用法</u>。

**3.成功退出await的标志**

已经竞争到了condition引用（关联）的lock

下图是await方法的调用过程，**调用await的线程必须是获得了lock的线程，也就是同步队列头节点**

![image-20190309212226684](https://ws2.sinaimg.cn/large/006tKfTcgy1g0wuz6ikrvj30yw0nitlj.jpg)

#### signal/signalAll实现原理

**调用condition的signal或者signalAll方法可以将等待队列中 `等待时间最长` 的节点移动到同步队列中**

**等待队列（FIFO）**：头节点必定是等待时间最长的

```java
public final void signal() {
    //1. 先检测当前线程是否已经获取lock
    if (!isHeldExclusively())
        throw new IllegalMonitorStateException();
    //2. 获取等待队列中第一个节点，之后的操作都是针对这个节点
	Node first = firstWaiter;
    if (first != null)
        doSignal(first);
}
private void doSignal(Node first) {
    do {
        if ( (firstWaiter = first.nextWaiter) == null)
            lastWaiter = null;
		//1. 将头结点从等待队列中移除
        first.nextWaiter = null;
		//2. while中transferForSignal方法对头结点做真正的处理
    } while (!transferForSignal(first) &&
             (first = firstWaiter) != null);
}
final boolean transferForSignal(Node node) {
    /*
     * If cannot change waitStatus, the node has been cancelled.
     */
	//1. 更新状态为0
    if (!compareAndSetWaitStatus(node, Node.CONDITION, 0))
        return false;
    /*
     * Splice onto queue and try to set waitStatus of predecessor to
     * indicate that thread is (probably) waiting. If cancelled or
     * attempt to set waitStatus fails, wake up to resync (in which
     * case the waitStatus can be transiently and harmlessly wrong).
     */
	//2.将该节点移入到同步队列中去
    Node p = enq(node);
    int ws = p.waitStatus;
    if (ws > 0 || !compareAndSetWaitStatus(p, ws, Node.SIGNAL))	//node状态变为signal
        LockSupport.unpark(node.thread);
    return true;
}
```

**signal调用总结**

**调用signal的线程必须是获取了lock 的线程**

**调用效果**：等待队列头节点->尾插入同步队列**`enq()`**（这样才await的线程才能从**`LockSupport.park(this)`**返回，才能调用**`acquireQueued()`**去竞争锁）

![image-20190310123118798](https://ws4.sinaimg.cn/large/006tKfTcgy1g0xl8us9yvj310k0laams.jpg)

> **signalAll**

```java
private void doSignalAll(Node first) {
    lastWaiter = firstWaiter = null;
    do {
        Node next = first.nextWaiter;
        first.nextWaiter = null;
        transferForSignal(first);
        first = next;
    } while (first != null);
}
```

**等待队列所有节点都移入到同步队列中**，即“通知”当前调用condition.await()方法的每一个线程。

#### await与signal/signalAll的结合思考

![image-20190310124511844](https://ws2.sinaimg.cn/large/006tKfTcgy1g0xlnb4jntj310e0j6te5.jpg)

如图，**线程awaitThread先通过lock.lock()方法获取锁成功后调用了condition.await方法进入等待队列，而另一个线程signalThread通过lock.lock()方法获取锁成功后调用了condition.signal或者signalAll方法，使得线程awaitThread能够有机会移入到同步队列中，当其他线程释放lock后使得线程awaitThread能够有机会获取lock，从而使得线程awaitThread能够从await方法中退出执行后续操作。如果awaitThread获取lock失败会直接进入到同步队列**。

#### await和signal比较

**相同点**

调用await和signal方法的线程必须都是**同步队列的头节点，因为必须是拥有锁的**

**区别**

- await是**对调用者线程起作用**，将当前线程**尾插入等待队列**，**释放锁**，并等待singal或者中断
- singal是对**等待队列的线程起作用**，**不释放当前线程锁**，将等待队列头节点尾插入同步队列，给其一个竞争锁的机会

#### LockSupport

LockSupprot是线程的阻塞**原语**，用来阻塞线程和唤醒线程。

AQS的底层都是基于LockSupport实现，LockSupport**不可重入**

> **阻塞线程**

1. `void park()`：阻塞当前线程，如果调用unpark方法或者当前线程被中断，从能从park()方法中返回
2. `void park(Object blocker`)：功能同方法1，入参增加一个Object对象，用来记录导致线程阻塞的阻塞对象，方便进行问题排查；
3. `void parkNanos(long nanos)`：阻塞当前线程，最长不超过nanos纳秒，增加了超时返回的特性；
4. `void parkNanos(Object blocker, long nanos)`：功能同方法3，入参增加一个Object对象，用来记录导致线程阻塞的阻塞对象，方便进行问题排查；
5. `void parkUntil(long deadline)`：阻塞当前线程，直到deadline；
6. `void parkUntil(Object blocker, long deadline)`：功能同方法5，入参增加一个Object对象，用来记录导致线程阻塞的阻塞对象，方便进行问题排查；

> **唤醒线程**

void unpark(Thread thread):唤醒处于阻塞状态的指定线程

实际上LockSupport阻塞和唤醒线程的功能是依赖于sun.misc.Unsafe，这是一个很底层的类，直接修改内存，所以叫Unsafe，比如park()方法的功能实现则是靠unsafe.park()方法。

**synchronzed致使线程阻塞，线程会进入到BLOCKED状态，而调用LockSupprt方法阻塞线程会致使线程进入到WAITING状态。**

```java
public class LockSupportDemo {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {
            LockSupport.park();
            System.out.println(Thread.currentThread().getName() + "被唤醒");
        });
        thread.start();
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        LockSupport.unpark(thread);
    }
}
```

### 并发容器

#### ConcurrentHashMap

 JDK 1.6版本关键要素：

1. segment继承了ReentrantLock充当锁的角色，为每一个segment提供了线程安全的保障；
2. segment维护了哈希散列表的若干个桶，每个桶由HashEntry构成的链表。

JDK 1.8的ConcurrentHashMap就有了很大的变化

1. 舍弃了segment，并且大量使用了synchronized，以及CAS无锁操作以保证ConcurrentHashMap操作的线程安全性
2. synchronzied做了很多的优化，包括偏向锁，轻量级锁，重量级锁，可以依次向上升级锁状态，但不能降级
3. 底层数据结构改变为采用数组+链表+红黑树的数据形式。

> **ConcurrentHashMap的关键属性**

**table** volatile Node<K,V>[] table://装载Node的数组，作为ConcurrentHashMap的数据容器，采用懒加载的方式，直到第一次插入数据的时候才会进行初始化操作，数组的大小总是为2的幂次方。

**nextTable** volatile Node<K,V>[] nextTable; //扩容时使用，平时为null，只有在扩容的时候才为非null

