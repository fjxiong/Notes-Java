# Java SE

## 一、Java概述

### 1.1 Java的发展历史

Java 是一种广泛使用的高级编程语言，自1995年发布以来，经历了多个重要的发展阶段。以下是 Java 的主要发展历史：

**1）起源与诞生（1991-1995）**

* **1991年**：==Java 的前身 Oak== 由 Sun Microsystems 的 ==James Gosling==及其团队开发，最初目的是为嵌入式系统（如家用电器）设计一种跨平台的编程语言。
* ==**1995年**：Oak 更名为 Java，并正式发布。Java 1.0 版本推出==，主打“一次编写，到处运行”（Write Once, Run Anywhere, WORA）的理念，通过 Java 虚拟机（JVM）实现跨平台能力。

**2）早期发展（1996-2000）**

* **1996年**：Java 1.0 发布，包含核心 API 和 JVM。
* **1997年**：Java 1.1 发布，引入了内部类、JDBC（Java 数据库连接）、RMI（远程方法调用）等重要特性。
* **1998年**：Java 1.2 发布，标志着 Java 2 平台的诞生。这一版本引入了 Swing GUI 工具包、集合框架（Collections Framework）和 JIT 编译器（Just-In-Time Compiler）。
* **2000年**：Java 1.3 发布，改进了性能并引入了 HotSpot JVM。

**3）成熟期（2002-2010）**

* **2002年**：Java 1.4 发布，引入了正则表达式、NIO（非阻塞 I/O）、XML 处理等特性。
* ==**2004年**：Java 5（也称为 Java 1.5）发布，是 Java 语言的重要里程碑，从此Java改为大版本号更新。==引入了泛型、注解、枚举、自动装箱/拆箱、可变参数等特性。
* **2006年**：Java 6 发布，改进了性能、脚本语言支持和 JDBC 4.0。
* ==**2010年**：Oracle 收购 Sun Microsystems，Java 的开发和维护由 Oracle 接手。==

**4）现代 Java（2011 年至今）**

* **2011年**：Java 7 发布，引入了 try-with-resources 语句、NIO 2.0、Fork/Join 框架等特性。
* ==**2014年**：Java 8 发布，是 Java 历史上最重要的更新之一。引入了 Lambda 表达式、Stream API、新的日期时间 API（java.time）等。==
* **2017年**：Java 9 发布，引入了模块化系统（Project Jigsaw），允许开发者将应用程序模块化。
* **2018年**：Java 10 和 Java 11 发布。Java 11 是长期支持版本（LTS），引入了新的 HTTP 客户端 API、局部变量类型推断（var）等特性。
* **2020年**：Java 14 和 Java 15 发布，引入了 Records、Pattern Matching 等新特性。
* **2021年**：Java 16 和 Java 17 发布。Java 17 是另一个长期支持版本（LTS），进一步增强了语言特性和性能。
* **2022年**：Java 18 和 Java 19 发布，引入了虚拟线程（预览特性）等新功能。
* **2023年**：Java 20 和 Java 21 发布。Java 21 是 LTS 版本，引入了虚拟线程（正式版）、模式匹配等特性。
* 、、、

**5）未来展望**

* Java 的开发仍在持续进行，Oracle 和 OpenJDK 社区致力于提升性能、简化开发流程，并引入更多现代编程语言的特性。
* Java 在云计算、大数据、人工智能等领域的应用也在不断扩展。

可以看到，Java 的更新一直保持着活跃的状态。在众多的 Java 版本中（包括过渡版本和LTS版本），我们通常选择较新的长期支持版本（LTS）进行学习和使用，新的版本往往会添加一些新的特性来方便开发。当然，我们不用担心新旧版本之间的兼容性问题，Java 的版本更新通常都是向下兼容的，即用旧版本 Java 开发的代码在新版本 Java 的运行环境下依然可以正常运行。

### 1.2 Java的三大平台

Java的用途非常广泛，针对不同的应用场景，Java推出了三个版本，即Java的三大平台：

* **Java SE（Java Platform, Standard Edition）：**Java SE是Java的标准版，是Java技术的核心和基础。它提供了Java语言的核心类库和API，是Java EE和Java ME的基础。

* **Java EE（Java Platform, Enterprise Edition）：**Java EE是Java的企业版，专为大型企业级应用设计。它在Java SE的基础上，提供了更丰富的API和框架，用于开发Web应用、分布式应用和企业级服务。

* **Java ME（Java Platform, Micro Edition）：**Java ME是Java的微型版，专为移动设备和嵌入式设备设计。它提供了适合资源受限设备运行的Java应用程序的开发框架和API，用于开发手机、PDA、电视机顶盒等设备上的应用。随着Android和iOS的发展，Java ME已经被市场淘汰。

### 1.3 Java的跨平台特性

Java具有跨平台、面向对象、安全性、多线程等众多特性，其中，Java的跨平台特性是其最显著的优势之一。Java的跨平台特性指的是“一次编写，到处运行”（Write Once，Run Anywhere，WORA），即假设我们编写了一个Java源程序，在Windows上编译后生成了字节码文件并运行，这个字节码文件在Linux、macOS等不同操作系统上也可以直接运行，而无需重新编译。

跨平台这一特性主要通过**字节码**和**Java虚拟机（JVM）**的机制来实现的：

* **字节码（Bytecode）：**
	Java 源代码（.java 文件）经过编译后生成字节码（.class 文件）。字节码是一种中间代码，与具体的操作系统和硬件无关。JVM 负责将字节码转换为特定平台的机器指令并执行。
* **Java 虚拟机（JVM）：**
	JVM 是 Java 跨平台的基石。它是一个虚拟的计算机，负责解释和执行 Java 字节码。不同操作系统（如 Windows、Linux、macOS）有各自对应的 JVM 实现，但它们都能运行相同的字节码文件（.class 文件）。



## 二、Java程序初体验

下面是一个Java的入门程序，它的功能是向控制台输出"Hello World!"。

```java
// 定义一个公共类，类名为HelloWorld
public class HelloWorld {

    // 定义一个公共的静态方法，名为main，这是程序的入口点
    public static void main(String[] args) {

        // 在控制台输出 "Hello, World!"
        System.out.println("Hello, World!");
    }
}
```

下面是对这段程序的解释：

* `//`开头的文字是Java的注释，它不会被JVM执行。
* `public class HelloWorld {}`定义了一个类，类名为`HelloWorld`，`public` 表示这个类是公共的，可以被其他类访问，`class` 是定义类的关键字，`{}`是类定义的范围。
* `public static void main(String[] args){}`是`main`方法。`main`方法是Java程序的起点，`public` 表示这个方法是公共的，可以被其他类访问，`static` 表示这个方法是静态的，意味着它属于类而不是类的实例，`void` 表示这个方法不返回任何值，`String[] args` 是 `main` 方法的参数，它是一个字符串数组，用于接收命令行参数。
* ` System.out.println("Hello, World!");`是一个用于向控制台输出文本的语句。`System` 是一个内置的类，提供了与系统相关的功能，`out` 是 `System` 类中的一个静态成员，表示标准输出流（`PrintStream`的对象），`println` 是 `PrintStream` 类中的一个方法，用于输出一行文本并在末尾添加换行符，`"Hello, World!"` 是要输出的字符串，`;`是语句的结束符。

如何运行上述代码：

1. 将上述代码保存到一个名为 `HelloWorld.java` 的文件中。
2. 打开命令行或终端，导航到保存文件的目录。
3. 使用 `javac HelloWorld.java` 命令编译代码。这将生成一个名为 `HelloWorld.class` 的字节码文件。
4. 使用 `java HelloWorld` 命令运行程序。你将在控制台看到输出 `Hello, World!`。



## 三、Java基础语法

### 3.1  注释

注释是对代码的解释和说明，注释的内容不会参与编译和运行。Java中的注释分为三种：

* 单行注释：

~~~java
// 这是单行注释文字
~~~

* 多行注释：

~~~java
/*
这是多行注释文字
这是多行注释文字
这是多行注释文字
*/
~~~

* 文档注释：

```java
/**
这是多行注释文字
这是多行注释文字
这是多行注释文字
*/
```

### 3.2  关键字

关键字就是具有特定含义的英文单词，Java的关键字对Java的编译器有特殊的意义，程序在编译运行时根据关键字来决定要做什么事情。

Java中共有五十多个关键字，随着Java版本的更新，这个数字可能还会增加。关键字有各自的用途，有用于说明数据类型的，有用于说明程序结构的，还有用于修饰的等等。下面是Java中的部分关键字列举：

| **abstract**   | **assert**       | **boolean**   | **break**      | **byte**   |
| -------------- | ---------------- | ------------- | -------------- | ---------- |
| **case**       | **catch**        | **char**      | **class**      | **const**  |
| **continue**   | **default**      | **do**        | **double**     | **else**   |
| **enum**       | **extends**      | **final**     | **finally**    | **float**  |
| **for**        | **goto**         | **if**        | **implements** | **import** |
| **instanceof** | **int**          | **interface** | **long**       | **native** |
| **new**        | **package**      | **private**   | **protected**  | **public** |
| **return**     | **strictfp**     | **short**     | **static**     | **super**  |
| **switch**     | **synchronized** | **this**      | **throw**      | **throws** |
| **transient**  | **try**          | **void**      | **volatile**   | **while**  |

### 3.3  字面量

字面量就是直接在代码中表示固定值的符号，即数据在程序中的书写格式。我们在程序中书写的字面量有以下几种类型：

| **字面量类型** | **说明**                                  | **程序中的写法**     |
| -------------- | ----------------------------------------- | -------------------- |
| 整数           | 不带小数的数字                            | 666，-88             |
| 浮点数         | 带小数的数字                              | 13.14，-5.21         |
| 字符           | 必须使用单引号，有且仅能一个字符          | ‘A’，‘0’，   ‘我’    |
| 字符串         | 必须使用双引号，内容可有可无              | “HelloWorld”，“你好” |
| 布尔值         | 布尔值，表示真假，只有两个值：true，false | true 、false         |
| 空值           | 一个特殊的值，空值                        | null                 |

### 3.4  变量和常量

变量就是可以变化的量，可以把它看作是存储数据的容器，其值可以在程序运行期间不断改变。

定义一个变量时，需要指明它的数据类型，可以在定义变量的同时对它进行初始化，也可以在之后使用等号`=`进行赋值：

```java
int age = 22;

double salary;
salary = 10000.0;
```

常量是指在程序运行期间其值不能被改变的量。在Java中，通过`final`关键字来定义常量：

```java
final int MAX_VALUE = 100;
final double PI = 3.14159;
```

注意点：

* 常量在声明时就必须进行初始化，否则会编译错误；

* 常量的值一旦被初始化，就不能再更改；
* 常量的命名通常使用全大写字母，单词之间用下划线分隔（例如：`MAX_VALUE`）；

### 3.5  数据类型

Java的数据类型分为两大类，分别是**基本数据类型**和**引用数据类型**。

**1）基本数据类型：**

基本数据类型直接存储值，而不是对象的引用（内存地址）。基本数据类型分为四类八种：

| 数据类型 | 关键字  | 内存占用 |                 取值范围                  |
| :------: | :-----: | :------: | :---------------------------------------: |
|   整数   |  byte   |    1     |    负的2的7次方 ~ 2的7次方-1(-128~127)    |
|          |  short  |    2     | 负的2的15次方 ~ 2的15次方-1(-32768~32767) |
|          |   int   |    4     |        负的2的31次方 ~ 2的31次方-1        |
|          |  long   |    8     |        负的2的63次方 ~ 2的63次方-1        |
|  浮点数  |  float  |    4     |        1.401298e-45 ~ 3.402823e+38        |
|          | double  |    8     |      4.9000000e-324 ~ 1.797693e+308       |
|   字符   |  char   |    2     |                  0-65535                  |
|   布尔   | boolean |    1     |                true，false                |

> e+38表示是乘以10的38次方，同样，e-45表示乘以10的负45次方。
>
> 在Java中整数默认是int类型，浮点数默认是double类型。

**2）引用数据类型：**

引用数据类型存储的是对象的引用（内存地址），而不是直接存储对象的值。在Java中，类、接口、数组等都是引用数据类型。

### 3.6  标识符

标识符就是我们给类、变量或者方法等起的名字。关于标识符的书写，有一些硬性要求，也有一些软性建议。

**1）硬性要求：**

* 必须由数字、字母、下划线_、美元符号$组成；
* 不能以数字开头；
* 不能是Java的关键字；
* 区分大小写。

**2）软性建议：**

* 标识符要做到见名知意；
* 对于变量名和方法名，采用小驼峰命名法；
* 对于类名，采用大驼峰命名法。

### 3.7  运算符

运算符就是对变量或者字面量进行操作的符号，用运算符把变量或者字面量连接起来，符合Java语法的式子称为表达式，不同的运算符连接的表达式是不同类型的表达式。

例如：对于语句`int c = a + b;`，`+`是运算符，并且是算数运算符，那么`a + b`就是一个算术表达式。

**1）算术运算符：**

算术运算符用于执行基本的数学运算，算术运算符操作的对象是数值类型的，包括整数和浮点数。

| 运算符 | 描述         | 示例              | 结果     |
| :----- | :----------- | :---------------- | :------- |
| `+`    | 加法         | `int a = 5 + 3;`  | `a = 8`  |
| `-`    | 减法         | `int b = 5 - 3;`  | `b = 2`  |
| `*`    | 乘法         | `int c = 5 * 3;`  | `c = 15` |
| `/`    | 除法         | `int d = 10 / 3;` | `d = 3`  |
| `%`    | 取模（取余） | `int f = 10 % 3;` | `f = 1`  |

字符也能进行算术运算，因为字符本质上也是数值类型。

```java
System.out.println('a' + 1); //97 + 1 = 98
System.out.println('A' + 1); //65 + 1 = 66
```

**2）赋值运算符：**

赋值运算符就是用来将某个值赋值给变量。在Java中，有下面几种赋值运算符：

| 运算符 | 描述     | 示例                  | 结果     |
| :----- | :------- | :-------------------- | :------- |
| `=`    | 简单赋值 | `int a = 5;`          | `a = 5`  |
| `+=`   | 加法赋值 | `int a = 5; a += 3;`  | `a = 8`  |
| `-=`   | 减法赋值 | `int a = 5; a -= 3;`  | `a = 2`  |
| `*=`   | 乘法赋值 | `int a = 5; a *= 3;`  | `a = 15` |
| `/=`   | 除法赋值 | `int a = 10; a /= 3;` | `a = 3`  |
| `%=`   | 取模赋值 | `int a = 10; a %= 3;` | `a = 1`  |

**补充：数据类型转换：**

在Java中，不同的数据类型占用的内存空间不同，所以它们的取值范围也不同，对于数值类型，它们之间的取值范围有如下关系：

**byte < short < int < long < float < double**

算术运算符要求参与运算的两个对象是同一类型的，不同类型的对象参与运算需要先进行数据类型的转换。在Java中，存在两种数据类型转换方式，即隐式类型转换（自动类型提升）和强制类型转换。

**隐式类型转换（自动类型提升）：**

隐式类型转换是指编译器自动进行的类型转换，通常发生在将**小范围数据类型赋值给大范围数据类型时**或者**小范围数据类型和大范围数据类型之间进行算术运算时**。这种转换是安全的，因为不会导致数据丢失。

隐式类型转换具有以下规则：

* 小范围数据类型赋值给大范围数据类型时，小的会先提升为大的，再进行赋值；

* 小范围数据类型和大范围数据类型之间进行算术运算时，小的会先提升为大的，再参与运算；
* byte、short、char三种类型的数据在运算的时候，都会先直接提升为int，然后再进行运算。

```java
public class OperatorDemo02 {
    public static void main(String[] args) {
        // 自动类型提升
        int a = 10;
        double b = 10.0;
        // a会先提升为double类型，再相加
        System.out.println(a + b); //20.0

        byte c = 10;
        byte d = 20;
        // c和d都会先提升为int类型，再相加
        System.out.println(c + d); //30
    }
}
```

**强制类型转换：**

强制类型转换是指程序员手动进行的类型转换，通常发生在将**大范围数据类型赋值给小范围数据类型**时。当我们想把一个取值范围大的赋值给取值范围小的，是不被允许的，如果非要这么做，就需要进行强制类型转换。这种转换可能导致数据丢失或精度损失。

```java
public class OperatorDemo03 {
    public static void main(String[] args) {
        double a = 3.14;
        int b = (int) a; //强制类型转换，double转为int，b的值为3（丢失小数部分）

        long c = 1000L;
        int d = (int) c; //long转为int
    }
}
```

如果转换的值超出目标类型的范围，结果可能会溢出。

```java
int a = 300;
byte b = (byte) a;  // 结果为 44，因为 300 超出了 byte 的范围（-128 到 127）
```

**3）自增和自减运算符：**

自增（`++`）和自减（`--`）运算符是 Java 中的单目运算符，用于对变量的值进行加 1 或减 1 操作。它们可以放在变量的前面（前缀形式）或后面（后缀形式），具体行为有所不同。

自增运算符：

```java
int a = 5;
int b = ++a;  // 前缀形式：a 先加 1 变为 6，然后赋值给 b
System.out.println("a: " + a + ", b: " + b);  // 输出：a: 6, b: 6

int c = 5;
int d = c++;  // 后缀形式：c 的当前值 5 赋值给 d，然后 c 加 1 变为 6
System.out.println("c: " + c + ", d: " + d);  // 输出：c: 6, d: 5
```

自减运算符：

```java
int x = 10;
int y = --x;  // 前缀形式：x 先减 1 变为 9，然后赋值给 y
System.out.println("x: " + x + ", y: " + y);  // 输出：x: 9, y: 9

int m = 10;
int n = m--;  // 后缀形式：m 的当前值 10 赋值给 n，然后 m 减 1 变为 9
System.out.println("m: " + m + ", n: " + n);  // 输出：m: 9, n: 10
```

注意事项：

* 自增和自减运算符只能用于变量，不能用于常量或表达式；
* 前缀形式（`++a` 或 `--a`）先改变值后返回；
* 后缀形式（`a++` 或 `a--`）先返回值后改变值。

**4）关系运算符：**

关系运算符用于比较两个操作数之间的关系，结果为布尔值（`true` 或 `false`）。在Java中，关系运算符有以下六种：

| 运算符 | 描述     | 示例                               | 结果        |
| :----- | :------- | :--------------------------------- | :---------- |
| `==`   | 等于     | `int a = 5; boolean b = (a == 3);` | `b = false` |
| `!=`   | 不等于   | `int a = 5; boolean c = (a != 3);` | `c = true`  |
| `>`    | 大于     | `int a = 5; boolean d = (a > 3);`  | `d = true`  |
| `<`    | 小于     | `int a = 5; boolean e = (a < 3);`  | `e = false` |
| `>=`   | 大于等于 | `int a = 5; boolean f = (a >= 3);` | `f = true`  |
| `<=`   | 小于等于 | `int a = 5; boolean g = (a <= 3);` | `g = false` |

**5）逻辑运算符：**

逻辑运算符用于对布尔值进行逻辑操作，这些运算符在条件判断和布尔表达式中非常常用。在Java中，常用的逻辑运算符有以下几种：

| 运算符 | 描述   | 示例                         | 结果        |
| ------ | ------ | ---------------------------- | ----------- |
| `&&`   | 逻辑与 | `boolean a = true && true;`  | `a = true`  |
| `||`   | 逻辑或 | `boolean a = true || false;` | `a = true`  |
| `!`    | 逻辑非 | `boolean a = !true;`         | `a = false` |

逻辑运算符的短路特性：

* 对于`&&`运算符前后的两个表达式，如果第一个表达式的结果为`false`，那么第二个表达式不会被计算，整体直接返回`false`；
* 对于`||`运算符前后的两个表达式，如果第一个表达式的结果为`true`，那么第二个表达式也不会被计算，整体直接返回`true`；

**6）三元运算符：**

在Java中，三元运算符用于根据条件选择两个值中的一个，它是一种简洁的条件判断的语法。

| 运算符                           | 描述                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| `布尔表达式 ? 表达式1 : 表达式2` | 如果布尔表达式的值为true，则返回表达式1的值；否则，返回表达式2的值 |

例如，可以用三元运算符计算两个数中较大的那一个：

```java
int x = 10;
int y = 20;
int max = x > y ? x : y;
System.out.println("最大值是: " + max);
```

### 3.8  流程控制语句

**1）分支结构：**

**1.if**

```java
if (关系表达式) {
    语句体;	
}
```

执行流程：

①首先计算关系表达式的值；

②如果关系表达式的值为true就执行语句体；

③如果关系表达式的值为false就不执行语句体；

④继续执行后面的语句内容。

**2.if...else**

```java
if (关系表达式) {
    语句体1;	
} else {
    语句体2;	
}
```

执行流程：

①首先计算关系表达式的值；

②如果关系表达式的值为true就执行语句体1；

③如果关系表达式的值为false就执行语句体2；

④继续执行后面的语句内容。

**3.if...else if...else**

```java
if (关系表达式1) {
    语句体1;	
} else if (关系表达式2) {
    语句体2;	
} 
…
else {
    语句体n+1;
}
```

执行流程：

①首先计算关系表达式1的值；

②如果值为true就执行语句体1，如果值为false就计算关系表达式2的值；

③如果值为true就执行语句体2，如果值为false就计算关系表达式3的值；

④…；

⑤如果没有任何关系表达式为true，就执行语句体n+1。

**4.switch语句：**

```java
switch (表达式) {
	case 1:
		语句体1;
		break;
	case 2:
		语句体2;
		break;
	...
	default:
		语句体n+1;
		break;
}
```

执行流程：

①首先计算出表达式的值 ;

②其次，将表达式的值和case依次比较，一旦有对应的值，就会执行相应的语句，在执行的过程中，遇到break就会结束；

③最后，如果所有的case都和表达式的值不匹配，就会执行default语句体部分，然后程序结束掉。 

关于switch语句的扩展：

- default可以放在任意位置，也可以省略

- 不写break会引发case穿透现象

- switch在JDK12的新特性：

```java
int number = 10;
switch (number) {
    case 1 -> System.out.println("一");
    case 2 -> System.out.println("二");
    case 3 -> System.out.println("三");
    default -> System.out.println("其他");
}
```

**2）循环结构：**

**1.for循环：**

```java
for (初始化语句;条件判断语句;条件控制语句) {
	循环体语句;
}
```

执行流程：

①执行初始化语句；

②执行条件判断语句，如果是false，循环结束，如果是true，继续执行；

③执行循环体语句；

④执行条件控制语句；

⑤回到②继续。

**2.while循环：**

```java
初始化语句;
while(条件判断语句){
	循环体语句;
	条件控制语句;
}
```

执行流程：

①执行初始化语句；

②执行条件判断语句，如果是false，循环结束，如果是true，继续执行；

③执行循环体语句；

④执行条件控制语句；

⑤回到②继续。

**3.do...while循环：**

```java
初始化语句;
do{
    循环体;
    条件控制语句;
}while(条件判断语句);
```

执行流程：

①执行初始化语句；

②执行循环体语句；

③执行条件控制语句；

④执行条件判断语句，如果是false，循环结束，如果是true，继续执行；

⑤回到②继续。

### 3.9  数组

在Java中，数组是一种用于存储固定数量同类型元素的数据结构。数组中的每个元素可以通过索引访问，索引从0开始。这里有两点需要注意：

* 数组一旦创建，大小就不能再改变；
* 数组只能用于存储同一数据类型的元素。

#### 数组的声明

数组的声明有两种语法格式：

第一种：`数据类型[] 数组名;`（推荐！）

第二种：`数据类型 数组名[];`

```java
// 格式一
int[] arr1;
// 格式二
int arr2[];
```

#### 数组的创建

数组的创建需要使用new关键字，具体的语法格式也有两种：

第一种：`new 数据类型[]{元素1, 元素2, ..., 元素n};`

第二种：`new 数据类型[数组大小];`

第一种方式还有一个简化写法：`{元素1, 元素2, ..., 元素n};`，即省略掉`new 数据类型[]`。

```java
// 方式一
int[] arr1;
arr1 = new int[]{1, 2, 3, 4, 5}; //或者：arr1 = {1, 2, 3, 4, 5}; 
// 方式二
int[] arr2;
arr2 = new int[5];
```

这两种创建数组的方式有各自的应用场景和特点：

* 第一种方式适用于事先知道数组要存储哪些元素；
* 第二种方式适用于不知道数组要存储哪些元素，但知道数组要存储的元素数量；
* 第一种方式创建的数组，元素为指定的元素，大小等于元素的数量；
* 第二种方式创建的数组，元素采用默认值，大小等于指定的大小。

采用方式二创建的数组中元素的默认值如下：

* 整数类型：0
* 小数类型：0.0
* 布尔类型：false
* 字符类型：'\u0000'
* 引用类型：null

#### 数组的初始化

我们可以在声明数组的同时创建数组，这叫数组的初始化。创建数组的两种方式分别对应着数组的静态初始化和动态初始化。

**数组的静态初始化：**

数组的静态初始化指的是我们可以在创建数组的时候指定数组中要存储的元素，创建后的数组的长度就是元素的个数。

```java
// 完整写法
int[] arr1 = new int[]{1, 2, 3, 4, 5};
// 简化写法
int[] arr2 = {1, 2, 3, 4, 5};
```

**数组的动态初始化：**

数组的动态初始化是指我们在创建数组的时候，只指定数组的长度，由虚拟机给出数组中元素的默认值。在之后，根据需要动态地修改数组中元素的值。

```java
int[] arr = new int[3]; // 数组中的元素全为0
```

#### 数组的地址

数组本身是引用数据类型，所以我们打印数组得到的是其在内存中的地址值。

```java
int[] arr1 = {1, 2, 3, 4, 5};
System.out.println(arr1); //[I@776ec8df

double[] arr2 = {1.1, 2.2, 3.3, 4.4, 5.5};
System.out.println(arr2); //[D@4eec7777
```

关于**[I@776ec8df**的解释：

* [ ：表示现在打印的是一个数组。

* I：表示现在打印的数组是int类型的。

* @：仅仅是一个间隔符号而已。

* 776ec8df：数组在内存中真正的地址值（十六进制的）。

#### 数组的索引

数组中的每一个元素都有一个编号，也叫索引，我们可以通过索引来获取或者修改数组中对应位置的元素。需要注意的是，索引是从0开始的，即索引0对应的是数组中的第一个元素。

```java
// 通过索引获取数组中的元素
int[] arr1 = {1, 2, 3, 4, 5};
System.out.println(arr1[0]); //1
System.out.println(arr1[1]); //2

// 通过索引修改数组中的元素
arr1[0] = 100;
System.out.println(arr1[0]);
```

#### 数组的遍历

可以借助for循环依次访问数组的每一个元素，这个过程也叫数组的遍历。循环的次数需要和数组中元素的数量一致，在Java中，可以通过`数组名.length`获取到数组的长度（即数组中元素的个数）。

```java
int[] arr1 = {1, 2, 3, 4, 5};
// 普通for循环
for (int i = 0; i < arr1.length; i++) {
    System.out.println(arr1[i]);
}

// 增强for循环
for (int n : arr1) {
    System.out.println(n);
}
```

> 小技巧：在idea中，可以通过`数组名.fori`快速生成遍历数组的for循环；也可以通过`数组名.for`快速生成遍历数组的增强for循环。

### 3.10  方法

在Java中，方法（Method）是类或对象的行为的体现，用于执行特定的任务或操作。方法可以接收输入参数，并返回一个结果。方法是Java程序的基本构建块之一，通常用于封装代码逻辑，提高代码的可重用性和可维护性。

#### 方法的定义

由于Java是一门纯面向对象编程语言，所有方法都要定义在类中，包括主方法，而有些方法属于类（静态方法），有些方法属于具体的对象（实例方法），这个后面面向对象编程会讲到。这里以静态方法为例进行讲解。

方法的定义一般具有如下的语法格式：

```java
访问修饰符 static 返回值类型 方法名(参数列表) {
    方法体;
    return 返回值;
}
```

需要注意的是：

* 如果方法不需要参数，则参数列表可以为空；
* 如果方法返回值类型为void，即方法没有返回值，则可以不写return语句，或者只写return;
* 访问修饰符用于控制方法的访问权限。常见的访问修饰符有：
	* `public`：方法可以被任何类访问。
	* `private`：方法只能在定义它的类中访问。
	* `protected`：方法可以在同一个包内或子类中访问。
	* `default`（没有显式修饰符）：方法只能在同一个包内访问。

例如，定义一个方法，用于求两数之和：

```java
public static int sum(int a, int b) {
    return a + b;
}
```

> 小技巧：定义方法时思考两件事：
>
> 1. 这个方法要干嘛？（用于确定方法名和方法体）
>
> 2. 完成这件事需要什么？（用于确定该方法需要哪些参数）

#### 方法的调用

定义方法后，可以通过方法名调用它。如果方法有返回值，可以将返回值赋给变量或直接使用。

```java
public class MethodDemo01 {
    // 主方法（程序的入口）
    public static void main(String[] args) {
        // 方法调用
        int sum = sum(1, 2);
        System.out.println(sum);
    }
    
    // 求两数之和方法的定义
    public static int sum(int a, int b) {
        return a + b;
    }
}
```

#### 方法的重载

方法的重载指的是在一个类中，可以定义多个同名的方法，但它们的参数列表必须不同参数类型、参数数量或参数顺序不同）。方法重载与返回类型无关。

例如，下面这个类中的几个方法都满足重载方法：

```java
public class Calculator {
    // 方法 1：两个整数相加
    public static int add(int a, int b) {
        return a + b;
    }

    // 方法 2：三个整数相加
    public static int add(int a, int b, int c) {
        return a + b + c;
    }

    // 方法 3：两个浮点数相加
    public static double add(double a, double b) {
        return a + b;
    }
    
    // 方法 4：一个整数和一个浮点数相加
    public static double add(double a, int b) {
        return a + b;
    }
    
    // 方法 5：一个浮点数和一个整数相加
    public static double add(int a, double b) {
        return a + b;
    }
}
```

#### 参数的传递

在Java中，所有方法的参数都是按值传递的，即形参拿到的是实参的副本。但需要区分基本数据类型参数和引用数据类型参数的不同：

* 对于基本数据类型（如 `int`、`double`、`char` 等），Java是按值传递的。这意味着方法接收到的是实际值的副本，而不是原始变量本身。因此，方法内部对参数的修改不会影响原始变量。

	```java
	public class MethodDemo03 {
	    public static void main(String[] args) {
	        int num = 10;
	        System.out.println("调用方法前：" + num); //输出10
	        changeValue(num);
	        System.out.println("调用方法后：" + num);  //输出10（值未改变）
	    }
	
	    public static void changeValue(int value) {
	        value = 20; //修改的是副本，不影响原始变量
	        System.out.println("在方法内部：" + value); //输出20
	    }
	}
	```

* 对于引用数据类型（如数组、字符串、自定义类等），Java仍然是按值传递的，但传递的是对象的引用（地址）的副本。因此，方法内部可以通过引用修改对象的状态。

	```java
	public class MethodDemo04 {
	    public static void main(String[] args) {
	        int[] arr = {1, 2, 3};
	        System.out.println("方法调用前: " + arr[0]); //输出1
	        changeArray(arr);
	        System.out.println("方法调用后: " + arr[0]);  //输出10
	    }
	
	    public static void changeArray(int[] arr) {
	        arr[0] = 10; //修改数组元素
	        System.out.println("在方法内部: " + arr[0]); //输出10
	    }
	}
	```



## 四、Java面向对象

Java是一种面向对象编程（Object-Oriented Programming，OOP）语言，其核心思想是将现实世界中的事物抽象为对象，并通过类和对象来组织代码。简单来讲，面向对象编程就是借助对象来完成某些事情，对象封装了数据和操作数据的行为，通过对象之间的交互来解决问题，更有利于程序结构的清晰，也更符合人类解决问题的思维习惯。

### 4.1 类和对象

**1）类（Class）：**

类是Java中的一种抽象数据类型，它是对现实世界中某一类事物的抽象描述。同时，类也是对象的蓝图或模板，定义了对象的属性和行为。在Java中，通过`class`关键字来定义一个类。

下面是一个定义Dog类的例子：

```java
public class Dog {
    // 属性
    String name;
    int age;

    // 行为
    public void bark() {
        System.out.println(name + " is barking!");
    }

    public void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}
```

**2）对象（Object）：**

对象是类的实例，具有类定义的属性和行为。在Java中，通过`new`关键字来创建一个对象。创建对象后，可以访问对象的属性或者调用对象的行为来做一些事情。

下面是根据Dog类创建对象的例子：

```java
public class DogTest {
    public static void main(String[] args) {
        // 创建Dog类的对象
        Dog myDog = new Dog();
        
        // 访问对象的属性
        myDog.name = "buddy";
        myDog.age = "3";

        // 调用对象的行为
        myDog.bark();
        myDog.displayInfo();
    }
}
```

**3）注意事项：**

* 一个Java文件中可以定义多个类，但只能有一个类是`public`修饰，而且`public`修饰的类名必须和文件名一致；
* 通常我们定义的用来描述一类事物的类叫作Javabean类，并且我们通常不在Javabean类中编写`main`方法；
* 通常我们称包含`main`方法的类叫作入口类、启动类、测试类等 。

### 4.2 成员变量和成员方法

成员变量和成员方法是类的两个核心组成部分，它们共同定义了类的属性和行为。

**1）成员变量：**

成员变量是定义在类中、方法之外的变量，用于描述类的属性或状态。它们也被称为实例变量或字段。

成员变量具有如下特点：

* 成员变量有默认值（如 `int` 默认为 `0`，`boolean` 默认为 `false`，引用类型默认为 `null`），无需显式初始化。
* 可以使用 `public`、`private`、`protected` 或默认修饰符来控制访问权限。

比如上面的Dog类中的`name`和`age`就是成员变量。

**2）成员方法：**

成员方法是定义在类中的方法，用于描述类的行为或操作。它们可以访问和操作成员变量。

成员方法具有如下特点：

* 非静态的成员方法和构造方法隐含有一个`this`参数，该参数是一个特殊的引用，用于指向方法的调用者。
* 可以使用 `public`、`private`、`protected` 或默认修饰符来控制访问权限。

比如上面的Dog类中的`bark()`和`displayInfo()`就是成员方法。

### 4.3 构造方法

构造方法（Constructor）也叫构造器，是Java类中的一种特殊方法，它会在创建对象的时候，由虚拟机自动调用，进行对象的初始化工作。Java中的构造方法具有以下特点：

* 构造方法的名称必须与类名完全相同；
* 构造方法没有返回类型，连 `void` 也没有；
* 构造方法是在创建对象的时候自动调用的；
* 一个类可以有多个构造方法，前提是它们之间要满足重载关系；
* 如果一个类没有显式地定义任何构造方法，Java编译器会自动提供一个无参的默认构造方法；
* 如果我们显式地定义了构造方法，Java编译器就不会提供默认构造方法。

通常我们会在定义类的时候手动地编写一个无参构造方法和一个有参构造方法，有参构造方法可以在让我们创建对象的时候传入一些参数来初始化成员变量。下面是定义构造方法的正确格式：

```java
public class GirlFriend {
    // 成员变量
    String name;
    int age;
    
    // 无参构造
    public GirlFriend() {
    }
    
    // 有参构造
    public GirlFriend(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // 成员方法
    public void sleep() {
        System.out.println("女朋友在睡觉");
    }

    public void eat() {
        System.out.println("女朋友在吃饭");
    }
}
```

### 4.4 静态变量和静态方法

静态变量和静态方法是指采用`static`关键字修饰的成员变量和成员方法，而没有采用`static`关键字修饰的成员变量和成员方法也叫实例变量和实例方法。

静态变量和静态方法属于类，而不属于具体的实例对象，或者说它们被该类所有的实例所共享。我们可以通过类名或对象名访问静态变量和调用静态方法，但通常都采用类名进行访问和调用（这更符合常理）。

**1）静态变量：**

静态变量也叫类变量，它是随着类的加载而加载的，在内存中处于静态存储区。我们创建的多个实例对象共享同一个静态变量。

下面是一个静态变量的例子，在这个例子中，`count` 是一个静态变量，它在所有 `MyClass` 实例之间共享。每次创建 `MyClass` 的实例时，`count` 都会增加。

```java
public class MyClass {
    // 静态变量
    public static int count = 0;

    public MyClass() {
        count++; // 每次创建实例时，count增加
    }
    
    public static void main(String[] args) {
        MyClass obj1 = new MyClass();
        MyClass obj2 = new MyClass();

        System.out.println("Count: " + MyClass.count); // 输出: Count: 2
    }
}
```

**2）静态方法：**

静态方法也是随着类的加载而加载的，可以直接通过类名调用，而不需要创建类的实例。

下面是一个静态方法的例子，在这个例子中，`incrementCount` 是一个静态方法，它可以直接通过类名 `MyClass` 调用，而不需要创建 `MyClass` 的实例。

```java
public class MyClass {
    // 静态变量
    public static int count = 0;

    // 静态方法
    public static void incrementCount() {
        count++;
    }

    public static void main(String[] args) {
        MyClass.incrementCount(); // 直接通过类名调用静态方法
        System.out.println("Count: " + MyClass.count); // 输出: Count: 1
    }
}
```

**3）注意事项：**

* 静态方法中没有`this`关键字。

* 静态方法只能访问静态变量和调用其他静态方法。
* 非静态方法可以访问静态变量和调用其他静态方法，也可以访问非静态变量（实例变量）和调用其他非静态方法（实例方法）。

### 4.5 静态代码块

静态代码块是指类中用`static`关键字修饰的一段代码，用于在类加载时执行一些初始化操作。它在类加载时执行，并且只执行一次。

下面是一个静态代码块的例子，在该例子中，程序执行`main`方法前，首先要加载`MyClass`类，而静态代码块便在类加载时执行，初始化了 `count` 变量。

```java
public class MyClass {
    // 静态变量
    public static int count;

    // 静态代码块
    static {
        count = 10;
        System.out.println("Static block executed. Count: " + count);
    }

    public static void main(String[] args) {
        System.out.println("Main method executed. Count: " + count);
    }
}
```

同静态方法一样，静态代码块也只能访问静态变量和调用静态方法，因为静态代码块在类加载时执行，而此时类的实例可能还没有创建，因此无法访问实例成员。

### 4.6 封装

封装是面向对象编程的一大特性，它是指将对象的属性和行为隐藏在对象内部，只通过公共接口与外界交互。这样有利于数据的安全性和代码的可维护性。在Java中，可以通过使用访问修饰符（如 `private`、`public`、`protected`）来实现正确的封装。

通常，一个类代表什么，就得封装对应的数据和数据对应的行为。其中，数据一般采用private修饰，方法一般采用public修饰，针对私有化的数据，还需要提供相应的get/set方法来作为与外界交互的接口。所以，在Java中，一个标准的Javabean类应该向下面这样定义：

```java
public class User {
    // 成员变量
    private String username;
    private String password;
    private int age;

    // 无参构造
    public User() {
    }

    // 全参构造
    public User(String username, String password, int age) {
        this.username = username;
        this.password = password;
        this.age = age;
    }

    // get/set方法
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

> 小技巧：在idea中，可以通过快捷及`Alt + Insert`快速生成一个类的构造方法和set/get方法。

### 4.7 继承

继承是面向对象编程（OOP）的核心概念之一，它允许一个类（子类）继承另一个类（父类）的属性和方法。通过继承，子类可以复用父类的代码，并在此基础上进行扩展或修改。

Java中的继承具有以下特点：

* Java只支持单继承，不支持多继承，但支持多层继承。
* Java中所有的类都直接或间接地继承于Object类。
* 继承后，子类只能访问父类中非私有的成员变量和成员方法。

**1）继承的语法：**

在Java中，使用`extends`关键字来实现继承。需要注意的是，一个类只能有一个父类，这就是Java的单继承机制。

```java
class ParentClass {
    // 父类的属性和方法
}

class ChildClass extends ParentClass {
    // 子类的属性和方法
}
```

继承之后，子类可以直接使用父类的非私有属性和方法，无需重新编写。子类还可以在继承的基础上添加新的属性和方法，或重写父类的方法。

**2）继承的内容：**

子类可以继承父类中所有非私有的成员变量（`public`、`protected`、默认访问修饰符修饰的成员变量）。

```java
class Parent {
    public int publicVar = 1;
    protected int protectedVar = 2;
    int defaultVar = 3; // 默认访问修饰符
    private int privateVar = 4; // 子类不能直接访问
}

class Child extends Parent {
    void display() {
        System.out.println(publicVar);    // 可以访问
        System.out.println(protectedVar); // 可以访问
        System.out.println(defaultVar);   // 可以访问（如果在同一个包中）
        // System.out.println(privateVar); // 编译错误，不能访问
    }
}
```

子类可以继承父类中所有非私有的成员方法（`public`、`protected`、默认访问修饰符修饰的成员方法）。

```java
class Parent {
    public void publicMethod() {
        System.out.println("Public Method");
    }

    protected void protectedMethod() {
        System.out.println("Protected Method");
    }

    void defaultMethod() { // 默认访问修饰符
        System.out.println("Default Method");
    }

    private void privateMethod() { // 子类不能直接调用
        System.out.println("Private Method");
    }
}

class Child extends Parent {
    void callMethods() {
        publicMethod();    // 可以调用
        protectedMethod(); // 可以调用
        defaultMethod();   // 可以调用（如果在同一个包中）
        // privateMethod(); // 编译错误，不能调用
    }
}
```

子类不能继承父类的构造方法，但子类的构造方法会隐式或显式地调用父类的构造方法，毕竟先有父才能有子。

* 如果父类有无参构造方法，子类构造方法会隐式调用父类的无参构造方法。
* 如果父类没有无参构造方法，子类必须显式调用父类的有参构造方法（使用`super`关键字）。

```java
class Parent {
    Parent() {
        System.out.println("Parent无参构造方法");
    }

    Parent(String message) {
        System.out.println("Parent有参构造方法: " + message);
    }
}

class Child extends Parent {
    Child() {
        // 隐式调用父类的无参构造方法
        System.out.println("Child无参构造方法");
    }

    Child(String message) {
        super(message); // 显式调用父类的有参构造方法
        System.out.println("Child有参构造方法");
    }
}
```

**3）super关键字：**

在子类中可以使用`super`关键字，它代表父类的引用，可以通过`super`关键字访问父类的属性或调用父类的方法。

在下面的例子中，子类继承了父类的`value`属性，同时子类自己又定义了一个`value`属性，此时要想访问到父类中的`value`属性，就可以使用`super`关键字。

```java
class ParentClass {
    int value = 10;
}

class ChildClass extends ParentClass {
    int value = 20;

    void display() {
        System.out.println("ChildClass value: " + value); // 20
        System.out.println("ParentClass value: " + super.value); // 10
    }
}
```

同样，当父类没有无参构造方法，子类必须显式调用父类的有参构造方法时，也可以使用`super`关键字进行调用（上面已提到过）。

**4）方法的重写：**

子类可以重写父类的方法，以提供不同的实现。重写的方法必须与父类方法具有相同的名称、参数列表和返回类型。重写时可以使用`@Override`注解来明确表示这是一个重写方法，这时如果我们重写的语法有问题，`Override`注解将会报错。

```java
class ParentClass {
    void display() {
        System.out.println("ParentClass display");
    }
}

class ChildClass extends ParentClass {
    @Override
    void display() {
        System.out.println("ChildClass display");
    }
}
```

**5）final关键字：**

* 如果一个类被声明为`final`，则不能被继承。
* 如果一个方法被声明为`final`，则不能被子类重写。

```java
// 该类不能被继承
final class FinalClass {
   
}

class ParentClass {
    // 该方法不能被子类重写
    final void display() {
        System.out.println("Cannot override this method");
    }
}
```

### 4.8 多态

多态也是面向对象编程的一大特性。它指的是通过继承之后，一个父类拥有多个子类，这些子类就是父类的多种形态。我们可以将子类的对象赋值给父类的引用，这样，同一个方法的调用就可以根据对象的不同而表现出不同的行为。

**1）多态的实现：**

多态是通过方法重写和向上转型实现的。方法重写是指子类重新定义父类中的方法，向上转型是指将子类对象赋值给父类引用。

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();  // 创建Animal对象
        Animal myDog = new Dog();         // 向上转型
        Animal myCat = new Cat();         // 向上转型

        myAnimal.sound();  // 输出: Animal makes a sound
        myDog.sound();      // 输出: Dog barks
        myCat.sound();      // 输出: Cat meows
    }
}
```

可以看到，同样是`Animal`类型的三个对象，在调用`sound()`方法时表现出了不同的形态，这就是多态的体现。

**2）注意事项：**

* 通过父类引用只能调用父类中定义的方法，不能调用子类特有的方法。

### 4.9 包

包就是文件夹，在Java中，通过包来组织和管理各种各样的类，不同包中的类可以有相同的名字。一个类真正的名字（全类名）应该是其所在的包名加上类名。

**1）包的声明：**

包通过`package`关键字声明，通常位于Java源文件的开头。例如：

```java
package com.example.mypackage;

public class MyClass {
    // 类的实现
}
```

`com.example.mypackage`是包的名称，通常采用反向域名命名法（如`com.example`），以确保唯一性。包名对应文件系统的目录结构。例如，`com.example.mypackage`对应的目录是`com/example/mypackage`。

**2）包的导入：**

使用同一个包中的类时是不需要进行导包的。但当我们使用其他包中的类时，如果不想写全类名，就需要通过`import`语句进行导包：

```java
import com.example.mypackage.MyClass;

public class AnotherClass {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
    }
}
```

关于导包，有两点需要注意：

* 使用`Java.lang`包中的类时，也不需要我们进行显式地导包，由于该包中的类过于常用，导包工作由编译器自动帮我们完成了。

* 如果同时使用两个包中的同名类，需要使用全类名。

### 4.10 访问权限修饰符

在Java中，访问权限修饰符用于控制类、方法、变量访问范围。Java提供了四种访问权限修饰符：

**1）public：任何类都可以访问。**

**2）default（默认，不使用任何修饰符）：同一个包中的类可以访问。**

**3）protected：同一个包中的类可以访问，不同包中的子类也可以访问。**

**4）private：只有本类中可以访问。**

通常，`public`和`private`使用最多。

### 4.11 抽象类和抽象方法

抽象类是不能被实例化的类，通常作为其他类的基类。它用于定义一些通用的行为和属性，具体的实现由其子类完成。

抽象方法是没有方法体的方法，只有方法声明。它必须在抽象类中声明，且子类必须重写（实现）这些抽象方法，除非子类也是抽象类。

#### 抽象类的定义

在Java中，通过`abstract`关键字来定义一个抽象类：

```java
public abstract class 类名 {
    // 成员变量
    // 构造方法
    // 具体方法
    // 抽象方法
}
```

#### 抽象类的特点

* 抽象类不能被实例化。
* 抽象类可以有构造方法，供子类调用。
* 抽象类可以有抽象方法，也可以有具体方法。

#### 抽象方法的定义

抽象方法通过`abstract`关键字修饰：

```java
public abstract 返回类型 方法名(参数列表);
```

#### 抽象方法的特点

* 抽象方法只有方法声明，没有方法实现。
* 声明抽象方法的类必须是抽象类。
* 子类必须实现父类的所有抽象方法，除非子类也是抽象类。

### 4.12 接口

接口（Interface）也是Java中的一种引用数据类型，它用于定义一些抽象方法，类与接口之间是实现关系，一个类实现了某个接口，就得重写接口中的抽象方法。

接口是对行为的抽象，它不像抽象类那样要求子类处于同一个继承体系，不同继承体系中的类所具有的共同行为可以定义在接口中。Java不支持类的多继承，但通过接口可以实现类似的效果，一个类可以实现多个接口。

#### 接口的定义

接口的定义使用 `interface` 关键字，语法如下：

```java
public interface 接口名 {
    
}
```

#### 接口的特点

* 接口中可以定义静态常量。接口中的常量默认是 `public static final` 修饰的，即使不显式声明。

```java
public interface 接口名 {
    // 常量定义（默认是 public static final）
    数据类型 常量名 = 值; //等价于：public static final 数据类型 常量名 = 值;
}
```

* 接口中可以定义抽象方法。默认是 `public abstract` 修饰的，即使不显式声明。

```java
public interface 接口名 {
    // 方法定义（默认是 public abstract）
    返回类型 方法名(参数列表); //等价于：public abstract 返回类型 方法名(参数列表);
}
```

* 从Java 8开始，接口中可以定义默认方法和静态方法，默认方法可以有方法体，静态方法可以直接通过接口名调用。

```java
public interface 接口名 {
    // Java 8 开始支持默认方法和静态方法
    default 返回类型 方法名(参数列表) {
        // 默认方法实现
    }

    static 返回类型 方法名(参数列表) {
        // 静态方法实现
    }
}
```

* 从Java 9开始，接口中可以定义私有方法，用于在接口内部复用代码。

```java
public interface 接口名 {
    // Java 9 开始支持私有方法
    private 返回类型 方法名(参数列表) {
        // 私有方法实现
    }
}
```

#### 接口的继承

接口可以通过 `extends` 关键字继承其他接口，并且可以继承多个接口。

```java
public interface 子接口 extends 父接口1, 父接口2 {
    // 可以定义新的方法
}
```

#### 接口的实现

类通过 `implements` 关键字实现接口，并且必须实现接口中定义的所有抽象方法（除非该类是抽象类）。

```java
public class 类名 implements 接口名 {
    @Override
    public 返回类型 方法名(参数列表) {
        // 方法实现
    }
}
```

一个类可以实现多个接口：

```java
public class 类名 implements 接口1, 接口2, 接口3 {
    // 实现所有接口中的方法
}
```

### 4.13 内部类

Java的内部类（Inner Class）是指定义在另一个类内部的类，它提供了更灵活的代码组织方式，并可以访问外部类的成员。内部类主要有四种类型：成员内部类、局部内部类、匿名内部类和静态内部类。

当一个类属于另一个类的一部分，且单独存在又没什么意义，我们便可以将它定义为另一个类的内部类。

#### 成员内部类

直接定义在外部类的内部，与成员变量/方法同级的类称为成员内部类。

示例：

```java
class Outer {
    private int num = 10;

    class Inner {
        public void show() {
            System.out.println("Outer num: " + num); // 直接访问外部类私有成员
        }
    }
}
```

特点：

* 必须先创建外部类的对象后，才能创建成员内部类的对象。

```java
Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
```

* 成员内部类可以访问外部类的所有成员（包括私有），而外部类无法访问成员内部类的成员。

```java
class Outer {
    private int num1 = 10;
    
    public void show() {
        System.out.println(num2); // 外部类不能访问内部类的成员
    }

    class Inner {
        private int num2 = 20;
        public void show() {
            System.out.println("Outer num: " + num1); // 成员内部类可以访问外部类的成员
        }
    }
}
```

#### 静态内部类

采用`static`关键字修饰的内部类称为静态内部类。

示例：

```java
class Outer {
    private static int staticNum = 10;

    static class Inner {
        public void show() {
            System.out.println("Static num: " + staticNum); // 只能访问外部类的静态成员
        }
    }
}
```

特点：

* 创建静态内部类的对象可以不用先常见外部类的对象。

```java
Outer.Inner inner = new Outer.Inner();
```

* 静态内部类只能访问外部类的静态成员。

```java
class Outer {
    private int num = 10;
    private static int staticNum = 10;

    static class Inner {
        public void show() {
            System.out.println("Num: " + num); // 不能访问外部类的非静态成员
            System.out.println("Static num: " + staticNum); // 只能访问外部类的静态成员
        }
    }
}
```

#### 局部内部类

定义在方法中的类称为局部内部类。

示例：

```java
class Outer {
    int num1 = 10;
    
    public void method() {
        int num2 = 20;

        class Inner {
            public void show() {
                System.out.println("Outer variable: " + num1); // 可以访问外部类的成员变量
                System.out.println("Local variable: " + num2); // 可以访问方法的局部变量
            }
        }

        Inner inner = new Inner();
        inner.show();
    }
}
```

特点：

* 只能在方法内部创建对象并使用。
* 可以访问外部类的成员，也可以访问方法内的局部变量。

#### 匿名内部类 !

匿名内部类是指没有名字的内部类，它可以帮助我们快速创建某个类的子类的对象或者某个接口的实现类对象。匿名内部类的特点是在通过`new`关键字创建对象的同时定义类体，往往这个类只需要用一次，所以我们完全没必要单独定义它并给它起个名字。

语法：

```java
// 语法示例
父类/接口 对象名 = new 父类/接口() {
    // 重写或者实现方法
};
```

示例：

```java
class Outer {
    public static void main(String[] args) {
        // 创建对象的同时定义出匿名内部类的类体
        Animal dog = new Animal() {
            public void eat() {
                System.out.println("Dog eat");
            }
        };

        dog.eat();
    }
}

class Animal {
    public void eat() {
        System.out.println("Animal eat");
    }
}
```

### 4.14 函数式编程

#### 函数式接口

函数式接口是只有一个抽象方法的接口，比如`Runnable`、`Comparator`等。Java 8中引入了`@FunctionalInterface`注解来标识这样的接口，这样编译器会检查是否符合条件。

#### Lambda表达式

`Lambda`表达式允许我们直接将函数作为方法参数，简化匿名内部类的书写。

比如，在之前版本的Java中，如果某个方法的参数是一个接口类型，需要我们传入一个该接口的实现类对象，我们会采用匿名内部类的形式书写。

```java
// 定义一个无序数组
Integer[] arr = {1, 3, 2, 5, 4, 6, 10, 8, 9, 7};
// 调用Arrays类的sort方法，使用匿名内部类创建对象作为第二个参数
Arrays.sort(arr, new Comparator<Integer>() {
    @Override
    public int compare(Integer o1, Integer o2) {
        return o1 - o2;
    }
});
// 输出排序后的数组
System.out.println(Arrays.toString(arr)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

在上面这个例子中，`Comparator`接口中只有一个抽象方法`compare()`，它是一个函数式接口，我们传入该接口的实现类对象也只是为了使用其中的方法。而`Lambda`表达式就允许我们简化这种匿名内部类的写法。`Lambda`表达式的语法格式为：

```java
(参数列表) -> { 方法体 }
```

其中：

* 参数类型可以省略。
* 只有一个参数的话，小括号可以省略。
* 方法体只有一行语句的话，可以省略大括号、return和分号。

比如，上面的例子通过`Lambda`表达式可以这样写：

```java
// 定义一个无序数组
Integer[] arr = {1, 3, 2, 5, 4, 6, 10, 8, 9, 7};

// 通过Lambda表达式传入第二个参数
// 完整写法
/*Arrays.sort(arr, (Integer o1, Integer o2) -> {
            return o1 - o2;
        });*/
// 简化写法
Arrays.sort(arr, (o1, o2) -> o1 - o2);

// 输出排序后的数组
System.out.println(Arrays.toString(arr)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

