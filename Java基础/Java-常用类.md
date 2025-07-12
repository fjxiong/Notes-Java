# Java常用类

学习Java的面向对象编程，不光要学习如何定义一个对象，还要学习如何使用已有的对象，尤其是Java标准库中定义的对象。

## 1. Object

在Java中，`Object`类是所有类的顶级父类，位于`java.lang`包中，所有类都直接或间接继承自它。因此，`Object`类中的方法对所有对象都可用。`Object`类的一个重要的作用就是提供所有对象所必要的一些基础方法。

### 常用方法

##### 1. `public String toString()`：返回对象的字符串表示（默认为：`类名@哈希码`）。

使用示例：

```java
// 创建对象
Object obj = new Object();
// 调用toString方法将对象转为字符串形式
String str = obj.toString();
// 输出对象对应的字符串
System.out.println(str); // java.lang.Object@776ec8df
```

值得注意的是，当我们直接打印对象时，`println()`方法在底层会自动调用对象的`toString()`方法，所以我们直接打印对象也可以得到同样的效果。

```java
// 创建对象
Object obj = new Object();
// 直接打印对象，也会默认调用对象的toString方法
System.out.println(obj); // java.lang.Object@776ec8df
```

`Object`类中定义的`toString()`方法返回的字符串默认为`类名@哈希码`的形式，通常这个形式对我们来说没什么意义，我们更期望调用一个对象的`toString()`方法时，可以返回该对象的具体信息（比如属性值的展示），这时就需要对`toString()`方法进行重写。

最常见的`String`类就实现了对`toString()`方法的重写，使得我们在打印字符串对象时，得到的不再是`类名@哈希码`的形式，而是字符串本身的值。

```java
// 创建字符串对象
String str = "hello呀";
// 打印字符串对象（自动调用字符串对象的toString方法）
System.out.println(str); // hello呀
```

当然了，我们自己定义的类也可以重写`toString()`方法来实现想要的输出效果。比如我们定义一个`Student`类，并重写其`toString()`方法。

```java
class Student {
    String name;
    int age;

    @Override
    public String toString() {
        return "Student{name=" + name + ", age=" + age + "}";
    }
}
```

此时，我们再打印`Student`类就不再是`类名@哈希码`的形式了，而是可以看到类中属性值的展示。

```java
// 创建对象并赋予属性
Student stu = new Student();
stu.name = "小明";
stu.age = 20;
// 打印学生对象（自动调用学生对象的toString方法）
System.out.println(stu); // Student{name=小明, age=20}
```

##### 2. `public boolean equals(Object obj)`：比较两个对象是否“相等”（默认比较内存地址是否相等）。

`Object`类中该方法的源码：

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

在`Object`类中，`equals()`方法比较的是两个对象的地址值是否相等。也就是说，有两个对象，它们的地址值不同，即使它们的属性值一致，比较的结果也是`false`。

```java
// 创建两个学生对象并赋予相同的属性值
Student stu1 = new Student("小明", 20);
Student stu2 = new Student("小明", 20);

// 调用默认的equals方法进行比较
System.out.println(stu1.equals(stu2)); // false
```

但通常我们认为两个对象的“相等”是指属性值的相等，而不是地址值的相等，这时就需要对`equals()`方法进行重写。

最常见的`String`类就已经对`equals()`方法进行了重写，所以我们在调用字符串的`equals()`方法进行字符串的比较时，比较的就是字符串的内容是否相等了。

```java
// 创建两个字符串对象
String str1 = new String("hello");
String str2 = new String("hello");

// 调用String类中重写的equals方法进行比较
System.out.println(str1.equals(str2)); // true
```

当然，我们也可以让自定义的`Student`类重写`equals()`方法，在重写的`equals()`方法中编写正确的比较逻辑，来实现通过属性值判断两个对象是否相等。

```java
class Student {
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true; // 如果二者的地址值相同，即同一个对象，则没必要进行下面的比较
        if (o == null || getClass() != o.getClass()) return false; // 如果比较的两个对象不是同一个类型，则不相等
        Student student = (Student) o;
        return age == student.age && name.equals(student.name); // 判断属性值是否相等
    }
}
```

此时，我们调用`Student`类重写的`equals()`方法进行比较，就可以实现我们想要的效果了。

```java
// 创建两个学生对象并赋予相同的属性值
Student stu1 = new Student("小明", 20);
Student stu2 = new Student("小明", 20);

// 调用重写后的equals方法进行比较
System.out.println(stu1.equals(stu2)); // true
```

##### 3. `public int hashCode()`：返回对象的哈希值（默认根据地址值返回一个整数）。

`hashCode()`方法用于返回对象的哈希值，通常当我们用哈希表这种数据结构来存储对象时，需要使用到该方法。

需要注意的是，如果两个对象相等（`equals()`返回`true`），则它们的哈希值也必须相同。反过来则不一定，所以如果重写了`equals()`方法，必须同时重写`hashCode()`方法。

最常见的`String`类就同时重写了`equals()`方法和`hashCode()`方法，以确保哈希行为的一致性。

```java
// 创建两个字符串对象
String str1 = new String("hello");
String str2 = new String("hello");

// 调用String类中重写的equals方法进行比较
System.out.println(str1.equals(str2)); // true

// 调用String类中重写的hashCode方法计算对象的哈希值
System.out.println(str1.hashCode()); // 99162322
System.out.println(str2.hashCode()); // 99162322
```



---



## 2. String

`String`类是Java标准库中的一个核心类，位于`java.lang`包中，它用于表示和操作字符串。Java中的所有字符串都被视为`String`类的对象。`String`类在内部通过一个`char[]`数组来表示字符串，并且采用`final`修饰，所以字符串对象是不可变的。

### 字符串对象的创建

**1) 通过双引号创建：**

在Java中，所有的字符串都被视为`String`类的对象，所以我们通过双引号括起来的字符序列就是一个字符串对象：

```java
String str = "songyuqiqiqi";
```

**2) 通过new关键字创建：**

我们也可以像创建一般类的对象那样，通过new关键字联合构造方法来创建字符串对象：

```java
//创建一个空白字符串，不包含任何内容
String str1 = new String(); //""

//根据传入的字符串，创建字符串对象
String str2 = new String("abc"); //"abc"

//根据字符数组，创建字符串对象
char[] chs = {'a', 'b', 'c'};
String str3 = new String(chs); //"abc"

//根据字节数组，创建字符串对象
byte[] bytes = {97, 98, 99};
String str3 = new String(bytes); //"abc"
```

### 字符串常量池

Java为了提高性能，引入了字符串常量池（String Pool）。当使用双引号创建字符串时，JVM会首先检查字符串常量池中是否已经存在相同内容的字符串。如果存在，则直接返回池中的引用；如果不存在，则在池中创建一个新的字符串对象并返回其引用。例如：

```java
String s1 = "Hello";
String s2 = "Hello"; //s1和s2指向的是同一个对象
```

此时，在内存（字符串常量池）中只创建了一个字符串对象，具体过程为：

* 将"Hello"赋值给s1变量时，JVM发现"Hello"并不存在于字符串常量池中，于是在池中创建一个"Hello"对象，并返回其引用；

* 当我们再把"Hello"赋值给s2变量时，JVM发现字符串常量池中已经存在相同内容的字符串，于是直接返回池中的引用。

而使用`new`关键字创建的字符串对象不会使用常量池，每次都会在堆内存中创建一个新的对象：

```java
String s3 = new String("Hello");
String s4 = new String("Hello"); //s3和s4指向的是两个不同的对象
```

综上，可以发现，使用双引号创建字符串对象的方式和使用new关键字创建字符串对象的方式不仅仅只是形式上不同。使用双引号创建字符串对象的方式可以共用字符串常量池，节约内存空间；而使用new关键字创建字符串对象的方式每次都会在堆内存中创建一个新的字符串对象。 所以在没有特别需求的时候，我们大多数都会采用第一种方式来创建字符串对象，又简单又节省内存，何乐而不为？

### 常用方法

`String`类提供了丰富的方法来操作字符串，以下是一些常用的方法：

#### 1. 字符串长度

* `int length()`：返回字符串的长度。

```java
String str = "Hello";
int length = str.length();  //5
```

#### 2. 字符串比较

* `boolean equals(Object anObject)`：比较字符串内容是否相等。
* `boolean equalsIgnoreCase(String anotherString)`：忽略大小写比较字符串内容是否相等。
* `int compareTo(String anotherString)`：按字典顺序比较两个字符串。
* `int compareToIgnoreCase(String str)`：忽略大小写按字典顺序比较两个字符串。

通常，我们比较两个字符串是否相等，是想比较它们的内容是否相等，这时就需要借助`equals()`方法来进行比较，而不能采用`==`运算符来进行比较，因为`==`运算符比较的是两个变量存储的值是否相等。对于基本数据类型，比较的就是它们的值是否相等，但对于字符串这种引用数据类型，比较的其实是它们的地址值是否相等。

所以，在进行字符串的比较时，总是采用`equals()`方法进行比较。

```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello");
System.out.println(s1 == s2); //true
System.out.println(s1 == s3); //false
System.out.println(s1.equals(s3)); //true
```

#### 3. 字符串查找

* `boolean contains(CharSequence s)`：判断字符串是否包含指定的字符序列。
* `int indexOf(String str)`：返回指定子字符串第一次出现的索引。
* `int lastIndexOf(String str)`：返回指定子字符串最后一次出现的索引。
* `boolean startsWith(String prefix)`：判断字符串是否以指定的前缀开始。
* `boolean endsWith(String suffix)`：判断字符串是否以指定的后缀结束。

```java
String str = "Hello World";
boolean contains = str.contains("World"); //true
int index = str.indexOf("World"); //6
int lastIndex = str.lastIndexOf("o"); //7
boolean startsWith = str.startsWith("Hello"); //true
boolean endsWith = str.endsWith("World"); //true
```

#### 4. 字符串截取

* `String substring(int beginIndex)`：返回从指定索引开始到字符串末尾的子字符串。
* `String substring(int beginIndex, int endIndex)`：返回从指定索引开始到指定索引结束的子字符串。

```java
String str = "Hello World";
String sub1 = str.substring(6); //"World"
String sub2 = str.substring(0, 5); //"Hello"
```

#### 5. 字符串替换

* `String replace(char oldChar, char newChar)`：替换字符串中的所有指定字符。
* `String replace(CharSequence target, CharSequence replacement)`：替换字符串中的所有指定字符序列。

```java
String str = "Hello World";
String replaced = str.replace('o', 'a'); //"Hella Warld"
String replacedAll = str.replace("World", "Java"); //"Hello Java"
```

#### 6. 字符串分割

* `String[] split(String regex)`：根据正则表达式将字符串分割为数组。

```java
String str = "Hello,World,Java";
String[] parts = str.split(","); //["Hello", "World", "Java"]
```

#### 7. 字符串大小写转换

* `String toLowerCase()`：将字符串转换为小写。
* `String toUpperCase()`：将字符串转换为大写。

```java
String str = "Hello World";
String lower = str.toLowerCase(); //"hello world"
String upper = str.toUpperCase(); //"HELLO WORLD"
```

#### 8. 字符串的拼接

* `String concat(String str)`：将指定字符串连接到此字符串的末尾。

```java
String str1 = "Hello";
String str2 = "World";
String result = str1.concat(" ").concat(str2); //"Hello World"
```

除了使用`concat()`方法来拼接字符串，还可以使用`+`运算符。

当`+`运算符操作的对象包含字符串时，这时`+`不再是算术运算符，而是字符串连接符。字符串连接符会将前后数据都当作字符串进行拼接，并产生一个新字符串。例如：

```java
System.out.println(1 + 2 + "abc" + 2 + 1); //结果是：3abc21
```

解释：

* 第一步：1 + 2 。在这个过程中，没有字符串参与，所以做的是加法运算，结果为3。

* 第二步：3 + "abc"。在这个过程中，有字符串参与，所以做的是拼接操作，产生一个新的字符串"3abc"。
* 第三步："3abc" + 2。在这个过程中，有字符串参与，所以做的是拼接操作，产生一个新的字符串"3abc2"。
* 第四步："3abc2" + 1。在这个过程中，有字符串参与，所以做的是拼接操作，产生一个新的字符串“3abc21”

#### 9.  字符串转换为字符数组

* `char[] toCharArray()`：将字符串转换为字符数组。

```java
String str = "Hello";
char[] chs = str.toCharArray(); //['H', 'e', 'l', 'l', 'o']
```

### 与字符串拼接相关的类

#### StringBuilder

当我们需要做大量的字符串拼接操作时，采用`+`运算符连接或者调用`concat()`方法每次都会创建一个新的字符串对象，既浪费内存，又影响效率。

为了能高效拼接字符串，Java标准库提供了`StringBuilder`这个类，它是一个可变对象，可以将它视为存放字符串的容器，往该容器中新增字符时，不会创建新的临时对象：

```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10; i++) {
    sb.append(i);
}
String str = sb.toString();
System.out.println(str); //0123456789
```

`StringBuilder`还支持链式编程：

```java
StringBuilder sb = new StringBuilder();
String str = sb.append("a").append("b").append("c").toString();
System.out.println(str); //abc
```

`StringBuilder`还提供了`reverse()`方法用于实现字符串的反转：

```java
StringBuilder sb = new StringBuilder();
String str = sb.append("abc").reverse().toString();
System.out.println(str); //cba
```

#### StringJoiner

`StringJoiner`和`StringBuilder`功能类似，也是用于高效地拼接字符串，不过`StringJoiner`可以指定在拼接字符串时的间隔符号、开始符号和结束符号。

```java
StringJoiner sj = new StringJoiner(",", "[", "]");
sj.add("a").add("b").add("c");
String str = sj.toString();
System.out.println(str); //[a,b,c]
```



---



## 3. Math

Java中的`Math`类是`java.lang`包下的一个工具类，提供了一系列静态方法用于执行数学运算。

### 静态常量

* **`Math.PI`**：表示圆周率π，约等于3.141592653589793。
	
* **`Math.E`**：表示自然对数的底数e，约等于2.718281828459045。

### 常用方法

#### 1. 基本运算

* **绝对值**
	`static double abs(double a)`
	`static int abs(int a)`

	......（支持多种数据类型）

	```java
	System.out.println(Math.abs(10)); //10
	System.out.println(Math.abs(-10)); //10
	System.out.println(Math.abs(-10.0)); //10.0
	```

* **最大值/最小值**
	`static int max(int a, int b)`
	`static double min(double a, double b)`

	......（支持多种数据类型）

	```java
	System.out.println(Math.max(10, 20)); //20
	System.out.println(Math.min(10.1, 10.2)); //10.1
	```

* **四舍五入**
	`static long round(double a)`：返回最接近的long值。
	`static int round(float a)`：返回最接近的int值。

	```java
	System.out.println(Math.round(10.2)); //10
	System.out.println(Math.round(10.5)); //11
	```

* **向上/向下取整**
	`static double ceil(double a)`：返回≥参数的最小整数（double类型）。
	`static double floor(double a)`：返回≤参数的最大整数（double类型）。

	```java
	System.out.println(Math.ceil(10.2)); //11.0
	System.out.println(Math.floor(10.6)); //10.0
	```

#### 2. 指数与对数

* **幂运算**
	`static double pow(double a, double b)`：返回a的b次方。

	```java
	System.out.println(Math.pow(2, 3)); //8.0
	```

* **平方根与立方根**
	`static double sqrt(double a)`
	`static double cbrt(double a)`

	```java
	System.out.println(Math.sqrt(16)); //4.0
	System.out.println(Math.cbrt(8)); //2.0
	```

* **自然对数和底数对数**
	`static double log(double a)`：自然对数（底为e）。
	`static double log10(double a)`：以10为底的对数。

	```java
	System.out.println(Math.log(Math.E)); //1.0
	System.out.println(Math.log10(100)); //2.0
	```

#### 3. 随机数

* **生成随机数**
	`static double random()`：返回[0.0, 1.0)之间的double值。

	```java
	System.out.println(Math.random()); //返回[0.0, 1.0)之间的随机数
	System.out.println((int)(Math.random() * 100)); //返回[0, 99)的随机数
	```

#### 4. 其他方法

* **精确算术运算（Java 8+）**
	`static int addExact(int a, int b)`：加法，溢出时抛出`ArithmeticException`。
	类似方法：`subtractExact`, `multiplyExact`。



---



## 4. System

Java中的`System`类是一个非常重要的工具类，位于`java.lang`包中，无需显式导入即可使用。它提供了与系统交互的核心功能，包括标准输入输出、系统属性管理、环境变量访问、时间获取、数组操作等。

### 静态常量

`System`类提供了三个静态常量，用于标准输入、输出和错误输出：

* **`System.in`**：标准输入流（通常是键盘输入）。
* **`System.out`**：标准输出流（控制台输出）。
* **`System.err`**：标准错误输出流（通常用于输出错误信息）。

```java
Scanner scanner = new Scanner(System.in); // 从键盘读取输入
System.out.println("Hello World");  // 输出到控制台
System.err.println("Error occurred!");    // 输出错误信息
```

### 常用方法

##### 1. `currentTimeMillis()`：返回当前时间的毫秒值。

`System`类中的`currentTimeMillis()`方法用于返回从时间原点（1970年1月1日）到现在所经历的毫秒值，它可以用来测试某段代码的执行时间。

```java
// 计算代码执行时间
long startTime = System.currentTimeMillis();
// 执行某些代码...
long endTime = System.currentTimeMillis();
System.out.println("耗时：" + (endTime - startTime) + "ms");
```

##### 2. `exit(int status)`：终止JVM，`status`为0表示正常退出，非0表示异常终止。

```java
System.exit(0); // 终止程序
```

##### 3. `arraycopy(Object src, int  srcPos, Object dest, int destPos, int length)`：用于高效复制数组。

参数说明：源数组、源起始位置、目标数组、目标起始位置、拷贝长度。

```java
int[] src = {1, 2, 3, 4, 5};
int[] dest = new int[5];
System.arraycopy(src, 0, dest, 0, src.length);
```



---



## 5. Random

Java中的`Random`类位于`java.util`包中，用于生成伪随机数序列。它是基于确定性算法生成的随机数，因此称为“伪随机”。

### Random对象的创建

* **无参构造方法**：使用系统时间（纳秒级）作为种子。

	```java
	Random random = new Random();
	```

* **指定种子的构造方法**：相同的种子会生成相同的随机数序列，适用于需要可复现的场景。

	```java
	Random randomWithSeed = new Random(123L); // 种子为123
	```

### 常用方法

##### 1. `nextInt()`：生成整数范围内（包含负数）的随机整数。

```java
// 创建对象
Random random = new Random();
// 获取一个随机整数(在整个int范围内)
int num = random.nextInt();
System.out.println(num); // 1873211484  -1985581843  -753286674 ...，每次获取都不一样
```

##### 2. `nextInt(int bound)`：生成`[0, bound)`之间的整数。

```java
// 获取指定范围内的随机整数
int num = random.nextInt(10); // 生成0~9的整数
System.out.println(num); //8 2 5 5 ...
```

##### 3. `nextDouble()`：生成`[0.0, 1.0)`之间的双精度浮点数。

```java
// 获取[0.0, 1.0)范围内的浮点数
double num = random.nextDouble();
System.out.println(num); // 0.43450477366704077
```

##### 4. `nextFloat()`：生成`[0.0, 1.0)`之间的单精度浮点数。

```java
// 获取[0.0, 1.0)范围内的浮点数
float num = random.nextFloat();
System.out.println(num); //0.7023995
```



---



## 6. Integer

`Integer`是Java中的一个包装类。在Java中，包装类（Wrapper Classes）是将基本数据类型封装为对象的类。由于Java是面向对象的语言，许多API（如集合类）需要操作对象而非基本类型，因此包装类提供了基本类型和对象之间的桥梁。

在Java中，八种基本数据类型都有对应的包装类，这里以最常用的`Integer`为例，来讲解包装类的使用场景和注意事项。

### Integer对象的创建

1. 构造方法（JDK 9以后已弃用）

```java
Integer i = new Integer(10);
```

2. 静态工厂方法（推荐）

```java
Integer i = Integer.valueOf(10);
```

3. 自动装箱（更简洁）

```java
Integer i = 10; // 编译器自动转换为Integer i = Integer.valueOf(10);
```

### 自动装箱与自动拆箱

JDK 5以前，想实现包装类和基本数据类型之间的转换，需要借助`Integer`中的`ValueOf()`和`intValue()`方法。

```java
// 基本数据类型 -> 包装类
Integer a = Integer.valueOf(10);
// 包装类 -> 基本数据类型
int b = a.intValue();
```

JDK 5以后，出现了自动装箱与自动拆箱机制，即我们可以不用显式地调用方法实现包装类和基本数据类型之间的转换了，编译器会自动帮我们做这项工作。

```java
// 基本数据类型 -> 包装类
Integer a = 10; // 编译器自动转换为Integer a = Integer.valueOf(10);
// 包装类 -> 基本数据类型
int b = a; // 编译器自动转换为int b = a.intValue();
```

### 缓存机制

部分包装类（如 `Integer`、`Byte`、`Short`、`Long`）会缓存特定范围的值（通常为-128~127），以提高性能。

```java
Integer a = 127;
Integer b = 127;
System.out.println(a == b); // true（同一缓存对象）

Integer c = 200;
Integer d = 200;
System.out.println(c == d); // false（超出缓存范围，新建对象）
```

### 常用方法

##### 1. `valueOf(int i)`/`valueOf(String s)`：将基本类型或字符串转为包装类。

```java
Integer i1 = Integer.valueOf(10); // 已被自动装箱代替
Integer i2 = Integer.valueOf("123");
```

##### 2. `intValue()`：将包装类转为基本类型。

```java
Integer a = 10;
int b = a.intValue(); // 已被自动拆箱代替
```

##### 3. `parseInt(String s)`：将字符串转为包装类。

```java
int i = Integer.parseInt("123");
```

##### 4. `toXxxString(int i)`：获取整数的某种进制的表现形式。

```java
// 100的二进制表示
String str1 = Integer.toBinaryString(100);
System.out.println(str1); // 1100100
// 100的16进制表示
String str2 = Integer.toHexString(100);
System.out.println(str2); // 64
```



---



## 7. Arrays

Java中的`Arrays`类位于`java.util`包中，是一个用于操作数组的工具类，提供了丰富的静态方法，涵盖排序、搜索、比较、填充等常用功能。

### 常用方法

##### 1. `toString(数组)`：数组转字符串。

```java
int[] arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
System.out.println(Arrays.toString(arr)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

##### 2. `copyOf(原数组, int newLength)`：数组拷贝。

参数1：要拷贝的数组。
参数2：新数组的长度(通常和要拷贝的数组保持一致)。

```java
int[] arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
int[] newArr = Arrays.copyOf(arr, arr.length);
System.out.println(Arrays.toString(newArr)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

##### 3. `copyOfRange(原数组, int from, int to)`：数组拷贝（拷贝一定范围内的元素）。

参数1：要拷贝的数组。
参数2：拷贝的起始索引（包括）。
参数3：拷贝的终止索引（不包括）。

```java
int[] arr = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
int[] newArr2 = Arrays.copyOfRange(arr, 0, 10);
System.out.println(Arrays.toString(newArr2)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

##### 4. `sort(数组)`：数组升序排序。

```java
int[] arr2 = {1, 3, 2, 5, 4, 7, 8, 10, 9, 6};
Arrays.sort(arr2);
System.out.println(Arrays.toString(arr2)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

##### 5.` sort(数组, 排序规则)`：按照排序规则进行排序。

这里第二个参数需要传入一个`Comparator`接口的实现类，其中的`compare()`方法定义了元素比较的规则，`sort()`方法依据该规则对元素进行排序。这里我们先不探究`sort()`方法的具体原理，暂且记住下述规则：

对于`compare()`方法的两个参数o1和o2：

* `return o1 - o2`：升序排序。
* `return o2 - o1`：降序排序。

```java
Integer[] arr3 = {1, 3, 2, 5, 4, 7, 8, 10, 9, 6};
Arrays.sort(arr3, new Comparator<Integer>() {
    @Override
    public int compare(Integer o1, Integer o2) {
        return o2 - o1;
    }
});
System.out.println(Arrays.toString(arr3)); // [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```

