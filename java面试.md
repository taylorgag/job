# java面试

## java语言

```
1. JVM(c++写的一个虚拟的计算机)  
不同的操作系统，肯定要使用不同的JVM。但是由于java程序是直接与jvm打交道，所以java程序一次编译之后，不会随着操作系统不同，发生修改。也就是说，JVM屏蔽了操作系统的差异。
但是，JVM怎么来的？
安装JDK的时候，自带JVM。所以JDK也有不同的版本（有windows和linux版本的）
 
JDK、JRE、JVM三者之间的关系？
JDK:java开发工具箱；
JRE:java运行环境
JVM:java虚拟机
JDK包括JRE,JRE包括JVM.有独立的JDK和JRE安装包，但是没有独立的JVM安装包。在安装JDK的时候，JRE就安装好了，JRE内部的JVM也安装好了。

GC(垃圾回收机制)

2. java的加载与执行
java程序的两个阶段：编译和运行。
编译：将普通代码文本转成JVM可以识别的“字节码”，称为编译；javac编译，将.java文件生成.class的字节码文件
     一个.java源程序可以编译生成多个.class文件，（A.class,B.class..)其中，A,B都是类的名字。
运行（JRE在起作用）：java运行。    .class文件首先加载到类加载器上，然后装载到java虚拟机上，java虚拟机将它变成可以被操作系统识别的二进制文件。

3.JVM内存结构
JVM主要的三块内存空间：栈、堆、方法区。除了这三块之外，还有其他的。

4.java创建对象的方式：使用new关键字、利用java的反射机制、实现Cloneable接口使用克隆方法、java的序列化和反序列化

5.java中的访问方式有4种，对于修饰类

6.被final修饰的类可以被重载但不能被重写。
```

**多态**

父类型的引用指向子类型的对象，父类型里面没有的方法，直接使用的话要不然强制类型转换，要不然就在父类型里面定义这个方法。

也就是说，什么是多态呢？

父类型和子类型里面有相同的方法，子类型却表现出和父亲不一样的行为

以下代码编译错误：

```java
class Base{
    public void method(){
        System.out.println("Base");
    }
}
class Son extends Base{
    @Override
    public void method() {
        System.out.println("Son");
    }
    public void methodB(){
        System.out.println("SonB");
    }
}

public class test02 {
    public static void main(String[] args) {
        Base base = new Son();
        base.method();
        base.methodB();//直接不通过，可改成((Son) base).methodB();
    }
}
```



**类的修饰符和访问权限**

|            | private | default（同包） | protected | public |
| ---------- | ------- | --------------- | --------- | ------ |
| 同一个类中 | √       | √               | √         | √      |
| 同一个包中 |         | √               | √         | √      |
| 子类中     |         |                 | √         | √      |
| 全局范围内 |         |                 |           | √      |

**访问控制权限的排序：public>protected>default>private**

（ 1 ）对于外部类而言，它也可以使用访问控制符修饰，但外部类只能有两种访问控制级别： public 和默认。因为外部类没有处于任何类的内部，也就没有其所在类的内部、所在类的子类两个范围，因此 private 和 protected 访问控制符对外部类没有意义。

（ 2 ）内部类的上一级程序单元是外部类，它具有 4 个作用域：同一个类（ private ）、同一个包（ protected ）和任何位置（ public ）。

（ 3 ） 因为局部成员的作用域是所在方法，其他程序单元永远不可能访问另一个方法中的局部变量，所以所有的局部成员都不能使用访问控制修饰符修饰，但可以使用final修饰。

```
1、抽象类：
JDK1.8之前，默认访问权限protected;JDK1.8时，默认访问权限是default
接口：
JDK1.8之前，接口中的方法必须是public;
JDK1.8,接口的方法是public或者default；
JDK1.9，接口可以是private
2、public的接口下面，我们想修饰一个变量，可以使用的修饰符时public，default，static，final
3、抽象类和接口的区别：
/*
1、抽象类中可以有构造方法（函数）
2、抽象类中可以有普通属性、方法、静态属性和方法
3、抽象类中可以有抽象方法（抽象方法所在的类一定是抽象类，但是抽象类中不一定有抽象方法）
4、抽象类中的抽象方法，需要有子类实现，如果子类不实现，则子类也需要定义为抽象的。
5、抽象类中可以有静态代码块
6、抽象类中的方法可以有方法体
* */
/*
1、接口中不能有构造方法（函数）
2、接口中有常量、普通方法（不能有方法体,且被public、default修饰）、静态方法（有方法体）
3、接口中不能有静态代码块
* */
4、JDK1.8,修饰interface只能是public,不能private,protected,final,static
```



![image-20220423221646968](C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220423221646968.png)

## 线程和进程

```
线程的6种不同的状态：初始、运行、阻塞、等待、超时、终止。
```

### 线程实现

### 线程同步

## 1.关键字

### volatile

```
1.禁止了指令重排（指令重排：处理器为了提高程序运行效率，可能会对输入代码进行优化，它不保证程序中各个语句的执行先后顺序同代码中的顺序一致，但是它会保证程序最终执行结果和代码顺序执行的结果是一致的-----两个语句如果没有数据依赖的关系，谁先执行都差不多，所以可能出现指令重排）
2.保证了不同线程对这个变量进行操作时的可见性，即一个线程修改了某个变量值，这个新值对其他线程是立即可见的。
3.不保证原子性（线程不安全）【记住啊啊啊啊啊啊啊啊】
4.volatile保证有序性，可见性
```

### synchronized

```
1、synchronized保证三大性，原子性，有序性，可见性。【记住啊啊啊啊啊啊】
2、synchronized可以修饰方法、代码块或对象   并不修饰变量。
```

哪种JAVA的变量声明方式可以避免程序在多线程竞争情况下读到不正确的值(volatile，static volatile )

程序在多线程竞争情况下读到不正确的值需要保证内存可见性，即当一个线程修改了volatile修饰的变量的值，volatile会保证新值立即同步到主内存，以及每次使用前立即从主内存读取。

synchronized可以修饰方法、代码块或对象，并不修饰变量；

static修饰的变量可见性是无法确保的，因此无法保证多线程情况下的安全性。

### 基本数据类型

**6 1 1**

6种数字类型（4种整数型+2种浮点型）

- 整数类型：byte/short/int【默认整数类型】/long
- 浮点型：float/double【默认浮点型】

1种字符类型:char

1种布尔类型：boolean

不同数据类型怎么写的？

| 基本类型  | 位数 | 字节 | 默认值  | 取值范围                                   |
| --------- | ---- | ---- | ------- | ------------------------------------------ |
| `byte`    | 8    | 1    | 0       | -128 ~ 127                                 |
| `short`   | 16   | 2    | 0       | -32768 ~ 32767                             |
| `int`     | 32   | 4    | 0       | -2147483648 ~ 2147483647                   |
| `long`    | 64   | 8    | 0L      | -9223372036854775808 ~ 9223372036854775807 |
| `char`    | 16   | 2    | 'u0000' | 0 ~ 65535                                  |
| `float`   | 32   | 4    | 0f      | 1.4E-45 ~ 3.4028235E38                     |
| `double`  | 64   | 8    | 0d      | 4.9E-324 ~ 1.7976931348623157E308          |
| `boolean` | 1    |      | false   | true、false                                |

```java
public static void main(String[] args) {
        int a = 42;
        double b = 42.0;
        long x = 42;
        float y = 42.f;
        System.out.println(x == y);//true
        System.out.println(a == b);//true
    }
```

除了double不能转为float外，其余int,short,long,byte都可以转为float

### 数据类型和他们的存储位置（极容易混淆）

基本数据类型

- 局部变量---java虚拟机栈的局部变量表中
- 成员变量
  1. 被static修饰（跟着类的）--栈内存当中
  2.  未被static修饰（属于实例）--JVM堆中

```
People people = new People();//new People()在堆上创建了一个对象实例；People people声明了一个People类的引用指向该对象实例，（引用存放于栈内存中）。
```

### 类、接口

**1、接口和抽象类有什么共同点和区别**

共同点：1、都不可以被实例化   2、里面可以包含抽象的方法  3、都可以有默认的实现方式

区别：

1、成员的区别：

**抽象类**

构造方法：有构造方法

成员变量：可以是变量，也可以是常量

成员方法：可以是抽象，也可以是非抽象的

静态代码块：可以有

**接口**

构造方法：无构造方法

成员变量：只能是常量，默认被public static final修饰

成员方法：要分jdk的版本来看，jdk1.7只能是抽象的，默认是public abstract的，jdk1.8可以写以default和static的。

静态代码块：不能有

2、类和接口的关系区别

抽象类：类与类只能单继承，可以多层继承

接口与接口：可以单继承和多继承

**2、java中的内部类**

![img](https://uploadfiles.nowcoder.com/images/20190109/242025553_1547012774538_BA9669C5826A238ACEC0BD86755FA5DB)

类的访问权限

```
1、外部类前可以修饰：public、default、abstract、final

2、内部类前可以修饰：public、protected、default、private、abstract、final、static

3、局部内部类前可以修饰：abstract、final

4、匿名内部类不能有访问修饰符和static，匿名内部类是唯一没有构造器的类

其中：访问修饰符（public、protected、default、private），其他都是非访问修饰符
```



## 2.servlet的生命周期(初始化、请求处理、销毁)

![image-20220615151913915](C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220615151913915.png)

```
Servlet的生命周期一般可以用三个方法来表示：
init()：仅执行一次，负责在装载Servlet时初始化Servlet对象
service() ：核心方法，一般HttpServlet中会有get,post两种处理方式。在调用doGet和doPost方法时会构造servletRequest和servletResponse请求和响应对象作为参数。
destory()：在停止并且卸载Servlet时执行，负责释放资源

Servlet的生命周期
1.加载：容器通过类加载器使用Servlet类对应的文件来加载Servlet
2.创建：通过调用Servlet的构造函数来创建一个Servlet实例
3.初始化：通过调用Servlet的init()方法来完成初始化工作，这个方法是在Servlet已经被创建，但在向客户端提供服务之前调用。
4.处理客户请求：Servlet创建后就可以处理请求，当有新的客户端请求时，Web容器都会创建一个新的线程来处理该请求。接着调用Servlet的
Service()方法来响应客户端请求（Service方***根据请求的method属性来调用doGet（）和doPost（））
5.卸载：容器在卸载Servlet之前需要调用destroy()方法，让Servlet释放其占用的资源。
```

## 3.声明数组的方式的正确形式

```java
int[][] ints1 = new int[6][6];
int[][] ints2 = new int[6][];//第一个有是对的，让他一泻千里把
int ints3[][] = new int[6][6];
int[] ints4[] = new int[6][6];
```

## 4.身份证号的正则表达式

```java
isIDCard=/^[1-9]\d{7}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{3}$/;
isIDCard=/^[1-9]\d{5}[1-9]\d{3}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{4}$/;
```

## 5.数据类型、装箱、拆箱

Byte/Short/Integer/Long都设有包装类缓存机制，范围是【-128，127】

两种浮点数类型的包装类 `Float`,`Double` 并没有实现缓存机制。

**首先结论：**

**（1）int与Integer、new Integer()进行==比较时，结果永远为true**

**（2）Integer与new Integer()进行==比较时，结果永远为false**

**（3）Integer与Integer进行==比较时，看范围；在大于等于-128小于等于127的范围内为true，在此范围外为false。**因此，对于Integer的比较推荐使用equals

（4）new Integer和new Integer相比较，

```java
public static void main(String[] args) {
        Integer a = 10;
        Integer b = new Integer(10);
        System.out.println(a == b);//false
    }
```

**（4）不同封装类之间**

```java
```



## 6.java异常[重点]

### 1.java异常层次图

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220705212621322.png" alt="image-20220705212621322" style="zoom: 67%;" />

![img](http://uploadfiles.nowcoder.com/images/20151113/140047_1447376765880_373DC390B08E99ABC340DB1F78F35FCB)

**Exception和Error的区别：**

在java中，所有的异常都有共同的祖先，`Throwable`.其下面有两个重要的子类：Exception和Error

Exception:程序本身可以处理的异常，可以通过catch进行捕获。可分为Checked Exception和Unchecked Exception.

Error:程序本身无法处理的异常，并不建议通过catch进行捕获。

**Checked Exception和 Unchecked Exception的区别**：

Checked Exception在编译的时候如果没有抛出或者捕获，程序是无法运行的。（IOException,FileNotFoundException,SQLException)

Unchecked Exception（Runntime Exception及其子类) 即使不处理也能够通过编译。（空指针异常、算术溢出异常、数组越界异常、类型转换异常。。。）



<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220724220332739.png" alt="image-20220724220332739" style="zoom:80%;" />

Java的异常分为两种，一种是运行时异常（RuntimeException）也叫Unchecked Exception，一种是非运行异常也叫检查式异常（CheckedException）【编译异常】。

1、运行时异常不需要程序员去处理，当异常出现时，JVM会帮助处理。常见的运行时异常有：

ClassCastException(类转换异常)

ClassNotFoundException

IndexOutOfBoundsException(数组越界异常)

NullPointerException(空指针异常)

ArrayStoreException(数组存储异常，即数组存储类型不一致)

还有IO操作的BufferOverflowException异常

2、非运行异常需要程序员手动去捕获或者抛出异常进行显示的处理，因为Java认为Checked异常都是可以被修复的异常。常见的异常有：

IOException(网址异常，比如访问的网址不存在)

```java
public static void main(String[] args){
        try {
            URL url = new URL("http://www.123.com");
            System.out.println(url);
        } catch (MalformedURLException e) {
            e.printStackTrace();
        }
    }
//输出：http://www.123.com
```



SqlException

**非运行时异常需要我们自己补获，而运行异常是程序运行时由虚拟机帮助我们补获，运行时异常包括数组的溢出，内存的溢出空指针，分母为0等！**



**try--catch--finally**

- try:捕获异常
- catch:处理try中捕获的异常
- finally:无论是否捕获或处理异常， finally块里的语句都会被执行( finally 之前虚拟机被终止运行的话/程序所在的线程死亡/关闭 CPU,finally都不会被执行)



## 7.String  StringBuffer StringBuilder

### 1.三者的比较

String,StringBuffer,StringBuilder都是==final==修饰的，为什么后面两者还是可以改变呢？

不可变包括的是，引用不可变以及对象不可变，而这三个都是属于引用不可变，（也就是**地址不要变，里面的内容随心所欲**），而StringBuilder , StringBuffer 中都包含append方法，可对对象中的内容进行增加。

**可变性**：

String是不可变的；

StringBuffer和StringBuilder都是可变的；

**线程安全性**

`String` 中的对象是不可变的，也就可以理解为常量，线程安全

`StringBuffer` 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的

`StringBuilder` 并没有对方法进行加同步锁，所以是非线程安全的。

总结：

1. 操作少量的数据: 适用 `String`
2. 单线程操作字符串缓冲区下操作大量数据: 适用 `StringBuilder`
3. 多线程操作字符串缓冲区下操作大量数据: 适用 `StringBuffer`
3. StringBuffer是线程安全的，而StringBuilder是非线程安全的，所以StringBuilder性能略高。一般情况下，要创建一个内容可变的字符串，建议优先考虑StringBuilder类。

### 2.String为啥不可变

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
    /** The value is used for character storage. */
    private final char value[];
}
```

原因有二：

1. 保存字符串的数组被 `final` 修饰且为私有的，并且`String` 类没有提供/暴露修改这个字符串的方法。 

   `private final char[] value` / `private final byte[] value`

2. `String` 类被 `final` 修饰导致其不能被继承，进而避免了子类破坏 `String` 不可变。

### 3.String中的各种

#### 3.1 String.intern()

`String.intern()` 是一个 native（本地）方法，其作用是将指定的字符串对象的引用保存在字符串常量池中，可以简单分为两种情况：

- 如果字符串常量池中保存了对应的字符串对象的引用，就直接返回该引用。
- 如果字符串常量池中没有保存了对应的字符串对象的引用，那就在常量池中创建一个指向该字符串对象的引用并返回。

```java
public static void main(String[] args) {
        // 在堆中创建字符串对象”Java“
// 将字符串对象”Java“的引用保存在字符串常量池中
        String s1 = "Java";
// 直接返回字符串常量池中字符串对象”Java“对应的引用
        String s2 = s1.intern();
// 会在堆中在单独创建一个字符串对象
        String s3 = new String("Java");
// 直接返回字符串常量池中字符串对象”Java“对应的引用
        String s4 = s3.intern();
// s1 和 s2 指向的是堆中的同一个对象
        System.out.println(s1 == s2); // true
        System.out.println(s1 == s3);//false
// s3 和 s4 指向的是堆中不同的对象
        System.out.println(s3 == s4); // false
// s1 和 s4 指向的是堆中的同一个对象
        System.out.println(s1 == s4); //true
        System.out.println(s2 == s4); //true
    }
```

#### 3.2 String.equals（）和  ==

```java
正常情况下，我们相比较字符串中的值是否相等，应该使用equals方法，这个是已经重写过的。所以下面的代码没有问题
        String str1 = "str";
        String str2 = "ing";
        String str3 = "str" + "ing";
        String str4 = str1 + str2;
        String str5 = "string";
        System.out.println(str3.equals(str4));//true
        System.out.println(str3.equals(str5));//true
        System.out.println(str4.equals(str5));//true
		String s="welcome"+"to"+360; // 这句话创建1个对象【重要】
```

```java
==比较的是地址是否相等
    String str1 = "str";
    String str2 = "ing";
    String str3 = "str" + "ing";
    String str4 = str1 + str2;
    String str5 = "string";
    System.out.println(str3 == str4);//false
    System.out.println(str3 == str5);//true
    System.out.println(str4 == str5);//false

	String s = new String("hello");
    System.out.println(s == "hello");//false
```

#### 3.3 String的拼接  +

```
看了+的底层可以知道，对象引用和“+”的字符串拼接方式实际上是通过 StringBuilder 调用 append() 方法实现的，拼接完成之后调用 toString() 得到一个 String 对象 。
```

**对于编译期可以确定值的字符串，也就是常量字符串 ，jvm 会将其存入字符串常量池。并且，字符串常量拼接得到的字符串常量在编译阶段就已经被存放字符串常量池，这个得益于编译器的优化**

并不是所有的常量都会进行折叠，只有编译器在程序编译期就可以确定值的常量才可以：

- 基本数据类型( `byte`、`boolean`、`short`、`char`、`int`、`float`、`long`、`double`)以及字符串常量。
- `final` 修饰的基本数据类型和字符串变量
- 字符串通过 “+”拼接得到的字符串、基本数据类型之间算数运算（加减乘除）、基本数据类型的位运算（<<、>>、>>> ）

**引用的值在程序编译期是无法确定的，编译器无法对其进行优化。**

## 8.JVM

JVM是运行在操作系统之上的，不和硬件进行交互。

```
-Xmx10240m -Xms10240m -Xmn5120m -XXSurvivorRatio=3
```

-Xmx：最大堆大小

-Xms：初始堆大小

-Xmn:年轻代大小

-XXSurvivorRatio：年轻代中Eden区与Survivor区的大小比值

年轻代5120m， Eden：Survivor=3，Survivor区大小=1024m（Survivor区有两个，即将年轻代分为5份，每个Survivor区占一份），总大小为2048m。

-Xms初始堆大小即最小内存值为10240m



假如某个JAVA进程的JVM参数配置如下：
-Xms1G -Xmx2G -Xmn500M -XX:MaxPermSize=64M -XX:+UseConcMarkSweepGC -XX:SurvivorRatio=3,
请问eden区最终分配的大小是多少？ **100M**

先分析一下里面各个参数的含义： 
-Xms：1G ， 就是说初始堆大小为1G 
-Xmx：2G ， 就是说最大堆大小为2G 
-Xmn：500M ，就是说年轻代大小是500M（包括一个Eden和两个Survivor） 
-XX:MaxPermSize：64M ， 就是说设置持久代最大值为64M 
-XX:+UseConcMarkSweepGC ， 就是说使用使用CMS内存收集算法 
-XX:SurvivorRatio=3 ， 就是说Eden区与Survivor区的大小比值为3：1：1
题目中所问的Eden区的大小是指年轻代的大小，直接根据-Xmn：500M和-XX:SurvivorRatio=3可以直接计算得出
500M*(3/(3+1+1)) 
=500M*（3/5） 
=500M*0.6 
=300M 
所以Eden区域的大小为300M。

### 1.jvm的类加载机制（类加载过程）

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220620201631755.png" alt="image-20220620201631755" style="zoom:67%;" />

类加载的过程：（来自书）加载--验证--准备--解析--初始化

**初始化做什么工作的？**

初始化阶段是执行初始化方法 `<clinit> ()`方法的过程，是类加载的最后一步，这一步 JVM 才开始真正执行类中定义的 Java 程序代码(字节码)。

### 2.JVM垃圾回收--JVM如何判断一个对象是否可以被回收（一个对象是否死亡？）

```
在JVM中，判断一个对象是否可以被回收，就看这个对象是否还在被使用，只有没有被使用的对象才能被回收。
1.引用计数器。为每个对象添加一个引用计数器，用来统计当前对象的引用次数，如果当前对象存在应用的更新，那么就对这个计数器进行增加。一旦这个计数器变成0，意味着可以被回收。但是这种需要额外的空间来存储引用计数器，实现简单、效率高。但是主流的JVM都没有使用这种方式，因为引用计数器在处理一些复杂的循环引用的时候，会出现一些不再使用但是又无法回收的内存，造成内存的泄漏。
2.可达性分析。他的主要思想是，首先确定一系列肯定不能回收的对象作为GC root,比如虚拟机栈里面的引用对象，本地方法栈引用对象等。然后以GC root作为起始节点，从这些节点开始向下搜索，去寻找它直接和间接引用的对象，当遍历完之后如果发现一些对象不可达，认为这些对象没有用了，需要被回收。在垃圾回收的时候，JVM首先找到所有的GC root，这个过程暂停所有的用户线程，也就是stop the world，然后再从GC root中向下搜索，可达对象保留，不可达的对象回收。【主流的JVM使用算法】

java中的垃圾回收机制并不是在程序结束的时候进行GC，GC的时间是不确定的，且GC的过程需要经过可达性分析，一个对象只有被标记2次才会被GC。
```

### 3.JVM垃圾回收--引用

强引用、软引用、弱引用、虚引用（引用强度减弱）

**强引用**：如果一个对象具有强引用，那就类似于**必不可少的生活用品**，垃圾回收器绝不会回收它。当内存空间不足，Java 虚拟机宁愿抛出 OutOfMemoryError 错误，使程序异常终止，也不会靠随意回收具有强引用的对象来解决内存不足问题。

**软引用**：类似于**可有可无的生活用品**，内存空间足够，垃圾回收器就不会回收它，如果内存空间不足了，就会回收这些对象的内存。只要垃圾回收器没有回收它，该对象就可以被程序使用。软引用可用来实现内存敏感的高速缓存。

**弱引用**：类似于**可有可无的生活用品**。弱引用与软引用的区别在于：只具有弱引用的对象拥有更短暂的生命周期。一旦发现了只具有弱引用的对象，不管当前内存空间足够与否，都会回收它的内存。

**虚引用**：**虚引用主要用来跟踪对象被垃圾回收的活动**。

### 3.JVM垃圾回收--JVM垃圾回收机制或算法

```
1.标记-清除法，首先标记出所有不需要回收的对象（所有存活的对象），在标记完之后统一回收所有没有被标记的对象。该算法的明显问题，效率问题；空间问题（标记清楚之后回产生大量不连续的碎片）
```

![image-20220617163954093](C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220617163954093.png)

```
2.标记-复制法。将内存分为大小相等的两块，每次使用其中的一块。当这一块的内存使用完成之后，就将还存活的对象复制到另一块去，再把使用过的空间一次性清除掉。
```

![image-20220617164212513](C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220617164212513.png)

```
3.标记-整理法 标记的过程和“标记-清除”是一样的，但是后续步骤不是对可回收的对象回收，而是让所有存活的对象向一端移动，然后直接清理掉边界之外的内存。
```

![image-20220617164506541](C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220617164506541.png)

```
4.分代收集法  当前虚拟机采用分代收集算法，这种算法根据对象存活周期不同分为几块。一般将java堆分为新生代和老生代，根据各个年代的特点选择合适的垃圾收集算法。
比如在新生代中，每次收集都会有大量对象死去，所以可以选择”标记-复制“算法，只需要付出少量对象的复制成本就可以完成每次垃圾收集。
而老年代的对象存活几率是比较高的，而且没有额外的空间对它进行分配担保，所以我们必须选择“标记-清除”或“标记-整理”算法进行垃圾收集。
```

**新生代**---**标记复制**

**老生代---标记清除、标记整理**



### 3.JVM垃圾回收--垃圾收集器

常见的垃圾回收器（详细介绍一下CMS和G1收集器）

**如果说收集算法是内存回收的方法论，那么垃圾收集器就是内存回收的具体实现。**

**Serial 收集器**：最基本、历史最悠久的单线程垃圾收集器。它只会使用一条垃圾收集线程去完成垃圾收集工作，更重要的是它在进行垃圾收集工作的时候必须暂停其他所有的工作线程（ **"Stop The World"** ），直到它收集结束。新生代（标记-复制）；老生代（标记-整理）

**ParNew 收集器**：**Serial 收集器**的多线程版本。除了使用多线程进行垃圾收集外，其余行为和**Serial 收集器**一样。新生代（标记-复制）；老生代（标记-整理）

**CMS收集器**：**一种以获取最短回收停顿时间为目标的收集器。它非常符合在注重用户体验的应用上使用。HotSpot 虚拟机第一款真正意义上的并发收集器，它第一次实现了让垃圾收集线程与用户线程（基本上）同时工作。**采用==标记-清除==算法。总共分为4个步骤：

- 初始标记： 暂停所有的其他线程，并记录下直接与 root 相连的对象。
- 并发标记：同时开启 GC 和用户线程，用一个闭包结构去记录可达对象，但闭包结构不会保证当前所有的可达对象。
- 重新标记：重新标记阶段就是为了修正并发标记期间因为用户程序继续运行而导致标记产生变动的那一部分对象的标记记录，该阶段的停顿时间比初始标记长，但远低并发标记的时间。
- 并发清除：开启用户线程，同时 GC 线程开始对未标记的区域做清扫。

**G1 (Garbage-First) 是一款面向服务器的垃圾收集器,主要针对配备多颗处理器及大容量内存的机器. 以极高概率满足 GC 停顿时间要求的同时,还具备高吞吐量性能特征**



### 4.JVM运行时的数据区域

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220706174155255.png" alt="image-20220706174155255" style="zoom: 50%;" />

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220706174216518.png" alt="image-20220706174216518" style="zoom:50%;" />

分为JDK 1.8之前  和   JDK1.8

==JDK1.8之前==  

线程共享--堆，方法区（运行时常量池）、直接内存（非运行时数据区一部分）

线程私有--虚拟机栈、本地方法栈、程序计数器

==JDK1.8==

线程共享--堆，方法区和直接内存（非运行时数据区一部分）【把方法区变成了元空间，然后和直接内存放在一起称 **本地内存**】

线程私有--虚拟机栈、本地方法栈、程序计数器

#### 线程私有-虚拟机栈

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220619173607726.png" alt="image-20220619173607726" style="zoom: 50%;" />

方法调用的数据需要通过栈来传递，方法调用时对应的栈帧被压入栈，方法调用结束栈帧被弹出。

栈由一个个的栈帧组成，每个栈帧包括局部变量表、操作数栈、动态链接、方法返回地址

**局部变量表**：编译期可知的各种数据类型、对象引用类型  

**操作数栈**：存放方法执行过程中产生的中间计算结果，临时变量

**动态链接**：将符号引用,转换为调用方法的直接引用。适用于一个方法调用另一个方法的场景，当源代码被编译成字节码时，所有的变量和引用都保存在常量池，当一个方法想要调用其他方法，需要将常量池中的引用转化成其在内存地址中的直接引用。

```
程序运行中栈可能会出现两种错误：
StackOverFlowError： 若栈的内存大小不允许动态扩展，那么当线程请求栈的深度超过当前 Java 虚拟机栈的最大深度的时候，就抛出 StackOverFlowError 错误。
OutOfMemoryError： 如果栈的内存大小可以动态扩展， 如果虚拟机在动态扩展栈时无法申请到足够的内存空间，则抛出OutOfMemoryError异常。
```

#### 线程私有-本地方法栈

跟上面的虚拟机栈类似，在本地方法栈会创建一个栈帧，用于存放本地方法的局部变量表、操作数栈、动态链接、出口信息。同样会有StackOverFlowError和OutOfMemoryError错误

区别是**虚拟机栈为虚拟机执行 Java 方法 （也就是字节码）服务，而本地方法栈则为虚拟机使用到的 Native 方法服务**

#### 线程私有-程序计数器

- 通过改变程序计数器来依次读取指令，实现代码的流程控制，顺序、选择、循环等。
- 多线程的情况下，用于记录当前线程执行的位置，当线程来回切换时知道该线程上次执行到哪里了。

程序计数器是唯一一个不会出现 `OutOfMemoryError` 的内存区域，它的生命周期随着线程的创建而创建，随着线程的结束而死亡。

#### 线程共享-堆

JVM管理的内存中最大的一块，**此内存区域的唯一目的就是存放对象实例，几乎所有的对象实例以及数组都在这里分配内存。**

但是因JIT编译器与逃逸分析技术的逐渐成熟，所有对象都分配到堆上也渐渐变得不那么绝对了。

Java 堆是垃圾收集器管理的主要区域，因此也被称作 **GC 堆（Garbage Collected Heap）**。从垃圾回收的角度，由于现在收集器基本都采用分代垃圾收集算法，所以 Java 堆还可以细分为：新生代和老年代。



在 JDK 7 版本及 JDK 7 版本之前，堆内存被通常分为下面三部分：

1. 新生代内存(Young Generation)
2. 老生代(Old Generation)
3. 永久代(Permanent Generation)

**JDK 8 版本之后 PermGen(永久) 已被 Metaspace(元空间) 取代，元空间使用的是直接内存**

堆这里最容易出现的就是 `OutOfMemoryError` 错误

在Java中，堆是JVM管理的最大的一块内存区域，被划分成新生代、老年代。新生代又被划分成三个区域：Eden、From survivor,to survivor.

#### 线程共享-方法区

在不同的虚拟机实现上，方法区的实现是不同的。方法区会存储已被虚拟机加载的 **类信息、字段信息、方法信息、常量、静态变量、即时编译器编译后的代码缓存等数据**。

**方法区和永久代以及元空间是什么关系呢？**---方法区和永久代以及元空间的关系很像Java中接口和类的关系，类实现了接口。这里的类指：永久代和元空间，接口指：方法区。永久代以及元空间是方法区的两种实现方式。永久代是 JDK 1.8 之前的方法区实现，JDK 1.8 及以后方法区的实现变成了元空间。

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220619213652729.png" alt="image-20220619213652729" style="zoom:50%;" />

**为什么要将永久代 (PermGen) 替换为元空间 (MetaSpace) 呢?**--

1.使用元空间溢出的概率比原来小。永久代有JVM本身设置的固定大小的上限，无法进行调整，元空间使用的是直接内存。

2.使用元空间加载的类更多。元空间里面存放的是类的元数据，加载多少类的元数据由系统实际可用的空间来控制。

3.在JDK8，合并hotSpot和JRockit 的代码时, 后者从来没有一个叫永久代的东西, 合并之后就没有必要额外的设置这么一个永久代的地方了。



**运行时常量池**【方法区】

运行时常量池是方法区的一部分，常量池表会在类加载后存放到方法区的运行时常量池中。常量池包括各种字面量（整数、浮点数和字符串字面量）和符号引用（类符号引用、字段符号引用、方法符号引用和接口方法符号引用）。

**字符串常量池**【堆】

**字符串常量池** 是 JVM 为了提升性能和减少内存消耗针对字符串（String 类）专门开辟的一块区域，主要目的是为了避免字符串的重复创建

```
// 在堆中创建字符串对象”ab“
// 将字符串对象”ab“的引用保存在字符串常量池中
String aa = "ab";
// 直接返回字符串常量池中字符串对象”ab“的引用
String bb = "ab";
System.out.println(aa==bb);// true
```

JDK1.7 之前，字符串常量池存放在永久代。JDK1.7 字符串常量池和静态变量从永久代移动了 Java 堆中。

==注意：JVM运行时常量池中存放的是引用，实际的对象保存在堆上。==

```java
对象和引用的区别：
People people = new People();
上述语句创建了一个People对象。右边的new People()即新建对象本身；左边的People people创建了一个People类的引用变量；=操作符使得对象引用指向刚刚的对象。
```

#### 直接内存

这部分内存被频繁地使用，而且也可能导致 `OutOfMemoryError `错误出现。

#### 对象的创建（重点）

**Step1:类加载检查**：虚拟机遇到一条 new 指令时，首先将去检查这个指令的参数是否能在常量池中定位到这个类的符号引用，并且检查这个符号引用代表的类是否已被加载过、解析和初始化过。如果没有，那必须先执行相应的类加载过程。

**Step2:分配内存**：在**类加载检查**通过后，接下来虚拟机将为新生对象**分配内存**。对象分配空间的任务等同于把一块确定大小的内存从 Java 堆中划分出来。**分配方式**有 **“指针碰撞”** 和 **“空闲列表”** 两种，**选择哪种分配方式由Java堆采用的垃圾收集器是否带有压缩整理功能决定**，指针碰撞适用堆规整的情况，空闲列表适用于不规整的堆的情况。

**Step3:初始化零值**: 内存分配完成后，虚拟机需要将分配到的内存空间都初始化为零值（不包括对象头），这一步操作保证了对象的实例字段在 Java 代码中可以不赋初始值就直接使用，程序能访问到这些字段的数据类型所对应的零值。

**Step4:设置对象头**：初始化零值完成之后，**虚拟机要对对象进行必要的设置**，例如这个对象是哪个类的实例、如何才能找到类的元数据信息、对象的哈希码、对象的 GC 分代年龄等信息。 **这些信息存放在对象头中。** 

**Step5:执行 init 方法**：执行 new 指令之后会接着执行 `<init>` 方法，把对象按照程序员的意愿进行初始化，这样一个真正可用的对象才算完全产生出来。

**对象访问定位的两种方式**：句柄和直接指针两种方式。

句柄：使用句柄，java堆会单独划分一块内存作为句柄池，对象引用中存储的是对象的句柄地址，而句柄中包含了对象实例数据与类型数据各自的具体地址信息。

直接指针：如果使用直接指针访问，那么 Java 堆对象的布局中就必须考虑如何放置访问类型数据的相关信息，而 reference 中存储的直接就是对象的地址。

### 5.类加载过程

**类的生命周期**

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220620115438413.png" alt="image-20220620115438413" style="zoom:50%;" />

Class 文件需要加载到虚拟机中之后才能运行和使用，虚拟机加载这些Class文件主要分三步：**加载-->连接-->初始化**，连接又分为三步：

**验证-->准备-->解析**

#### 加载

类加载过程的第一步，主要完成下面 3 件事情：

1. 通过全类名获取定义此类的二进制字节流；
2. 将字节流所代表的静态存储结构转换为方法区的运行时数据结构；
3. 在内存中生成一个代表该类的 `Class` 对象，作为方法区这些数据的访问入口；

#### 验证

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220620120054706.png" alt="image-20220620120054706" style="zoom: 80%;" />

#### 准备

准备阶段是正式为类变量分配内存并设置类变量初始值的阶段。

#### 解析

解析阶段是虚拟机将常量池内的符号引用替换为直接引用的过程。

#### 初始化

初始化阶段是执行初始化方法 `<clinit> ()`方法的过程，是类加载的最后一步，这一步 JVM 才开始真正执行类中定义的 Java 程序代码(字节码)。

#### 卸载

卸载类即该类的 Class 对象被 GC。

卸载类需要满足 3 个要求:

1. 该类的所有的实例对象都已被 GC，也就是说堆不存在该类的实例对象。
2. 该类没有在其他任何地方被引用
3. 该类的类加载器的实例已被 GC



## 9.反射机制

### 1.什么是反射机制，它有什么用？

通过java的反射机制可以操作字节码文件。通过反射机制可以操作代码片段。

反射机制相关的类在`java.lang.reflect.*`

反射中的重要的类有`java.lang.Class`，(代表整个类)`java.lang.reflect.Method`（代表类中的方法）,`java.lang.reflect.Field`（代表类中的属性）,`java.lang.reflect.Constructor`（代表类中的构造方法）

### 2.获取Class的三种方式

`Class.forName（完整类名带包名）`

`对象.getClass()`

`类.class`

```java
public static void main(String[] args) {
        Class a = null;
        try {
            a = Class.forName("java.lang.String");
            System.out.println(a);//class java.lang.String
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        String s = "abc";
        Class b = s.getClass();
        System.out.println(a == b);//true
    
     	Class c = String.class;
        System.out.println(b == c);//true
    }
```

解析：JVM中的方法区中仅仅包含一份字节码文件，也就是说字节码文件装载到JVM中的时候，只装载一份。

## 10.序列化和反序列化

**序列化**：将数据结构或者对象转化成二进制字节流的过程

**反序列化**：将在序列化过程中生成的二进制字节流转化成数据结构或者对象的过程

**序列化的主要目的是通过网络传输对象或者说是将对象存储到文件系统、数据库、内存中**



### 实际开发场景中的序列化和反序列化

1. 对象在进行网络传输（比如远程方法调用 RPC 的时候）之前需要先被序列化，接收到序列化的对象之后需要再进行反序列化；
2. 将对象存储到文件中的时候需要进行序列化，将对象从文件中读取出来需要进行反序列化。
3. 将对象存储到缓存数据库（如 Redis）时需要用到序列化，将对象从缓存数据库中读取出来需要反序列化。



序列化协议位于TCP/IP 4层模型中的==应用层==

## 11.代理模式

**我们使用代理对象来代替对真实对象(real object)的访问，这样就可以在不修改原目标对象的前提下，提供额外的功能操作，扩展目标对象的功能**

代理模式的作用是扩展目标对象的功能，在目标对象某个方法的执行前后增加自定义的操作。

### 静态代理

对目标对象的每个方法的增强都是手动完成的，非常不灵活（比如接口一旦新增加方法，目标对象和代理对象都要进行修改）且麻烦(需要对每个目标类都单独写一个代理类)

### 动态代理

- 动态代理和静态代理的角色一样

- 动态代理的代理类是动态生成的，不是我们直接写好的

- 动态代理分为两大类：基于接口的动态代理，基于类的动态代理

  基于接口--JDK动态代理

  基于类--cglib

==从JVM的角度，动态代理是在运行时动态生成类字节码，并加载到JVM中的==

#### JDK动态代理

1. 定义一个接口及其实现类；
2. 自定义 `InvocationHandler` 并重写`invoke`方法，在 `invoke` 方法中我们会调用原生方法（被代理类的方法）并自定义一些处理逻辑；
3. 通过 `Proxy.newProxyInstance(ClassLoader loader,Class<?>[] interfaces,InvocationHandler h)` 方法创建代理对象；

## 12.集合

### 1.集合概述

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220622155852712.png" alt="image-20220622155852712" style="zoom:80%;" />

![image-20220622155914501](C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220622155914501.png)

```
一个是 Collection接口，主要用于存放单一元素；另一个是 Map 接口，主要用于存放键值对。

先插的位置在前，后插的位置在后，则为有序，反之无序。

实现了List接口的集合类全部有序，如ArrayList、LinkedList
实现了Set接口的集合类中，HashSet无序，TreeSet排序
实现了Map接口的集合类中，HashMap无序，TreeMap排序

HashMap、 HashSet、 HashTable 等 基于哈希存储方式的集合是无序的。其它的集合都是有序的。

而TreeMap TreeSet 等集合是排序的。

List：有序可重复
Set:无序不可重复
Queue:有序可重复
Map:键值对存储，key无序不可重复

java中集合有4大类，分别是Set,List,Queue,Map。
前面三个都继承Collection接口。
java提供了众多集合实现类，包括HashSet,TreeSet,ArrayList,LinkedList等等。上面的这些集合都位于java.util.*包下，大都是非线程安全。虽然非线程安全,但性能比较好，且可以利用Collections工具类里面的synchronizedXxx()方法包装成线程安全的集合类。 java.util包下的集合类中,也有少数的线程安全的集合类,例如Vector、Hashtable,它们都是非常古老的API。虽然它们是线程安全的,但是性能很差,已经不推荐使用了。
从JDK 1.5开始,并发包下新增了大量高效的并发的容器,这些容器按照实现机制可以分为三类。
第一类是以降低锁粒度来提高并发性能的容器,它们的类名以Concurrent开头,如ConcurrentHashMap。
第二类是采用写时复制技术实现的并发容器,它们的类名以CopyOnWrite开头,如CopyOnWriteArrayList。
第三类是采用Lock实现的阻塞队列,内部创建两个Condition分别用于生产者和消费者的等待,这些类都实现了BlockingQueue接口,如ArrayBlockingQueue。
```

```java
public static void main(String[] args) {
        ArrayList<Integer> res = new ArrayList<>();//有序
        res.add(2);
        res.add(3);
        res.add(1);
        HashSet<Integer> set = new HashSet<>();//无序
        set.add(2);
        set.add(3);
        set.add(1);
        TreeSet<Integer> treeSet = new TreeSet<>();//有序，按照升序排列
        treeSet.add(2);
        treeSet.add(3);
        treeSet.add(1);
        Queue<Integer> queue = new LinkedList<>();//有序
        queue.add(2);
        queue.add(3);
        queue.add(1);
        HashMap<Integer, Integer> map = new HashMap<>();//key是无序的
        map.put(2,2);
        map.put(3,3);
        map.put(1,1);
        System.out.println(res);//[2, 3, 1]
        System.out.println(set);//[1, 2, 3]
        System.out.println(treeSet);//[1, 2, 3]
        System.out.println(queue);//[2, 3, 1]
        System.out.println(map);//{1=1, 2=2, 3=3}
    }
```

### 2.List

- `Arraylist`： `Object[]` 数组
- `Vector`：`Object[]` 数组
- `LinkedList`： 双向链表

**ArrayList**  **LinkedList**  **Vector**

 java.util包下的集合类中,大部分都是非线程安全的,但也有少数的线程安全的集合类,例如Vector、Hashtable,它们都是非常古老的API。虽然它们是线程安全的,但是性能很差,已经不推荐使用了。

对于这个包下非线程安全的集合,可以利用Collections工具类,该工具类提供的`synchronizedXxx()`方法,可以将这些集合类包装成线程安全的集合类。

- `ArrayList` 是 `List` 的主要实现类，底层使用 `Object[ ]`存储，适用于频繁的查找工作，线程不安全 ；
- `Vector` 是 `List` 的古老实现类，底层使用`Object[ ]` 存储，线程安全。 ==Stack继承Vector，所以线程安全==
- `LinkedList`底层使用的是 **双向链表** 数据结构,线程不安全

**ArrayList**  **LinkedList** 的区别是什么？

1.ArrayList的底层是Object数组，LinkedList是双向链表

2.随机访问一个元素，ArrayList要优于LinkedList,前者时间复杂度O(1)，后者时间复杂度O(N)

3.插入和删除一个元素，LinkedList要优于ArrayList,因为当元素被添加到LinkedList任意位置的时候,不需要像ArrayList那样重新计算大小或者是更新索引。但是增删的场景也不要下意识地认为就是LinkedList.

4.占用内存，LinkedList更占内存，因为除了存储数据还要存储两个引用。

**ArrayList**  的理解包括ArrayList的扩容机制

ArrayList的底层是Object数组，我们可以有三种方式来初始化ArrayList。

第一是无参构造，该数组先被初始化为空数组,之后在首次添加数据时再将其初始化成长度为10的数组。

第二是带初始容量参数的构造函数，通过参数显式的指定数组的容量。

第三是构造包含指定collection元素的列表的构造函数。

如果向ArrayList添加数据会超过数组长度的限制，则会触发自动扩容，再添加数据。扩容就是数组拷贝，将旧数组中的数据拷贝到新数组中，新数组的长度变成原来的1.5倍。ArrayList支持缩容，但不会自动缩容，如果希望缩减ArrayList的容量，则需要调用`trimToSize()`方法

**谈谈CopyOnWriteArrayList的原理**

一个线程安全且读操作无锁的ArrayList。

在写操作时会复制一份新的List，在新的List上完成写操作，然后再将原引用指向新的List。这样就保证了写操作的线程安全。

优点：读操作性能很高，因为无需任何同步措施，比较适用于读多写少的并发场景。

缺点：一是内存占用问题，毕竟每次执行写操作都要将原容器拷贝一份，数据量大时，对内存压力较大，可能会引起频繁GC。

​           二是无法保证实时性

```java
public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(0,0);
        System.out.println(list);
    }
//输出：[0, 1, 2]
//解析：add(index,element)只会将原先index的数字挤到后面去，list的长度是会增加1的。
```



### 3.Set

以下的三个都是set接口的实现类，都不是线程安全的。

- `HashSet`(无序，唯一): 基于 `HashMap` 实现的（哈希表）
- `LinkedHashSet`: `LinkedHashSet` 是 `HashSet` 的子类，并且其内部是通过 `LinkedHashMap` 来实现的。有点类似于我们之前说的 `LinkedHashMap` 其内部是基于 `HashMap` 实现一样，不过还是有一点点区别的（链表+哈希表）
- `TreeSet`(有序，这里的有序指的是顺序，唯一): 红黑树(自平衡的排序二叉树)（红黑树）

Set的无序是指存储的数据在底层数组中并非按照数组索引的顺序添加 ，而是根据数据的哈希值决定的。



**Hashset如何检查重复**

对于要加入的对象，首先会计算这个对象的hashcode,判断这个值与其他对象的hashcode。如果不相同，则认为此前没有加入此对象，否则调用equals方法比较hashcode相等的两个对象是否真的相等。如果相等，不会让其加入成功。

**HashSet的底层数据结构是什么**

HashSet是基于HashMap实现的，默认构造函数是构建一个初始容量为16，负载因子为0.75 的HashMap。

### 4.queue

- `PriorityQueue`: `Object[]` 数组来实现二叉堆
- `ArrayQueue`: `Object[]` 数组 + 双指针

### 5.Map

- `HashMap`(重点）： JDK1.8 之前 `HashMap` 由==数组+链表==组成的，数组是 `HashMap` 的主体，链表则是主要为了解决哈希冲突而存在的（“拉链法”解决冲突）。JDK1.8 以后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以减少搜索时间。
- `LinkedHashMap`： `LinkedHashMap` 继承自 `HashMap`，所以它的底层仍然是基于拉链式散列结构即由数组和链表或红黑树组成。另外，`LinkedHashMap` 在上面结构的基础上，增加了一条双向链表，使得上面的结构可以保持键值对的插入顺序。同时通过对链表进行相应的操作，实现了访问顺序相关逻辑。详细可以查看：[《LinkedHashMap 源码详细分析（JDK1.8）》](https://www.imooc.com/article/22931)
- `Hashtable`： 数组+链表组成的，数组是 `Hashtable` 的主体，链表则是主要为了解决哈希冲突而存在的
- `TreeMap`： 红黑树（自平衡的排序二叉树）

**HashMap**和**Hashtable**的区别：

1.线程安全：`HashMap`非线程安全，`Hashtable`线程安全。`Hashtable` 内部的方法基本都经过`synchronized` 修饰。（如果你要保证线程安全的话就使用 `ConcurrentHashMap` ！）；

2.效率：`HashMap`比`Hashtable`的效率更高

3.`HashMap`可存储null的key和value,`Hashtable`不允许有null的key和value

4.初始容量大小和扩充容量：`Hashtable`默认初始值为11，之后每次扩容变为原来2n+1;`HashMap`默认初始值为16，之后每次扩容变为原来的2倍； 创建时如果给定了容器的初始值，`Hashtable`直接使用给定的大小，`HashMap`会将其扩充为2的幂次方大小

5.底层的数据结构。 JDK1.8 以后的 `HashMap` 在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以减少搜索时间。Hashtable 没有这样的机制。

**HashMap**的底层实现原理：（重点）

在JDK1.8的时候，`HashMap`的底层实现是==数组+链表/红黑树==。当链表长度超过8时，如果数组的长度小于64会首先进行扩容，当大于64的时候，才会将链表变成红黑树。

HashMap是基于哈希算法来确定元素的位置的，当我们向集合中添加元素的时候，它会计算传入的Key的哈希值并利用哈希值取余的方式计算插入的位置。如果元素发生了碰撞，也就是插入的位置有值，则hashMap通过链表将这些元素链接起来。如果链接的长度超过8，并且数组的长度超过64，则会创建红黑树代替链表，提高链表中数据的查找速度。

HashMap中，数组默认的初始容量为16，之后每次扩容变为原来的2倍。具体来说,当数组中的元素达到一定比例的时候HashMap就会扩容,这个比例叫做负载因子,默认为0.75。采用2的指数进行扩容,是为了利用位运算,提高扩容运算的效率。==（HashMap的扩容机制）==

**Hashmap的put的机制**

（下面好拗口，不好记住）

- 判断数组，若数组为空，进行首次扩容；
- 判断头节点，若发现头节点为空，则新建链表节点，存入数组
- 判断头节点，若发现头节点非空，则将元素插入槽内。
  - 若元素的key与头节点一致，则直接覆盖头节点；
  - 若元素为树型节点，则将元素追加到树中；
  - 若元素为链表节点，则将元素追加到链表中。根据链表的长度判断是否将其转化成红黑树。若链表长度为8但是数组长度未达到64，则扩容；否则将链表转成红黑树。
- 插入元素后，判断元素的个数，若超过阈值则再次扩容。

（记住这个）

- 插入元素，如果定位到的数组位置没有元素则直接插入；
- 如果定位到的数组位置有元素，就要和插入的key进行比较，如果相等，就直接覆盖；如果key不等，就判断元素是否是树型节点，若是就直接追加到树中；若元素为链表节点，则将元素追加到链表中。根据链表的长度判断是否将其转化成红黑树。若链表长度为8但是数组长度未达到64，则扩容；否则将链表转成红黑树。
- 插入元素后，判断元素的个数，若超过阈值则再次扩容。

**HashMap底层为什么是红黑树,用B树可以吗？**

红黑树是常用的平衡二叉搜索树，B树/B+树这种数据结构的特点就是比较矮胖，主要用于数据存储在磁盘上的场景，比如数据库底层就是使用这种数据结构，每个节点存放一个磁盘大小的数据，这样一次可以把一个磁盘页大小的数据读入内存，提高效率。

红黑树多用于内存中排序，也就是内部排序。

**HashMap的7种遍历方式**

1. 使用迭代器（Iterator）EntrySet 的方式进行遍历；
2. 使用迭代器（Iterator）KeySet 的方式进行遍历；
3. 使用 For Each EntrySet 的方式进行遍历；
4. 使用 For Each KeySet 的方式进行遍历；
5. 使用 Lambda 表达式的方式进行遍历；
6. 使用 Streams API 单线程的方式进行遍历；
7. 使用 Streams API 多线程的方式进行遍历。

**从以上结果可以看出 `entrySet` 的性能比 `keySet` 的性能高出了一倍之多，因此我们应该尽量使用 `entrySet` 来实现 Map 集合的遍历**。

```java
public static void main(String[] args) {
        // 创建并赋值 HashMap
        Map<Integer, String> map = new HashMap();
        map.put(1, "Java");
        map.put(2, "JDK");
        map.put(3, "Spring Framework");
        map.put(4, "MyBatis framework");
        map.put(5, "Java中文社群");
        // 遍历
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println(entry.getKey());
            System.out.println(entry.getValue());
        }
    }
```

**谈谈对ConcurrentHashMap的理解**

1.ConcurrentHashMap的底层数据结构和HashMap一样，采用数组+链表/红黑树；

2.采用锁定头节点的方式降低锁粒度，以较低的性能实现线程安全，ConcurrentHashMap 使用segment来分段和管理锁，segment继承自ReentrantLock，因此ConcurrentHashMap使用ReentrantLock来保证线程安全；

3.线程安全实现机制：

3.1初始化数组或者头节点，ConcurrentHashMap并没有加锁，而是采用CAS方式进行原子替换；

3.2插入数据时会进行加锁处理，但锁定的不是整个数组而是槽中的头节点；所以,ConcurrentHashMap中锁的粒度是槽,而不是整个数组,并发的性能很好

3.3扩容时会进行加锁处理,锁定的仍然是头节点。并且,支持多个线程同时对数组扩容,提高并发能力；

3.4在扩容的过程中,依然可以支持查找操作；



## 13.并发

### 13.1什么是进程和线程？优缺点和区别

进程是程序的一次执行的过程，是系统运行程序的基本单位。在 Java 中，当我们启动 main 函数时其实就是启动了一个 JVM 的进程，而 main 函数所在的线程就是这个进程中的一个线程，也称主线程。

线程与进程类似，但线程是比进程更小的执行单位。一个进程在执行的过程中可以产生多个线程。在JVM中，不同的线程是共享堆和方法区（JDK1.8之后，方法区的实现是元空间）的，每个线程自己有自己的虚拟机栈、本地方法栈、程序计数器。

二者的区别可从以下几个角度展开：

- 地址空间：进程有独立的地址空间，线程有自己的堆栈和局部变量，但线程没有单独的地址空间；
- 开销：进程线程切换时，需要切换进程和线程的上下文。进程上下文的切换时间开销远远大于线程上下文切换时间；
- 并发性：进程的并发较低，线程的并发性较高；
- 内存空间：系统在运行的时候会为每个进程分配不同的内存空间，对线程来说，除了CPU之外，系统不会为线程分配内存，线程组之间只能共享内存。
- 一个进程崩坏之后，不会对其他进程造成影响，但是一个线程崩溃整个进程死掉。所以多进程要比多线程健壮。

### 13.2并发和并行的区别

- 并发：两个及两个以上的作业在同一时间段内执行；
- 并行：两个及两个以上的作业在同一时刻执行；



### 13.3为什么要使用多线程以及多线程的问题

**为什么使用多线程**：从计算机的底层来说，线程是更加轻量级的进程，线程进行来回切换的时候的开销是比进程要低的；从当前互联网的发展趋势来说，现在动不动就是百万级或者千万级的并发量，多线程并发编程是开发高并发系统的基础。

**多线程带来的问题**：内存泄漏、死锁、线程不安全等

### 13.4线程的生命周期和状态

线程的6种不同的状态：

- 初始（NEW)
- 运行（RUNNABLE）【RUNNING,READY】
- 阻塞（BLOCKED)
- 等待  (WAITING)
- 超时 (TIME_WAITING)
- 终止 (TERMINATED)

线程创建之后就会处于NEW状态，调用start()方法之后开始运行，线程处于READY状态。READY状态获得了CPU时间片后就处于RUNNING状态。

线程执行wait()方法之后，线程进入WAITING状态，并依靠其他线程的通知才能返回到运行状态；

在等待状态的基础上增加超时限制，sleep（long millis）`方法或 `wait（long millis）线程置于TIME_WAITING状态，当超时时间到达之后才能返回到运行状态；

线程调用同步方法的时候，在没有获得锁的情况下，将进入BLOCKED状态。线程在执行 Runnable 的`run()`方法之后将会进入到 TERMINATED（终止）状态。

### 13.5什么是上下文切换

线程在执行过程中会有自己的运行条件和状态（也称上下文），以下情况下，线程会从占用的CPU中退出。

- 主动让出CPU，调用sleep()或者wait()方法【sleep和wait方法有啥区别：最主要的区别在于sleep方法没有释放锁，wait方法释放了锁。两者都可以暂停线程的执行。】
- 时间片用完，操作系统要防止一个线程或者进程长时间占用CPU导致其他线程饿死
- 调用了阻塞类型的系统中断，比如请求IO
- 被终止或结束运行

### 13.6 线程死锁和如何避免死锁

**线程死锁**：两个或两个以上的线程在执行过程中,因争夺共享资源而造成的一种互相等待的现象,若无外力作用,它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁。这些永远在互相等待的进程称为死锁进程。

**产生死锁的四个必要的条件**：

- 互斥条件：该资源任意一个时刻只由一个线程占用。
- 请求与保持条件：一个线程因请求资源而阻塞时，对已获得的资源保持不放。
- 不剥夺条件:线程已获得的资源在未使用完之前不能被其他线程强行剥夺，只有自己使用完毕后才释放资源。
- 循环等待条件:若干线程之间形成一种头尾相接的循环等待资源关系。

**避免死锁**：

- **破坏请求与保持条件** ：一次性申请所有的资源。
- **破坏不剥夺条件** ：占用部分资源的线程进一步申请其他资源时，如果申请不到，可以主动释放它占有的资源。
- **破坏循环等待条件** ：靠按序申请资源来预防。按某一顺序申请资源，释放资源则反序释放。破坏循环等待条件。

**为什么我们调用 start() 方法时会执行 run() 方法，为什么我们不能直接调用 run() 方法？**

new一个Thread，线程进入了新建状态。调用start方法，会启动一个线程并使线程进入就绪状态，当分配时间片的时候，就可以开始运行了。start会执行线程相应的准备工作，然后自动执行run方法的内容，这才是真正的多线程。**调用 `start()` 方法方可启动线程并使线程进入就绪状态，直接执行 `run()` 方法的话不会以多线程的方式执行。**

### 13.7synchronized 关键字

**`synchronized` 关键字解决的是多个线程之间访问资源的同步性，`synchronized`关键字可以保证被它修饰的方法或者代码块在任意时刻只能有一个线程执行。**

### 13.8 volatile关键字

**说说 synchronized 关键字和 volatile 关键字的区别**

`synchronized` 关键字和 `volatile` 关键字是两个互补的存在，而不是对立的存在！

- **`volatile` 关键字**是线程同步的**轻量级实现**，所以 **`volatile `性能肯定比`synchronized`关键字要好** 。但是 **`volatile` 关键字只能用于变量而 `synchronized` 关键字可以修饰方法以及代码块** 。
- **`volatile` 关键字能保证数据的可见性，但不能保证数据的原子性。`synchronized` 关键字两者都能保证。**
- **`volatile`关键字主要用于解决变量在多个线程之间的可见性，而 `synchronized` 关键字解决的是多个线程之间访问资源的同步性。**

### 13.9 创建线程的两种方式

创建线程的方式其实有3种：Thread,Runnable,Callable

**1、从java.lang.Thread类派生一个新的线程类（继承Thread类）；重写它的run()方法，编写线程执行体；创建线程对象，调用start()方法启动线程**

```java
public class Solution_02{
    public static void main(String[] args) {
        Thread thread = new Mythread();
        thread.start();

        for (int i = 0; i < 10; i++) {
            System.out.println("我是main线程："+i);
        }
    }
}
class Mythread extends Thread{
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("我是线程:"+ Thread.currentThread().getName()+":" + i);
        }
    }
}
/*
以上代码的输出结果是不确定的。
继承Thread类，重写run方法，start启动程序
*/
```



**2、实现Runnable接口，重写Runnable接口中的run()方法，传入目标对象+Thread.start()方法**

```java
public class Thread2 implements Runnable{
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("我在写代码"+i);
        }
    }

    public static void main(String[] args) {
        Thread2 thread2 = new Thread2();
        new Thread(thread2).start();
        for (int i = 0; i < 10; i++) {
            System.out.println("main线程"+i);
        }
    }
}

/*
以上代码的输出结果是不确定的。
实现Runnable接口，重写run方法，run启动程序
*/
```

**3、实现Callable接口，重写call()方法,有返回值。但是在运行这个线程的时候比较复杂**

```java
public class Thread5 implements Callable<Boolean> {
    private String url;
    private String name;

    public Thread5(String url, String name) {
        this.url = url;
        this.name = name;
    }

    public Boolean call() throws Exception {
        WebDownloader webDownloader = new WebDownloader();
        webDownloader.downloader(url,name);
        System.out.println("下载了文件名为："+name);
        return true;
    }

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        Thread5 ts1 = new Thread5("https://bkssl.bdimg.com/static/wiki-lemma/widget/lemma_content/configModule/posterBg/resource/img/darkBg_0300f82.png", "ts1.png");
        Thread5 ts2 = new Thread5("https://bkssl.bdimg.com/static/wiki-lemma/widget/lemma_content/configModule/posterBg/resource/img/darkBg_0300f82.png", "ts2.png");
        Thread5 ts3 = new Thread5("https://bkssl.bdimg.com/static/wiki-lemma/widget/lemma_content/configModule/posterBg/resource/img/darkBg_0300f82.png", "ts3.png");
        /*创建执行服务*/
        ExecutorService ser = Executors.newFixedThreadPool(3);
        /*提交执行*/
        Future<Boolean> res1 = ser.submit(ts1);
        Future<Boolean> res2 = ser.submit(ts2);
        Future<Boolean> res3 = ser.submit(ts3);
        /*获取结果*/
        Boolean r1 = res1.get();
        Boolean r2 = res2.get();
        Boolean r3 = res3.get();
        /*关闭服务*/
        ser.shutdownNow();

    }
}
class WebDownloader{
    public void downloader(String url,String name){
        try {
            FileUtils.copyURLToFile(new URL(url),new File(name));
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("IO异常，downloader方法出现异常");
        }
    }
}
```

### 13.10 线程状态

![image-20220810110823373](C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220810110823373.png)

**如何停止一个线程**？不推荐使用JDK自带的stop，destroy方法【已经废弃】，建议使用一个标志位进行中止变量。当flag=false,则中止线程运行。

```java
public class TestStop implements Runnable{
    boolean flag = true;
    @Override
    public void run() {
        while (flag){
            System.out.println("run----Thread");
        }
    }
    
    public void stop(){
        this.flag = false;
    }
}

```

**线程方法**

setPriority

sleep(long s):在只当的毫秒内让当前的线程失眠

join：等待该线程终止

yield：暂停当前正在执行的线程，并执行其他线程；但是礼让不一定会成功，要看CPU的心情；

interrupt

isAlive

暂停线程的几种方法：sleep，join,wait

**线程休眠**

单位是毫秒  1s=1000ms；sleep存在异常InterruptedException;

sleep时间达到之后线程进入就绪状态

==每个对象都有一个锁，sleep不会释放锁；==

作用：模拟网络延迟，放大问题的发生性；模拟倒计时

```java
public class Thread6 {

    public static void tenDown() throws InterruptedException {
        int num = 10;
        while (true){
            Thread.sleep(1000);
            System.out.println(num--);
            if(num <= 0) break;
        }
    }

    public static void main(String[] args) throws InterruptedException {
        tenDown();
    }
}
/*
10
9
8
7
6
5
4
3
2
1
*/
```

**线程礼让**

```java
public class Thread7 {
    public static void main(String[] args) {
        MyYield th1 = new MyYield();
        MyYield th2 = new MyYield();

        new Thread(th1,"a").start();
        new Thread(th2,"b").start();
    }
}
class MyYield implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"线程开始执行");
        Thread.yield();
        System.out.println(Thread.currentThread().getName()+"线程结束执行");
    }
}

```

**线程优先级**

线程优先级是最小是1，最大是10，默认是父线程的优先级，启动main方法线程的优先级一般是5。

```java
public class Thread8 {
    public static void main(String[] args) {
        System.out.println(Thread.currentThread().getName()+"----------------"+Thread.currentThread().getPriority());

        MyThread t1 = new MyThread();

        Thread thread1 = new Thread(t1);
        Thread thread2 = new Thread(t1);
        Thread thread3 = new Thread(t1);

        thread1.setPriority(Thread.MAX_PRIORITY);
        thread1.start();

        thread2.setPriority(5);
        thread2.start();

        thread3.setPriority(1);
        thread3.start();
    }
}
class MyThread implements Runnable{

    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"----------------"+Thread.currentThread().getPriority());
    }
}
/*
main----------------5
Thread-0----------------10
Thread-1----------------5
Thread-2----------------1
*/
```



## 14.设计模式

设计模式是一种思维、一种态度。

- 创造型模式【5】       **在创建对象的同时隐藏创建逻辑的方式**
  - 单例模式、工厂模式、抽象工厂模式、建造者模式、原型模式
- 结构型模式【7】   **关注类和对象的组合**
  - 适配器模式、桥接模式、装饰模式、组合模式、外观模式、享元模式、代理模式
- 行为型模式【11】 **特别关注对象之间的通信**
  - 模板方法模式、命令模式、迭代器模式、观察者模式、中介者模式、备忘录模式、解释器模式、状态模式、策略模式、责任链模式、访问者模式

### 1.创造型模式--单例模式【必须要会写】

单例模式的出发点在于对于某些类来说，只有一个实例很重要。比如一个系统只能有一个计时工具；一个系统中可以存在多个打印任务，但是只能有一个正在工作的任务。

==单例模式最重要的思想，构造器私有。==

[轻松手写单例模式的6种实现方式！再也不怕面试官问了！_资源分享_牛客网 (nowcoder.com)](https://www.nowcoder.com/discuss/612016)

单例模式确保一个类只有一个实例，并提供该实例的全局访问点。

单例模式的设计要素：

- 一个私有构造函数
- 一个私有静态变量
- 一个公有静态函数

6种实现方式

1.**懒汉式**（线程不安全）  在单线程下线程安全，在多线程下线程不安全。

```java
public class Singleton {
    private static Singleton uniqueInstance;

    private Singleton() {
    }
    public static Singleton getUniqueInstance(){
        if(uniqueInstance == null){
            uniqueInstance = new Singleton();
        }
        return uniqueInstance;
    }
}

```

```java
// 懒汉式的多线程测试
public class LazySingleton {
    private LazySingleton(){
        System.out.println(Thread.currentThread().getName()+"ok");
    }
    private static LazySingleton lazySingleton;
    public static LazySingleton getInstance(){
        if(lazySingleton == null){
            lazySingleton = new LazySingleton();
        }
        return lazySingleton;
    }

    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            new Thread(() ->{
                LazySingleton.getInstance();
            }).start();
        }
    }
}
```



2.**饿汉式**（线程安全）

```java
public class Singleton{
    private static Singleton uniqueInstance = new Singleton();
    private Singleton(){
        
    }
    public static Singleton getUniqueInstance(){
        return uniqueInstance;
    }
}
```

**懒汉式**（线程安全）  在get方法上 加了一把锁

```java
public class Singleton{
    private static Singleton singleton;
    private Singleton(){
        
    }
    public static synchronized Singleton getSingleton(){
        if(singleton == null){
            singleton = new Singleton();
        }
        return singleton;
    }
}
```

3.**双重检查锁实现**（线程安全） ==DCL懒汉式==

双重检查数相当于是改进了 线程安全的懒汉式。加一个 `volatile `关键字修饰 uniqueInstance ，volatile 会禁止 JVM 的指令重排，就可以保证多线程环境下的安全运行。

```java
public class Singleton{
    private volatile static Singleton uniqueInstance;
    private Singleton(){
        
    }
    public static Singleton getUniqueInstance(){
        if(uniqueInstance == null){
            synchronized (Singleton.class){
                if(uniqueInstance == null){
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```

4.**静态内部类实现**（线程安全）

```java
public class Singleton {

    private Singleton() {
    }

    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getUniqueInstance() {
        return SingletonHolder.INSTANCE;
    }

}
```

5.**枚举类实现**（线程安全）

```java
public enum EnumSingleton {
    INSATNCE;
    public EnumSingleton getInsatnce(){
        return INSATNCE;
    }
}
/*下面代码想要使用反射破坏枚举类型的单例模式，发现破坏不了，枚举类型不支持使用反射破坏*/
class Test{
    public static void main(String[] args) throws NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
        EnumSingleton insatnce1 = EnumSingleton.INSATNCE;
        Constructor<EnumSingleton> declaredConstructor = EnumSingleton.class.getDeclaredConstructor(String.class, int.class);
        declaredConstructor.setAccessible(true);
        EnumSingleton insatnce2 = declaredConstructor.newInstance();
        System.out.println(insatnce1.equals(insatnce2));
    }
}

/*输出：Exception in thread "main" java.lang.IllegalArgumentException: Cannot reflectively create enum objects
	at java.lang.reflect.Constructor.newInstance(Constructor.java:417)
	at single.Test.main(EnumSingleton.java:24)
*/
```

最后，我觉得以一种循序渐进的方式理解更好：
实现单例模式的话，
\1. 首先可以使用 饿汉式[方法2]，但是饿汉式是非延迟加载的，如果系统初始化很久之后才第一次使用这个单例对象的话，会造成系统资源的浪费。
2.所以为了实现延迟加载，我们有了懒汉式[方法1]，第一次使用这个单例对象的时候才创建，但是这个懒汉式是线程不安全的。
3.所以在普通懒汉式[方法1]的基础上我们在公共获取单例对象的方法上加了一把锁，实现了线程安全的懒汉式[方法3]。虽然既实现了延迟加载，又保证了线程安全，但是新的问题又来了，效率太低，每次访问都会被加锁。
4.所以，我们又把线程安全的懒汉式[方法3]改造了，使用了双重校验锁+volatile来实现，也就是双重校验锁实现[方法4]，如此不仅实现了延迟加载，保证了线程安全，还提升了性能。
5.但是双重校验锁的方式终究还是使用了锁，并且volatile 也还是会消耗一定的性能，所以我们直接不用锁了，使用静态内部类的特点来实现，如此一来，既实现了延迟加载，又保证了线程安全，还进一步提升了性能。
\6. 然后最后枚举类的话，我觉得是另辟蹊径的一种方式，是利用了枚举类的特点来实现。

应用场景：

IO、数据库连接、Redis连接

### 2.创造型模式--工厂模式

在创建对象时不会对客户端暴露创建逻辑，需要什么只需要去工厂里面获取就行了。（调用工厂里面的静态方法）

缺点：如果使用工厂模式，就需要引入一个工厂类，会增加系统的复杂度。

应用场景：

- JDBC中Connection对象的获取
- Spring中IOC容器创建管理bean对象
- 反射中Class对象的newInstance方法

### 3.创造型模式--抽象工厂模式

围绕一个超级工厂创建其他工厂，在抽象工厂模式中，接口是负责创建一个相关对象的工厂。

### 4.创造型模式--建造者模式

### 5.结构型模式--适配器模式

结构型模式的作用是从程序上实现松耦合，从而扩大整体的类结构，用来解决更大的问题。

适配器模式是将一个类的接口转换成客户希望的另一个接口。Adapter模式使得原本由于接口不兼容而不能一起工作的那些类可以在一起工作。

应用场景：

- ==比如IO中使用了适配器模式，由于 InputStream 是字节流不能享受到字符流读取字符那么便捷的功能，借助 InputStreamReader 将其转为 Reader 子类，因而可以拥有便捷操作文本文件方法；==
- java.util.Arrays 下面的asList把其他类适配为集合类。

### 6.结构型模式--代理模式

**动态代理**：

- 基于接口的动态代理JDK动态代理
- 基于类的动态代理  CGLIG动态代理

1.定义Animal接口

```java
public interface Animal {
    void eat();
}
```

2.定义Dog类

```java
public class Dog implements Animal{
    @Override
    public void eat() {
        System.out.println("小狗在吃东西");
    }
}
```

3.定义Cat类

```java
public class Cat implements Animal {
    @Override
    public void eat() {
        System.out.println("小猫在吃东西");
    }
}
```

4.动态代理生成代理类

```java
/*
方式一：生成动态代理类，调用Proxy.newProxyInstance()方法
该方法有三个参数：
loader: 用哪个类加载器去加载代理对象
interfaces:动态代理类需要实现的接口
h:某一个InvocationHandler,动态代理方法在执行时，会调用h里面的invoke方法去执行


继承InvocationHandler,重写里面的invoke方法，该方法三个参数：
proxy：就是代理对象，newProxyInstance方法的返回对象
method：调用的方法
args: 方法中的参数
*/
public class AnimalProxy implements InvocationHandler {
    private Object target;

    public AnimalProxy(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("方法调用前");
        Object result = method.invoke(target, args);
        System.out.println("方法调用后");
        return result;
    }

    public static void main(String[] args) {
        Dog dog = new Dog();
        Animal animal = (Animal) Proxy.newProxyInstance(dog.getClass().getClassLoader(), dog.getClass().getInterfaces(), new AnimalProxy(dog));
        animal.eat();

    }
}


//更通用
public class AnimalProxy implements InvocationHandler {
    private Object target;

    public Object getInstance(Object target){
        this.target = target;
        return Proxy.newProxyInstance(target.getClass().getClassLoader(),target.getClass().getInterfaces(),this);
    }
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.println("调用前");
        Object result = method.invoke(target, args);
        System.out.println("调用后");
        return result;
    }

    public static void main(String[] args) {
        AnimalProxy proxy = new AnimalProxy();
        Animal dog = (Animal) proxy.getInstance(new Dog());
        dog.eat();
    }
}

```

### JDK类库中使用到的设计模式有哪些？

**1、工厂模式**

- java.text.DateFormat 工具类 【通常我们使用其下面的SimpleDateFormat】

```java
public static void main(String[] args){
        SimpleDateFormat dateFormat1 = new SimpleDateFormat("yyyy年MM月dd日 hh:mm:ss");
        SimpleDateFormat dateFormat2 = new SimpleDateFormat();
        Date date = new Date();
        System.out.println(dateFormat1.format(date));  //2022年08月05日 10:22:08
        System.out.println(dateFormat2.format(date));  //22-8-5 上午10:22
    }
```

- 加密类KeyGenerator

```java
public static void main(String[] args) throws NoSuchAlgorithmException {
    KeyGenerator wangben = KeyGenerator.getInstance("DESede");//javax.crypto.KeyGenerator@224aed64
    System.out.println(wangben);
}
```

**2、适配器模式**   java.util包下面的Arrays

```java
public static void main(String[] args)  {
        List<Integer> list1 = Arrays.asList(1, 2, 3);
        List<Integer> list2 = Arrays.asList(new Integer[]{1, 2, 3});
        System.out.println(list1); //[1, 2, 3]
        System.out.println(list2); //[1, 2, 3]
    }
```

**3、代理模式**

JDK动态代理  定义一个类去实现InvocationHandler接口，重写里面的invoke方法。生成代理类的时候调用Proxy.getInstance方法

**4、单例模式**

全局只允许一个实例

```java
Runtime.getRuntime();
```

**5、装饰器模式**

```java
java.io.BufferedInputStream(InputStream);  
java.io.DataInputStream(InputStream);  
java.io.BufferedOutputStream(OutputStream);  
java.util.zip.ZipOutputStream(OutputStream);  
java.util.Collections.checkedList(List list, Class type) ;
```

**6、模板方法模式**  Arrays.sort方法，实现Comparable接口

```java
class Person implements Comparable{
    private Integer age;

    public Person(Integer age) {
        this.age = age;
    }

    public Integer getAge() {
        return age;
    }

    @Override
    public int compareTo(Object o) {
        Person person = (Person) o;
        return this.age.compareTo(person.age);
    }
}
public class Test {
    public static void main(String[] args)  {
        Person person1 = new Person(10);
        Person person2 = new Person(5);
        Person person3 = new Person(8);
        Person persons[] = {person1,person2,person3};
        Arrays.sort(persons);
        for (int i = 0; i < persons.length; i++) {
            System.out.println(persons[i].getAge());
        }
    }
}
```

### IO中使用到了哪些设计模式

- 适配器模式：`InputStreamReader` 和 `OutputStreamWriter` 就是两个适配器(Adapter)， 同时，它们两个也是字节流和字符流之间的桥梁。  InputStream 是字节流不能享受到字符流读取字符那么便捷的功能，借助 InputStreamReader 将其转为 Reader 子类，因而可以拥有便捷操作文本文件方法;
- 装饰器模式:  将 InputStream 字节流包装为其他流的过程就是装饰器模式，比如，包装为 FileInputStream、ByteArrayInputStream、PipedInputStream 等。
- 工厂模式：工厂模式用于创建对象。比如`Files` 类的 `newInputStream` 方法用于创建 `InputStream` 对象
- 观察者模式：NIO 中的文件目录监听服务使用到了观察者模式。NIO中的文件监听服务基于WatchService接口和Watchable接口。WatchService属于观察者，Watchable属于被观察者。

### Spring中都使用了哪些设计模式

- 代理模式：在 AOP 中有使用，Spring AOP就是基于动态代理的。
- 单例模式：bean 默认是单例模式
- 模板方法模式：jdbcTemplate
- 工厂模式：BeanFactory
- 观察者模式：Spring 事件驱动模型就是观察者模式很经典的一个应用，比如，ContextStartedEvent 就是 ApplicationContext 启动后触发的事件
- 适配器模式：Spring AOP中是基于代理模式，但是Spring AOP的增强或通知使用到了适配器模式。与之相关的接口是`AdvisorAdapter `。Spring MVC 中也是用到了适配器模式（==处理器适配器==）适配 Controller

### 并发中的设计模式

- 代理模式。这里面Thread实现了Runnable接口，lamba表达式这边也实现类Runnable接口。

```java
new Thread(()-> System.out.println("我爱你")).start();    //代理模式
```



## 15、IO

### 1、文件类和流

java提供的file类位于java.io包中，File类只负责对磁盘、文件和目录建立连接，不负责数据的输入和输出。

数据的输入和输出由流来完成。

读取文件中的内容：字节的文件流（FileInputStream)  字符的文件流（FileReader)  

向文件中写入内容：字节的文件流（FileOutputStream) 字符的文件流（FileWriter)

**字符流：各种Reader和Writer**
**字节流：各种InputStream和OutputStream**

![img](https://uploadfiles.nowcoder.com/images/20200805/643412545_1596634989327_DEF638F8839D3C558612E08DC0A11BFF)

## 总结

```
1、HashMap的底层是红黑树。  
2、Vector、HashTable、Properties和Stack是同步类,所以它们是线程安全的,可以在多线程环境下使用
3、接口没有继承Object类。
4、互斥锁指的是只有一个线程可以访问该对象。
通过继承Thread类或实现Runnable接口，只是创建线程的两种方式。
5、final 定义的变量，可以在不是必须要在定义的同时完成初始化，也可以在构造方法中完成初始化。
   final修饰方法，不能被子类重写，但是可以被重载。
6、CopyOnWriteArrayList适用于写少读多的并发场景；ReadWriteLock即为读写锁，他要求写与写之间互斥，读与写之间互斥，
   读与读之间可以并发执行。在写少读多的情况下可以提高效率；ConcurrentHashMap是同步的HashMap，读写都加锁；volatile只保证多线	  程操作的可见性，不保证原子性。
7、final修饰变量，变量的引用（也就是指向的地址）不可变，但是引用的内容可以变（地址中的内容可变）。
```





# 数据库

## 1、数据库三范式

第一范式：所有的列都是原子性的，每一列不可分割。比如地址可以存为南京市江宁区，违背了第一范式，应该拆开存储。

第二范式：在第一范式的基础之上，同时要求数据库每个记录被唯一区分。比如存储用户和权限，如果使用用户id和权限id作为主键，其中任意的一个信息并不是和主键完全相关的。

第三范式：在第二范式的基础之上，一个关系不包含已在其他关系中已包含的非主关键字信息。比如，部门信息表有部门编号，部分名称等，员工信息表列出部门编号之后，就不能将部门名称再加入了，否则会冗余。

## 2. sql 中的正则表达式

| 选项 | 说明               | 例子                            | 匹配值示例               |
| :--- | :----------------- | :------------------------------ | :----------------------- |
| ^    | 匹配文本的开始字符 | '^b' 匹配以字母 b 开头 的字符串 | book、big、banana、 bike |

| [^]  | 匹配不在括号中的任何字符 | '[^abc]’ 匹配任何不包 含 a、b 或 c 的字符串 | desk、fox、f8ke |
| ---- | ------------------------ | ------------------------------------------- | --------------- |
|      |                          |                                             |                 |

```sql
SELECT * FROM Person Address REGEXP '^[^CO]';//不在的
```



表示筛查出所有匹配[^CO]的项，而[^CO]表示匹配任何不包含C、O的字符串

## 3. MyISAM 和 InnoDB 的区别是什么？

存储引擎用来存储数据，提供读写的接口。

MyISAM （Mysql5.5之前默认的存储引擎） 

 InnoDB （Mysql5.5之后默认的存储引擎）

**是否支持行级锁**:MyISAM 只有表级锁(table-level locking)，而 InnoDB 支持行级锁(row-level locking)和表级锁,默认为行级锁。

**是否支持事务**：MyISAM 不提供事务支持。InnoDB 提供事务支持，实现了 SQL 标准定义了四个隔离级别，具有提交(commit)和回滚(rollback)事务的能力。==重要==

**是否支持外键**：MyISAM 不支持，而 InnoDB 支持。外键对于维护数据一致性非常有帮助，但是对性能有一定的损耗。因此，通常情况下，我们是不建议在实际生产项目中使用外键的。

**是否支持数据库异常崩溃后的安全恢复**：MyISAM 不支持。

而 InnoDB 支持。使用 InnoDB 的数据库在异常崩溃后，数据库重新启动的时候会保证数据库恢复到崩溃前的状态。==重要==

**是否支持 MVCC**：MyISAM 不支持，而 InnoDB 支持。 MyISAM 连行级锁都不支持。MVCC 可以看作是行级锁的一个升级。

**读写性能**：InnoDB增删改性能更优；MyISAM查询性能更优。

**索引实现不一样**： MyISAM 引擎和 InnoDB 引擎都是使用 B+Tree 作为索引结构，但是两者的实现方式不太一样。

InnoDB 引擎中，其数据文件本身就是索引文件。相比 MyISAM，索引文件和数据文件是分离的，其表数据文件本身就是按 B+Tree 组织的一个索引结构，树的叶节点 data 域保存了完整的数据记录。

## 4.什么是事务？事务的特性，事务的隔离级别？

**什么是事务**：事务是逻辑上的一组操作，要么都执行，要么都不执行。

**关系型数据库事务的四大特性**：关系型数据库是建立在关系模型之上的数据库，关系模型包括一对一，一对多或者多对多。

原子性：事务是最小的执行单位，不可以再划分。

一致性：执行事务的前后，数据是一致的。

隔离性：并发访问数据库的时候（多个用户访问数据库的时候），一个用户的事务不被其他的事务打扰。

持久性：一个事务被提交之后，对数据库的修改是永久的。

## 5.并发事务带来的问题以及事务的隔离机制

**并发事务带来的问题可以分为4类：脏读，丢失修改、不可重复读、幻读**

脏读：一个事务在访问数据库数据的时候，对其进行了修改，但是这种修改还没有提交到数据库之中。另一个事务对其进行了访问，因为修改的数据还没有提交到数据库，导致读取的数据是脏数据。

丢失修改：两个事务同时访问一个数据，并对其进行修改，后一个事务的修改导致前一个事务的修改结果丢失，不起作用。

不可重复读：一个事务多次访问一个数据，访问的过程中，另一个事务对其进行了修改，导致第一个事务前后读取的数据不一样。

幻读：和不可重复读类似，指一个事务读取表中的数据，当已经读取几行数据之后，另一个事务对表进行操作，或增加或删除行数据，导致第一个事务在后面的查询过程中，发现了不存在的数据（增加了/减少了记录），像发生幻觉一样。

**SQL 标准定义了四个隔离级别：**

- **READ-UNCOMMITTED(读取未提交)** ： 最低的隔离级别，允许读取尚未提交的数据变更，可能会导致脏读、幻读或不可重复读。
- **READ-COMMITTED(读取已提交)** ： 允许读取并发事务已经提交的数据，可以阻止脏读，但是幻读或不可重复读仍有可能发生。
- **REPEATABLE-READ(可重复读)** ： 对同一字段的多次读取结果都是一致的，除非数据是被本身事务自己所修改，可以阻止脏读和不可重复读，但幻读仍有可能发生。
- **SERIALIZABLE(可串行化)** ： 最高的隔离级别，完全服从 ACID 的隔离级别。所有的事务依次逐个执行，这样事务之间就完全不可能产生干扰，也就是说，该级别可以防止脏读、不可重复读以及幻读。

| 隔离级别         | 脏读 | 不可重复读 | 幻读 |
| ---------------- | ---- | ---------- | ---- |
| READ-UNCOMMITTED | √    | √          | √    |
| READ-COMMITTED   | ×    | √          | √    |
| REPEATABLE-READ  | ×    | ×          | √    |
| SERIALIZABLE     | ×    | ×          | ×    |

上述4种隔离级别MySQL都支持,并且InnoDB存储引擎默认支持隔离级别是==REPEATABLE READ==（可重复读）。

## 6.Mysql锁

**表级锁和行级锁了解吗？有什么区别？**

MyISAM 仅仅支持表级锁(table-level locking)，一锁就锁整张表。

InnoDB 不光支持表级锁(table-level locking)，还支持行级锁(row-level locking)，默认为行级锁。行级锁的粒度更小。



innodb支持的锁类型：

- 记录锁（单个记录上的锁）
- 间隙锁（锁定一个范围，不包括记录本身）
- 临键锁（锁定一个范围，包括记录本身）

## 7.索引

**什么是索引**：索引相当于是一本字典的目录，通过目录，我们可以快速查找到我们想要查找的数据。索引其实是一种数据结构，是看表中的哪些行符合where子句后面的条件，并根据这些行找到其他列的数据结构。

**索引的底层数据结构**：

- hash表：哈希表是键值对集合，根据key能够快速的找到value。**为什么MySQL 没有使用其作为索引的数据结构呢？**首先是**Hash 冲突问题** ：我们上面也提到过Hash 冲突了，不过对于数据库来说这还不算最大的缺点。其次是**Hash 索引不支持顺序和范围查询(Hash 索引不支持顺序和范围查询是它最大的缺点**）
- B树和B+树：在提到B+树的时候，首先会提到B树，B树又称多路平衡查找树，B+树是B树的变体。

​		1、B树的所有节点既存放key也存放数据。而B+树只有叶子节点存放key和对应的数据，其他节点存放的只是key

​        2、B树的叶子节点之间是相互独立的，B+树的叶子节点之间有引用链指向相邻的节点

​		3、B树的检索过程相当于是对范围内每个节点的关键字做二分查找，可能还没有访问到叶子节点，查询就结束了；

​				而B+树的检索效率就很稳定了，任何查找都是从根节点 到叶子节点的过程，叶子节点的顺序检索很明显。

**索引类型**

1、主键索引和二级索引。

主键索引：数据表中主键列使用的就是主键索引。一张表只能有一个主键，不能为空，不能重复。

二级索引：二级索引的叶子节点存放的数据是主键，通过索引可以快速定位到主键的位置。普通索引，唯一索引，前缀索引，全文索引都是二级索引。

2、聚集索引和非聚集索引。

聚集索引即索引结构和数据一起存放的索引，主键索引属于聚集索引。

聚集索引的优点：聚集索引的查询速度很快，定位到索引的节点相当于定位到了数据。

聚集索引的缺点：依赖于有序的数据且更新的代价大。

非聚集索引即索引结构和数据分开存放的索引，二级索引属于非聚集索引。

非聚集索引的优点：更新代价比聚集索引小。

非聚集索引的缺点：依赖于有序的数据且可能会进行二次查询。

==非聚集索引也不一定走回表查询==

3、覆盖索引和联合索引。

如果一个索引包含所有需要查询的字段的值，我们就称之为“覆盖索引”。

使用表中的多个字段创建索引，就是 **联合索引**，也叫 **组合索引** 或 **复合索引**。覆盖索引和联合索引其实并不等价。

**最左前缀原则**（重点）

最左前缀匹配原则指的是，在使用联合索引时，**MySQL** 会根据联合索引中的字段顺序，从左到右依次到查询条件中去匹配，如果查询条件中存在与联合索引中最左侧字段相匹配的字段，则就会使用该字段过滤一批数据，直至联合索引中全部字段匹配完成，或者在执行过程中遇到范围查询，如 **`>`**、**`<`**、**`between`** 和 **`以%开头的like查询`** 等条件，才会停止匹配。

## 8.Mysql性能优化

Mysql的性能优化可以从4个部分。

- 硬件和操作系统的优化，从硬件层面讲，影响Mysql性能的因素CPU、可用内存大小，磁盘读写速度和网络带宽。从操作系统层面来讲，操作系统网络配置都会影响Mysql性能。这部分优化一般由运维工程师完成。
- 架构设计层面的优化。Mysql是一个磁盘IO访问非常频繁的关系型数据库，此时的优化可以分为：
  - 搭建Mysql主从集群，单个Mysql服务容易出现单点故障，一旦服务器宕机就会导致依赖Mysql的应用全部失效；
  - 读写分离设计，在读多写少的场景中，通过读写分离，可以避免读写冲突导致的性能影响
  - 引入分库分表机制，分库可以降低单个服务器节点的IO压力，分表可以降低单表数据量，提升sql查询的效率。
  - 针对热点数据，引入更高效的分布式数据库，比如Redis等，缓解Mysql访问的压力。

- MYSQL程序配置的优化：一般通过Mysql中的配置文件my.cnf来完成，比如Mysql5.7版本中默认最大连接数151，这个值可以在my.cnf中修改。
- SQL优化
  - ==慢sql的定位和排查==，通过慢查询日志和慢查询分析工具得到有问题的sql列表；
  - ==执行计划分析==，针对慢sql，可以使用explain查看当前sql的执行计划，可以重点关注type key rows等字段，从而定位该sql执行慢的根本原因。
  - ==使用show profile工具==，针对运行慢的sql可以使用profile工具，得到sql执行过程中所有的资源的开销情况，如IO开销，cpu开销，内存开销等。

## 9.Redis

使用redis缓存是为了解决访问常规关系型数据库的速度和程序处理速度不对等的问题。

## 10、数据库的语句

**修改数据库表名称**

```sql
ALTER TABLE 旧表名 RENAME TO 新表名；
```

**升序排序**

```sql
SELECT * FROM TABLE ORDER BY ID;(默认升序排序，或者加上ASC)
SELECT * FROM TABLE ORDER BY ID DESC;(按照id降序排序)
```

**不去重处理**

```sql
UNION ALL

/*查找山东大学或者男性的记录，不去重*/
select device_id,gender,age,gpa from user_profile where university = '山东大学' 
union all
select device_id,gender,age,gpa from user_profile where gender = 'male'
```

```sql
UNION    把两次或者多次查询的结果结合起来，必须保证两次查询的列数必须相同。
SELECT device_id, gender, age, university,gpa from user_profile where gpa > 3.8 and university = '复旦大学' UNION
SELECT device_id, gender, age, university,gpa from user_profile where gpa > 3.5 and university = '山东大学'
```



**INNER JOIN**左右两个表中都有的数据，并且子段都不能为NULL才可以匹配

Mysql中表student_table(id,name,birth,sex)，插入如下记录：

('1003' , '' , '2000-01-01' , '男');
('1004' , '张三' , '2000-08-06' , '男');
('1005' , NULL , '2001-12-01' , '女');

('1006' , '张三' , '2000-08-06' , '女');

('1007' , ‘王五’ , '2001-12-01' , '男');

('1008' , '李四' , NULL, '女');

('1009' , '李四' , NULL, '男');

('1010' , '李四' , '2001-12-01', '女');

执行

```sql
select t1.*,t2.* from(
select * from student_table where sex = '男')t1
inner join
(select * from student_table where sex = '女')t2
on t1.birth = t2.birth and t1.name=t2.name;
```

题目中【inner join ... on t1.birth = t2.birth and t1.name = t2.name ; 】inner join意思是左右表中的birth、name都不为NULL时才会匹配上，结果中不含有一个字段为NULL或两个字段都为NULL的记录，结果只有‘张三’一条记录。所以选D.

查询结果如下图：

![img](https://uploadfiles.nowcoder.com/images/20211101/385276_1635751629172/D4A043968C035B4C0B353BB2BA4E84E3)



### 基础的编程题目

#### 1、建立表格（最基本的）

```sql
create table if not exists `user_info_vip`(
    id int primary key auto_increment comment '自增ID',
    uid int unique not null comment '用户ID',
    nick_name varchar(64) comment '昵称',
    achievement int default 0 comment '成就值',
    level int comment '用户等级',
    job varchar(32) comment '职业方向',
    register_time datetime default current_timestamp comment '注册时间'
) character set utf8;

或者
create table user_info_vip(
    id int primary key auto_increment comment '自增ID',
    uid int unique not null comment '用户ID',
    nick_name varchar(64) comment '昵称',
    achievement int default 0 comment '成就值',
    level int comment '用户等级',
    job varchar(32) comment '职业方向',
    register_time datetime default CURRENT_TIMESTAMP comment '注册时间'
) charset=utf8

```

==插入数据==

1、往表格中插入多条记录，存在自增主键的情况下，我i们不用插入主键了。

```sql
insert into exam_record (uid,exam_id,start_time,submit_time,score) values
(1001,9001,'2021-09-01 22:11:12','2021-09-01 23:01:12',90),
(1002,9002,'2021-09-04 07:01:02',Null,Null)
```

2、从另一个表中导入（注意datetime时间的比较）

```sql
insert into exam_record_before_2021(uid,exam_id,start_time,submit_time,score)
select uid,exam_id,start_time,submit_time,score
from exam_record where year(submit_time) < '2021'
```

3、修改表格中的子段，部分插入

可以先删除原有的子段然后再插入

```sql
delete from examination_info
where exam_id = 9003;

insert into examination_info(exam_id,tag,difficulty,duration,release_time) values 
(9003,'SQL','hard',90,'2021-01-01 00:00:00')
```

直接使用replace函数 replace into .. values..

```sql
replace into examination_info
values (null,9003,'SQL','hard',90,'2021-01-01 00:00:00')
```

==更新数据==

1、直接更新 UPDATE table_name SET column_name=new_value [, column_name2=new_value2] [WHERE column_name3=value3]

```sql
UPDATE examination_info
SET tag = "Python"
WHERE tag = "PYTHON";
```

```sql
update exam_record
set submit_time = '2099-01-01 00:00:00', score = 0
where start_time < '2021-09-01 00:00:00' and submit_time is null
```

2、根据已有值替换 UPDATE table_name SET key1=replace(key1, '查找内容', '替换成内容') [WHERE column_name3=value3]

```sql
UPDATE examination_info
SET tag = REPLACE(tag, "PYTHON", "Python")
WHERE tag = "PYTHON";
```

==删除记录==

1、根据条件删除  DELETE FROM tb_name [WHERE options] [ [ ORDER BY fields ] LIMIT n ]

时间差**TIMESTAMPDIFF(interval, time_start, time_end)**，其中interval中常选

- SECOND 秒
- MINUTE 分钟（返回秒数差除以60的整数部分）
- HOUR 小时（返回秒数差除以3600的整数部分）
- DAY 天数（返回秒数差除以3600*24的整数部分）
- MONTH 月数
- YEAR 年数

删除用时小于5分钟的且分数低于60 的记录

```sql
delete from exam_record
where timestampdiff(minute,start_time,submit_time) < 5 and score < 60
```

删除未完成作答的记录或者或作答时间小于5分钟整的记录中  前3条记录

```sql
delete from exam_record
where submit_time is null or timestampdiff(minute,start_time,submit_time) < 5 
order by start_time
limit 3
```

删除整张表的记录并重置自增主键

```sql
truncate exam_record 
```

删除表

```sql
drop table if exists exam_record_2011,exam_record_2012,exam_record_2013,exam_record_2014
```

delete，truncate，drop的区别：

1、truncate和delete只删除数据不删除表的结构，而drop会删除表的结构被依赖的约束(constrain)，[触发器](https://so.csdn.net/so/search?q=触发器&spm=1001.2101.3001.7020)(trigger)，索引；

2、delete命令是DML(数据操作语言），删除的数据将存储在系统回滚段中，需要的时候，数据可以回滚恢复。

而truncate，drop命令是DDL（数据定义语言），删除的数据是操作立即生效，原数据不放到rollback segment中，不能回滚，数据不可以回滚恢复。

3、delete命令，不会自动提交事务，操作会触发trigger；而truncate，drop命令，执行后会自动提交事务，操作不触发trigger。

4、速度：drop>truncate>delete

==修改表==

增加表格某一列：alter table 增加的表格 add 增加列的名称 数据类型 位置(after level 在level 之后)

```sql
alter table user_info add school varchar(15) after level;
增加列在某列之后
```

更改列的名称和数据类型：alter table user_info change 原列名 修改列名 修改数据类型

```sql
alter table user_info change job profession varchar(10);
```

更改列的值：alter table 表名 modify 修改列名称 数据类型 默认值等

```sql
alter table user_info modify achievement int(11) default 0;
```



#### 2、索引（最基本的）

==创建索引==

create方式和alter方式

```sql
CREATE 
  [UNIQUE -- 唯一索引
  | FULLTEXT -- 全文索引
  ] INDEX index_name ON table_name -- 不指定唯一或全文时默认普通索引
  (column1[(length) [DESC|ASC]] [,column2,...]) -- 可以对多列建立组合索引  
  
ALTER TABLE tb_name ADD [UNIQUE | FULLTEXT] [INDEX] index_content(content)
```

```sql
create index idx_duration on examination_info(duration);/*创建普通索引*/
create unique index uniq_idx_exam_id on examination_info(exam_id);/*创建普通索引*/
create fulltext index  full_idx_tag on examination_info(tag);/*创建全局索引*/
```

==删除索引==

drop方式和alter方式

```sql
DROP INDEX <索引名> ON <表名>
ALTER TABLE <表名> DROP INDEX <索引名>
```



#### **查询结果去重**

```sql
select distinct university from user_profile;
select university from user_profile group by university;

select 
count(id) as total_pv,
count(score) as complete_pv,
count(distinct exam_id and score is not null) as complete_exam_cnt 
from exam_record
```

#### **限制查询返回的行数**

LIMIT 子句可以被用于强制 SELECT 语句返回指定的记录数

1、只接受一个参数，返回最大记录行的数目

检索前5个记录行

```sql
select * from table limit 5
```

2、给定两个参数，第一个参数指定第一个返回记录行的偏移量，第二个参数指定返回记录行的最大数目

检索6-10行

```sql
select * from table limit 5,5
```

3、检索从某一个偏移量到记录集的结束所有的记录行，可以指定第二个参数为 -1。

检索记录行11开始到结束

```sql
select * from table limit 10,-1
```

#### **查询到记录结束并更改列值**

需要查看前2个用户明细设备ID数据，并将列名改为 'user_infos_example'

```sql
select device_id as user_infos_example from user_profile limit 2
```

#### **查找后单列排序**

取出用户信息表中的用户年龄，请取出相应数据，并按照年龄升序排序

```sql
select device_id,age from user_profile order by age
```

#### **查找后多列排序**

取出用户信息表中的年龄和gpa数据，并先按照gpa升序排序，再按照年龄升序排序输出，请取出相应数据。【升序可以省略asc】

```sql
select device_id,gpa,age from user_profile order by gpa,age          (升序排序)
select device_id,gpa,age from user_profile order by gpa desc,age desc(降序排序)
```

#### **查找某个阶段的信息**

between 和 and

```sql
select device_id,gender,age from user_profile where age>=20 and age<=23
select device_id,gender,age from user_profile where age between 20 and 23
```

#### **查找信息 排除某个子段**

查看除复旦大学以外的所有用户明细

```sql
select device_id,gender,age,university from user_profile where university<>'复旦大学'
select device_id,gender,age,university from user_profile where university != '复旦大学'
select device_id,gender,age,university from user_profile where university not like '复旦大学'
select device_id,gender,age,university from user_profile where university not in ('复旦大学')
```

#### **查找子段不为空的信息（过滤空值）**

```sql
select device_id,gender,age,university from user_profile where age != 'null'
select device_id,gender,age,university from user_profile where age is not null
```

**where in ** 和 **not in **

要找到学校为北大、复旦和山大的同学进行调研

```sql
select device_id,gender,age,university,gpa from user_profile where university in ('北京大学','复旦大学','山东大学')
```

#### **模糊匹配**

_：匹配任意一个字符；
%：匹配0个或多个字符；
[ ]：匹配[ ]中的任意一个字符(若要比较的字符是连续的，则可以用连字符“-”表 达 )；
[^]：不匹配[ ]中的任意一个字符。

- 查询学生表中姓’张‘的学生的学生姓名 

```sql
select * from 学生表 where 姓名 like '张%'
```

- 查询姓’张‘且名字是三个字的学生

```sql
select * from 学生表 where 姓名 like '张__'
```

- 查询学生表中姓‘张’、姓‘李’和姓‘刘’的学生的情况。

```sql
SELECT * FROM 学生表 WHERE 姓名 LIKE '[张李刘]%’
```

- 从学生表表中查询学号的最后一位不是2、3、5的学生信息。

```sql
SELECT * FROM 学生表 WHERE 学号 LIKE '%[^235]'
```



#### **找到一列的最大值**

知道复旦大学学生gpa最高值是多少

```sql
select gpa from user_profile where university = '复旦大学' order by gpa desc limit 1
select max(gpa) from user_profile where university = '复旦大学'
```

#### **平均数，计数**

看一下男性用户有多少人以及他们的平均gpa是多少，并把列重新命名

```sql
select count(gender) as male_num, round(avg(gpa),1) as avg_gpa from user_profile where gender = 'male'
```

去掉最大值和最小值求平均值

```sql
select tag,difficulty,
round((sum(score)-max(score)-min(score))/(count(score)-2),1) as clip_avg_score
from examination_info ei
join exam_record er
on ei.exam_id=er.exam_id
where  tag='SQL' and difficulty='hard'
```

平均活跃天数和月活跃人数==【与时间相关】==

计算2021年每个月里试卷作答区用户平均月活跃天数avg_active_days和月度活跃人数mau

```sql
select date_format(submit_time,'%Y%m') as month,
round(count(distinct uid,date_format(submit_time,'%y%m%d'))/count(distinct uid),2) as avg_active_days,
count(distinct uid) as mau
from exam_record
where submit_time is not null and year(submit_time) = 2021
group by date_format(submit_time,'%Y%m')
```

统计出2021年每个月里用户的月总刷题数month_q_cnt 和日均刷题数avg_day_q_cnt（按月份升序排序）

```sql
select 
date_format(submit_time,'%Y%m') submit_month, 
any_value(count(submit_time)) month_q_cnt, 
any_value(round(count(submit_time)/day(last_day(submit_time)),3)) avg_day_q_cnt
from practice_record
where year(submit_time) = '2021'
group by submit_month
union
select 
'2021汇总' as submit_month,
count(submit_time) month_q_cnt, 
round(count(submit_time)/31,3) avg_day_q_cnt
from practice_record
where year(submit_time) = '2021'
order by submit_month
```

了解复旦大学的每个用户在8月份练习的总题目数和回答正确的题目数情况，请取出相应明细数据，对于在8月份没有练习过的用户，答题数结果返回0.

用户信息表user_profile

| id   | device_id | gender | age  | university | gpa  | active_days_within_30 |
| ---- | --------- | ------ | ---- | ---------- | ---- | --------------------- |
| 1    | 2138      | male   | 21   | 北京大学   | 3.4  | 7                     |
| 2    | 3214      | male   |      | 复旦大学   | 4.0  | 15                    |
| 3    | 6543      | female | 20   | 北京大学   | 3.2  | 12                    |
| 4    | 2315      | female | 23   | 浙江大学   | 3.6  | 5                     |
| 5    | 5432      | male   | 25   | 山东大学   | 3.8  | 20                    |
| 6    | 2131      | male   | 28   | 山东大学   | 3.3  | 15                    |
| 7    | 4321      | female | 26   | 复旦大学   | 3.6  | 9                     |

示例：question_practice_detail

| id   | device_id | question_id | result | date       |
| ---- | --------- | ----------- | ------ | ---------- |
| 1    | 2138      | 111         | wrong  | 2021-05-03 |
| 2    | 3214      | 112         | wrong  | 2021-05-09 |
| 3    | 3214      | 113         | wrong  | 2021-06-15 |
| 4    | 6543      | 111         | right  | 2021-08-13 |
| 5    | 2315      | 115         | right  | 2021-08-13 |
| 6    | 2315      | 116         | right  | 2021-08-14 |
| 7    | 2315      | 117         | wrong  | 2021-08-15 |
| ……   |           |             |        |            |

根据示例，你的查询应返回以下结果：

| device_id | university | question_cnt | right_question_cnt |
| --------- | ---------- | ------------ | ------------------ |
| 3214      | 复旦大学   | 3            | 0                  |
| 4321      | 复旦大学   | 0            | 0                  |

```sql
select up.device_id, '复旦大学' as university,
    count(question_id) as question_cnt,
    sum(if(qpd.result='right', 1, 0)) as right_question_cnt
from user_profile as up

left join question_practice_detail as qpd
  on qpd.device_id = up.device_id and month(qpd.date) = 8

where up.university = '复旦大学'
group by up.device_id
```



#### 日期相关（重点）

```
1.date_format(submit_time,'%Y%m') ---年/月
2.date_format(submit_time,'%y%m%d') ---年、月、日
3.select DAYNAME("1998-02-05");--'Thursday'  返回date的星期名字
4.select MONTHNAME("1998-02-05");--'February' 返回date的月份名字
5.两个日期的间隔1天   date_add(date1, interval 1 day)=date2
```

**第二天再来（难点）**

```sql
select count(date2) / count(date1) as avg_ret
from (
    select
        distinct qpd.device_id,
        qpd.date as date1,
        uniq_id_date.date as date2
    from question_practice_detail as qpd
    left join(
        select distinct device_id, date
        from question_practice_detail
    ) as uniq_id_date
    on qpd.device_id=uniq_id_date.device_id
        and date_add(qpd.date, interval 1 day)=uniq_id_date.date
) as id_last_next_date
```

#### 文本相关

```
1.substring_index()---截取函数
2.substring_index(substring_index())--取出某个值
```



1、想要统计每个性别的用户分别有多少参赛者，请取出相应结果

示例：user_submit

| device_id | profile              | blog_url            |
| --------- | -------------------- | ------------------- |
| 2138      | 180cm,75kg,27,male   | http:/url/bigboy777 |
| 3214      | 165cm,45kg,26,female | http:/url/kittycc   |
| 6543      | 178cm,65kg,25,male   | http:/url/tiger     |
| 4321      | 171cm,55kg,23,female | http:/url/uhksd     |
| 2131      | 168cm,45kg,22,female | http:/urlsydney     |

根据示例，你的查询应返回以下结果：

| gender | number |
| ------ | ------ |
| male   | 2      |
| female | 3      |

```sql
select substring_index(profile,',',-1) as gender,
count(device_id) as number
from user_submit
group by gender

SELECT IF(profile LIKE '%female','female','male') gender,COUNT(*) number
FROM user_submit
GROUP BY gender;
```

2、

#### **分组计算**

要对每个学校不同性别的用户活跃情况和发帖数量进行分析，请分别计算出每个学校每种性别的用户数、30天内平均活跃天数和平均发帖数量。

用户信息表：user_profile

30天内活跃天数字段（active_days_within_30）

发帖数量字段（question_cnt）

回答数量字段（answer_cnt）

| id   | device_id | gender | age  | university | gpa  | active_days_within_30 | question_cnt | answer_cnt |
| ---- | --------- | ------ | ---- | ---------- | ---- | --------------------- | ------------ | ---------: |
| 1    | 2138      | male   | 21   | 北京大学   | 3.4  | 7                     | 2            |         12 |
| 2    | 3214      | male   |      | 复旦大学   | 4.0  | 15                    | 5            |         25 |
| 3    | 6543      | female | 20   | 北京大学   | 3.2  | 12                    | 3            |         30 |
| 4    | 2315      | female | 23   | 浙江大学   | 3.6  | 5                     | 1            |          2 |
| 5    | 5432      | male   | 25   | 山东大学   | 3.8  | 20                    | 15           |         70 |
| 6    | 2131      | male   | 28   | 山东大学   | 3.3  | 15                    | 7            |         13 |
| 7    | 4321      | male   | 26   | 复旦大学   | 3.6  | 9                     | 6            |            |

查询返回结果需要对**性别和学校分组**，示例如下，结果保留1位小数，1位小数之后的四舍五入：

| gender | university | user_num | avg_active_day | avg_question_cnt |
| ------ | ---------- | -------- | -------------- | ---------------- |
| male   | 北京大学   | 1        | 7.0            | 2.0              |
| male   | 复旦大学   | 2        | 12.0           | 5.5              |
| female | 北京大学   | 1        | 12.0           | 3.0              |
| female | 浙江大学   | 1        | 5.0            | 1.0              |
| male   | 山东大学   | 2        | 17.5           | 11.0             |

```sql
select 
gender,university,
count(device_id) as user_num,
round(avg(active_days_within_30),1) as avg_active_day,
round(avg(question_cnt),1) as avg_question_cnt
from user_profile
group by gender,university
```

#### **分组过滤--where / having**

==注意：聚合函数结果作为筛选条件时，不能用where，而是用having语法，配合重命名即可；==

group by 和 having一起使用

取出平均发贴数低于5的学校或平均回帖数小于20的学校。

根据示例，你的查询应返回以下结果，请你保留3位小数(系统后台也会自动校正)，3位之后四舍五入：

| university | avg_question_cnt | avg_answer_cnt |
| ---------- | ---------------- | -------------- |
| 北京大学   | 2.5000           | 21.000         |
| 浙江大学   | 1.000            | 2.000          |

```sql
select university,
round(avg(question_cnt),3) as avg_question_cnt,
round(avg(answer_cnt),3) as avg_answer_cnt
from user_profile
group by university
having avg_question_cnt <5 or avg_answer_cnt <20
```

#### 分组排序

查看不同大学的用户平均发帖情况，并期望结果按照平均发帖情况进行升序排列，请你取出相应数据。
根据示例，你的查询应返回以下结果：

| university | avg_question_cnt |
| ---------- | ---------------- |
| 浙江大学   | 1.0000           |
| 北京大学   | 2.5000           |
| 复旦大学   | 5.5000           |
| 山东大学   | 11.0000          |

```sql
select university,
avg(question_cnt) as avg_question_cnt
from user_profile
group by university
order by avg_question_cnt
```

#### 连表查询

1、要查看所有来自浙江大学的用户题目回答明细情况，请你取出相应数据

question_practice_detail

| id   | device_id | question_id | result |
| ---- | --------- | ----------- | ------ |
| 1    | 2138      | 111         | wrong  |
| 2    | 3214      | 112         | wrong  |
| 3    | 3214      | 113         | wrong  |
| 4    | 6543      | 114         | right  |
| 5    | 2315      | 115         | right  |
| 6    | 2315      | 116         | right  |
| 7    | 2315      | 117         | wrong  |

user_profile

| id   | device_id | gender | age  | university | gpa  | active_days_within_30 | question_cnt | answer_cnt |
| ---- | --------- | ------ | ---- | ---------- | ---- | --------------------- | ------------ | ---------- |
| 1    | 2138      | male   | 21   | 北京大学   | 3.4  | 7                     | 2            | 12         |
| 2    | 3214      | male   |      | 复旦大学   | 4.0  | 15                    | 5            | 25         |
| 3    | 6543      | female | 20   | 北京大学   | 3.2  | 12                    | 3            | 30         |
| 4    | 2315      | female | 23   | 浙江大学   | 3.6  | 5                     | 1            | 2          |
| 5    | 5432      | male   | 25   | 山东大学   | 3.8  | 20                    | 15           | 70         |
| 6    | 2131      | male   | 28   | 山东大学   | 3.3  | 15                    | 7            | 13         |
| 7    | 4321      | female | 26   | 复旦大学   | 3.6  | 9                     | 6            | 52         |

输出：查询结果根据question_id升序排序：

![img](https://uploadfiles.nowcoder.com/images/20210825/999991344_1629872498861/D9E601E7A15464E123E07993B5B38512)

子查询

```sql
select device_id,question_id,result 
from question_practice_detail
where device_id in
(select device_id from user_profile where university = '浙江大学')
order by question_id

select
   score min_score_over_avg
from exam_record
where exam_id in 
     (select exam_id from examination_info
      where tag = 'SQL') and 
      score >= (select avg(score) from exam_record
                where exam_id in 
                (select exam_id from examination_info
                where tag = 'SQL'))
order by score
limit 1
```

连接查询

```sql
select question_practice_detail.device_id,question_id,result 
from question_practice_detail,user_profile
where question_practice_detail.device_id=user_profile.device_id and user_profile.university = '浙江大学'
order by question_practice_detail.question_id
```

内连接查询

```sql
select question_practice_detail.device_id,question_id,result 
from question_practice_detail inner join user_profile
on question_practice_detail.device_id=user_profile.device_id and user_profile.university = '浙江大学'
order by question_practice_detail.question_id
```

2、计算不同学校、不同难度的用户平均答题量，

用户信息表：user_profile

| id   | device_id | gender | age  | university | gpa  | active_days_within_30 | question_cnt | answer_cnt |
| ---- | --------- | ------ | ---- | ---------- | ---- | --------------------- | ------------ | ---------- |
| 1    | 2138      | male   | 21   | 北京大学   | 3.4  | 7                     | 2            | 12         |
| 2    | 3214      | male   | NULL | 复旦大学   | 4    | 15                    | 5            | 25         |
| 3    | 6543      | female | 20   | 北京大学   | 3.2  | 12                    | 3            | 30         |
| 4    | 2315      | female | 23   | 浙江大学   | 3.6  | 5                     | 1            | 2          |
| 5    | 5432      | male   | 25   | 山东大学   | 3.8  | 20                    | 15           | 70         |
| 6    | 2131      | male   | 28   | 山东大学   | 3.3  | 15                    | 7            | 13         |
| 7    | 4321      | male   | 28   | 复旦大学   | 3.6  | 9                     | 6            | 52         |

question_practice_detail

| id   | device_id | question_id | result |
| ---- | --------- | ----------- | ------ |
| 1    | 2138      | 111         | wrong  |
| 2    | 3214      | 112         | wrong  |
| 3    | 3214      | 113         | wrong  |
| 4    | 6534      | 111         | right  |
| 5    | 2315      | 115         | right  |
| 6    | 2315      | 116         | right  |
| 7    | 2315      | 117         | wrong  |
| 8    | 5432      | 117         | wrong  |
| 9    | 5432      | 112         | wrong  |
| 10   | 2131      | 113         | right  |
| 11   | 5432      | 113         | wrong  |
| 12   | 2315      | 115         | right  |
| 13   | 2315      | 116         | right  |
| 14   | 2315      | 117         | wrong  |
| 15   | 5432      | 117         | wrong  |
| 16   | 5432      | 112         | wrong  |
| 17   | 2131      | 113         | right  |
| 18   | 5432      | 113         | wrong  |
| 19   | 2315      | 117         | wrong  |
| 20   | 5432      | 117         | wrong  |
| 21   | 5432      | 112         | wrong  |
| 22   | 2131      | 113         | right  |
| 23   | 5432      | 113         | wrong  |

question_detail

| id   | question_id | difficult_level |
| ---- | ----------- | --------------- |
| 1    | 111         | hard            |
| 2    | 112         | medium          |
| 3    | 113         | easy            |
| 4    | 115         | easy            |
| 5    | 116         | medium          |
| 6    | 117         | easy            |

输出：以下结果(结果在小数点位数保留4位，4位之后四舍五入)：

| university | difficult_level | avg_answer_cnt |
| ---------- | --------------- | -------------- |
| 北京大学   | hard            | 1.0000         |
| 复旦大学   | easy            | 1.0000         |
| 复旦大学   | medium          | 1.0000         |
| 山东大学   | easy            | 4.5000         |
| 山东大学   | medium          | 3.0000         |
| 浙江大学   | easy            | 5.0000         |
| 浙江大学   | medium          | 2.0000         |

```sql
select university,difficult_level,
round(count(b.question_id)/count(distinct b.device_id),4) as avg_answer_cnt
from question_practice_detail as b 
inner join user_profile as a 
on a.device_id = b.device_id
inner join question_detail as c 
on b.question_id = c.question_id
group by a.university,c.difficult_level
```



#### 常用函数

**条件函数**(case/if)

`case when else end`

![alt](https://uploadfiles.nowcoder.com/images/20211201/900200538_1638366560048/D2B5CA33BD970F64A6301FA75AE2EB22)

```sql
select 
case 
	when age>=25 then '25岁及以上'
	else '25岁以下' end age_cut,
count(*)
from user_profile
group by age_cut

select 
if(age < 25 or age is null,"25岁以下","25岁及以上") as age_cut,
count(id) as num
from user_profile
group by age_cut
```



查看不同年龄段的用户明细(case--when--else--end)

运营想要将用户划分为**20岁以下，20-24岁，25岁及以上**三个年龄段，分别查看不同年龄段用户的明细情况，

输出：

| device_id | gender | age_cut    |
| --------- | ------ | ---------- |
| 2138      | male   | 20-24岁    |
| 3214      | male   | 其他       |
| 6543      | female | 20-24岁    |
| 2315      | female | 20-24岁    |
| 5432      | male   | 25岁及以上 |
| 2131      | male   | 25岁及以上 |
| 4321      | male   | 25岁及以上 |

```sql
select device_id,gender,
case 
    when age >= 25 then "25岁及以上"
    when age >= 20 then "20-24岁"
    when age < 20 then "20岁以下"
    else "其他" end
    as age_cut
 from user_profile
```



```sql
select code,name,
sum(score) as totalscore,
case 
    when totalscore >= 280 then "A"
    when totalscore >= 250 then "B"
    when totalscore >= 220 then "C"
    when totalscore >= 180 then "D"
    else "E" end 
    as level
from exam as b
join student as a 
on a.id = b.student_id
group by code
order by code
```

#### 合并查询

union 和 union all 

二者的区别是对结果的处理，union 会自动去除，union all 不会去重

```sql
select * from
( select * from t1  order by 字段 )t1 -- 一定要对表重新命名，否则报错 
union 
select * from
( select * from t2  order by 字段 )t2
```

1、现有试卷作答记录表exam_record（uid用户ID, exam_id试卷ID, start_time开始作答时间, submit_time交卷时间, score得分）：

| id   | uid  | exam_id | start_time          | submit_time         | score  |
| ---- | ---- | ------- | ------------------- | ------------------- | ------ |
| 1    | 1001 | 9001    | 2021-09-01 09:01:01 | 2021-09-01 09:41:01 | 81     |
| 2    | 1002 | 9002    | 2021-09-01 12:01:01 | 2021-09-01 12:31:01 | 70     |
| 3    | 1002 | 9001    | 2021-09-01 19:01:01 | 2021-09-01 19:40:01 | 80     |
| 4    | 1002 | 9002    | 2021-09-01 12:01:01 | 2021-09-01 12:31:01 | 70     |
| 5    | 1004 | 9001    | 2021-09-01 19:01:01 | 2021-09-01 19:40:01 | 85     |
| 6    | 1002 | 9002    | 2021-09-01 12:01:01 | (NULL)              | (NULL) |

题目练习表practice_record（uid用户ID, question_id题目ID, submit_time提交时间, score得分）：

| id   | uid  | question_id | submit_time         | score |
| ---- | ---- | ----------- | ------------------- | ----- |
| 1    | 1001 | 8001        | 2021-08-02 11:41:01 | 60    |
| 2    | 1002 | 8001        | 2021-09-02 19:30:01 | 50    |
| 3    | 1002 | 8001        | 2021-09-02 19:20:01 | 70    |
| 4    | 1002 | 8002        | 2021-09-02 19:38:01 | 70    |
| 5    | 1003 | 8001        | 2021-08-02 19:38:01 | 70    |
| 6    | 1003 | 8001        | 2021-08-02 19:48:01 | 90    |
| 7    | 1003 | 8002        | 2021-08-01 19:38:01 | 80    |

请统计每个题目和每份试卷被作答的人数和次数，分别按照"试卷"和"题目"的uv & pv降序显示，示例数据结果输出如下：

| tid  | uv   | pv   |
| ---- | ---- | ---- |
| 9001 | 3    | 3    |
| 9002 | 1    | 3    |
| 8001 | 3    | 5    |
| 8002 | 2    | 2    |

```sql
方法一：
select exam_id tid,
count(distinct uid) uv,
count(exam_id) pv
from exam_record 
group by exam_id
union all
select question_id tid,
count(distinct uid) uv,
count(question_id) pv
from practice_record
group by question_id
order by left(tid,1) desc,uv desc,pv desc

方法二：
select * from 
(select exam_id tid,
count(distinct uid) uv,
count(exam_id) pv
from exam_record
group by tid
order by uv desc,pv desc) a
union all
select * from 
(select question_id tid,
count(distinct uid) uv,
count(question_id) pv
from practice_record
group by tid
order by uv desc,pv desc) b
```



# 计算机网络

## 1. OSI的7层模型和TCP的4层模型

**OSI 的7层模型**

**应用层**：为计算机用户提供服务

**表示层**：数据处理（编码解码、加密解密、压缩解压缩）

**会话层**：管理应用程序之间的会话。

**传输层**：为两台主机进程之间的通信提供通用的数据传输服务。

**网络层**：路由和寻址

**数据链路层**：相邻节点直接的数据通信。

**物理层**：利用传输介质为数据链路层提供支持，实现相邻计算机节点之间的比特流传输。



**tcp 的4层模型**

**应用层**：应用层位于传输层之上，主要提供两个终端设备上的应用程序之间信息交换的服务。它定义了信息交换的格式，消息会交给下一层传输层来传输。我们把应用层交互的数据单元称为报文。【HHTP、FTP、SSH、DNS】

**传输层**：负责向两台终端设备进程之间的通信提供通用的数据传输服务。【TCP**传输控制协议**、UDP**用户数据协议**】

**网络层**：负责为分组交换网上的不同主机提供通信服务。

**网络接口层**：数据链路层和物理层的合体。数据链路层的作用是将网络层交下来的IP数据报封装成帧，在两个相邻节点之间的链路上传送帧。每一帧包含数据和必要的控制信息（同步、地址、差错控制信息等）。物理层是实现相邻计算机节点的比特流传输。

## 2.HTTP和HTTPs

HTTP协议：超文本传输协议，是应用层的协议。以TCP（传输层）作为底层协议，默认端口为80.

HTTP的通信过程：

服务器在80端口等待客户的请求；

浏览器发起到服务器的TCP连接（创建套接字Socket)；

服务器接收来自浏览器的TCP连接；

浏览器与服务器交换HTTP消息；

关闭tcp连接。

HTTPS协议：HTTP的加强版本。HTTPS是基于HTTP的，也是以TCP作为底层协议，并额外使用SSL/TLS作为加密和安全验证，默认端口443.   SSL是指安全套接字协议，SSL3.0被命名为TLS1.0。  

**总结**：

- **端口号** ：HTTP 默认是 80，HTTPS 默认是 443。
- **URL 前缀** ：HTTP 的 URL 前缀是 `http://`，HTTPS 的 URL 前缀是 `https://`。
- **安全性和资源消耗** ： HTTP 协议运行在 TCP 之上，所有传输的内容都是明文，客户端和服务器端都无法验证对方的身份。HTTPS 是运行在 SSL/TLS 之上的 HTTP 协议，SSL/TLS 运行在 TCP 之上。所有传输的内容都经过加密，加密采用对称加密，但对称加密的密钥用服务器方的证书进行了非对称加密。所以说，HTTP 安全性没有 HTTPS 高，但是 HTTPS 比 HTTP 耗费更多服务器资源。

## 3. HTTP1.0和HTTP1.1的对比

1. **连接方式** : HTTP 1.0 为短连接，HTTP 1.1 支持长连接。
2. **状态响应码** : HTTP/1.1中新加入了大量的状态码，光是错误响应状态码就新增了24种。比如说，`100 (Continue)`——在请求大资源前的预热请求，`206 (Partial Content)`——范围请求的标识码，`409 (Conflict)`——请求与当前资源的规定冲突，`410 (Gone)`——资源已被永久转移，而且没有任何已知的转发地址。
3. **缓存处理** : 在 HTTP1.0 中主要使用 header 里的 If-Modified-Since,Expires 来做为缓存判断的标准，HTTP1.1 则引入了更多的缓存控制策略例如 Entity tag，If-Unmodified-Since, If-Match, If-None-Match 等更多可供选择的缓存头来控制缓存策略。
4. **带宽优化及网络连接的使用** :HTTP1.0 中，存在一些浪费带宽的现象，例如客户端只是需要某个对象的一部分，而服务器却将整个对象送过来了，并且不支持断点续传功能，HTTP1.1 则在请求头引入了 range 头域，它允许只请求资源的某个部分，即返回码是 206（Partial Content），这样就方便了开发者自由的选择以便于充分利用带宽和连接。
5. **Host头处理** : HTTP/1.1在请求头中加入了`Host`字段。

## 4. HTTP常见状态码

有1开头、2开头、3开头、4开头、5开头的。

**2开头（成功状态码）**：

- **200 OK** ：请求被成功处理。比如我们发送一个查询用户数据的HTTP 请求到服务端，服务端正确返回了用户数据。这个是我们平时最常见的一个 HTTP 状态码。
- **201 Created** ：请求被成功处理并且在服务端创建了一个新的资源。比如我们通过 POST 请求创建一个新的用户。
- **202 Accepted** ：服务端已经接收到了请求，但是还未处理。
- **204 No Content** ： 服务端已经成功处理了请求，但是没有返回任何内容。

**3开头（重定向状态码）**：

- **301 Moved Permanently** ： 资源被永久重定向了。比如你的网站的网址更换了。
- **302 Found** ：资源被临时重定向了。比如你的网站的某些资源被暂时转移到另外一个网址。

**4开头（客户端错误状态码）**：

- **400 Bad Request** ： 发送的HTTP请求存在问题。比如请求参数不合法、请求方法错误。
- **401 Unauthorized** ： 未认证却请求需要认证之后才能访问的资源。
- **403 Forbidden** ：直接拒绝HTTP请求，不处理。一般用来针对非法请求。
- **404 Not Found** ： 你请求的资源未在服务端找到。比如你请求某个用户的信息，服务端并没有找到指定的用户。
- **409 Conflict** ： 表示请求的资源与服务端当前的存状态在冲突，请求无法被处理。

**5开头（服务端错误状态码）**：

- **500 Internal Server Error** ： 服务端出问题了（通常是服务端出Bug了）。比如你服务端处理请求的时候突然抛出异常，但是异常并未在服务端被正确处理。
- **502 Bad Gateway** ：我们的网关将请求转发到服务端，但是服务端返回的却是一个错误的响应。

## 5、应用层有哪些常见的协议

- http：超文本传输协议，主要为web浏览器与web浏览器之间的通信而设计的。http协议是基于tcp协议的，发送http请求之前首先要建立tcp连接，也就是3次握手。目前http协议大部分都是1.1，在1.1协议里面，默认开启Keep-Alive的，这样的话建立的连接就可以在多次请求中被复用。
- SMTP：简单邮件传输协议，基于tcp协议，用来发送电子邮件。**而接受邮件的协议是POP3协议**。
- POP3/IMAP: 邮件接收的协议
- FTP：文件传输协议，提供文件传输服务，基于TCP实现可靠的传输，使用FTP传输文件的好处就是可以屏幕操作系统和文件存储的方式。
- SSH：安全的网络传输协议，建立在可靠的tcp之上，专为远程登录会话和其他网络服务提供安全性的协议。

```
传输过程： 
 用户*** --http--> 邮件服务器 -----smtp ---> 邮件服务器 ---http ---> 用户*** 
 所以我们呢可以记住：用户向邮件服务器
```



## 6. TCP的三次握手和四次挥手【面试常客】

**time-wait**  **close-wait**

**TCP的三次握手**

- 客户端发送带有SYN标志的数据包到服务端
- 服务端发送带有SYN/ACK标志的数据包到客户端【ACK是为了告诉客户端，服务端接收到的信息就是你发送的信号；SYN是为了建立从服务端到客户端的通信。】
- 客户端发送带有ACK标志的数据包到服务端

**为什么要进行三次握手？**

三次握手的目的其实就是建立可靠的通信信道，双方确认自己与对方的发送和接收是正常的。

- 第一次握手：客户端什么都不能确认，服务端确认对方发送正常，自己接收正常；
- 第二次握手：客户端确认自己接收、发送正常，对方发送、接收正常；服务端确认对方发送正常，自己接收正常；
- 第三次握手：客户端确认自己接收、发送正常，对方发送、接收正常；服务端确认对方发送、接收正常，自己发送、接收正常。

**为什么要四次挥手**：

- 客户端--发送一个FIN，用来关闭客户端到服务端的数据传送；
- 服务端--收到这个FIN，发送一个ACK，确认序号为收到的序号加1。和SYN一样，一个FIN将占掉一个序号。
- 服务端--关闭与客户端的连接，发送一个FIN给客户端
- 客户端--发送ACK报文确认，并将确认序号设置为收到序号加1.

## 7.TCP和UDP的区别

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220717151512950.png" alt="image-20220717151512950" style="zoom:80%;" />

TCP：提供面向连接的服务，在传送数据之前必须先建立连接，数据传送结束后要释放连接。由于TCP要提供可靠的、面向连接的服务，（TCP 的可靠体现在 TCP 在传递数据之前，会有三次握手来建立连接，而且在数据传递时，有**确认、窗口、重传、拥塞控制**机制，在数据传完后，还会断开连接用来节约系统资源）这难以避免要增加许多开销，如确认，流量控制，计时器等。TCP一般用于文件传输、发送和接收邮件、远程登录等场景。

UDP:传送数据之前不需要先建立连接，远地主机在收到UDP报文后，不需要给出任何的确认。虽然UDP不提供可靠的支付，但是在某些情况下却是一种有效的方式，一般用于QQ语音、QQ视频、直播等等。**数据多播，无线连接，复用/分用服务**

# 操作系统

## 1、什么是操作系统

1. **操作系统（Operating System，简称 OS）是管理计算机硬件与软件资源的程序，是计算机的基石。**
2. **操作系统本质上是一个运行在计算机上的软件程序 ，用于管理计算机硬件和软件资源。** 举例：运行在你电脑上的所有应用程序都通过操作系统来调用系统内存以及磁盘等等硬件。
3. **操作系统存在屏蔽了硬件层的复杂性。** 操作系统就像是硬件使用的负责人，统筹着各种相关事项。
4. **操作系统的内核（Kernel）是操作系统的核心部分，它负责系统的内存管理，硬件设备的管理，文件系统的管理以及应用程序的管理**。 内核是连接应用程序和硬件的桥梁，决定着系统的性能和稳定性。

## 2、什么是系统调用

在了解系统调用之前，首先了解用户态和系统态。根据进程访问资源的特点，将进程在系统上的运行分为用户态和系统态。

用户态：用户态运行的进程可直接读取用户程序的数据。

系统态运行的进程或程序几乎可以访问计算机的任何资源。

我们运行的程序基本都是在用户态，如果我们调用操作系统提供的系统态级别的子功能该怎么办呢？这就需要系统调用了。

即**在我们运行的用户程序中，凡是与系统态级别的资源有关的操作（如文件管理、进程控制、内存管理等)，都必须通过系统调用方式向操作系统提出服务请求，并由操作系统代为完成**。

## 3、进程的几种状态？

- 创建：进程正在被创建，尚未到达就绪状态。
- 就绪：进程获得了除了处理器之外的一切所需资源，一旦得到处理器资源即可运行。
- 运行：进程在处理器上运行。
- 阻塞：进程正在等待某一事件而暂停运行如等待某资源为可用或等待 IO 操作完成。
- 结束：进程正在从系统中消失。

## 4、进程之间的通信方式

- 管道/匿名管道：亲缘关系的父子进程、兄弟进程
- 有名管道：为了解决匿名管道没有名字，只能用于具有亲缘关系的进程之间的通信的缺点，提出严格遵循**先进先出**的有名管道。
- 信号：比较复杂的通信方式，用于通知接收进程某个事件已经发生。
- 消息队列：**消息队列克服了信号承载信息量少，管道只能承载无格式字节流以及缓冲区大小受限等缺点。**消息队列是消息的链表，管道和消息队列的通信数据都是先进先出的原则。与管道不同的是，消息队列存放在内核中，只有在内核重启或者显式的删除一个消息队列时，该消息队列才会被删除。
- 信号量：信号量是一个计数器，用于多进程对共享数据的访问，信号量的意图在于进程间同步。
- 共享内存：使得多个进程可以访问同一块内存空间，不同进程可以及时看到对方进程中对共享内存中数据的更新。
- 套接字：在客户端和服务器之间通过网络进行通信。简单的说就是通信的两方的一种约定，用套接字中的相关函数来完成通信过程。

线程之间同步的方式：==互斥量==：只有拥有互斥对象的线程才有访问公共资源的权限，这样可以保证公共资源不会被多个线程同时访问。

==信号量==：它允许同一时刻多个线程访问同一个资源，但是需要控制同一时刻访问此资源的最大线程数量。

==事件==：通过通知的方式保持多线程同步。

## 5、虚拟内存中的页面置换算法

地址映射过程中，若在页面中发现所访问的页面不在内存中，就会发生缺页中断。当发生缺页中断的时候，如果当前内存中并没有空闲的页面，操作系统就必须在内存选择一个页面将其移出内存，以便为即将调入的页面让出空间。用来选择淘汰哪一页的规则叫做页面置换算法，我们可以把页面置换算法看成是淘汰页面的规则。

- **OPT 页面置换算法（最佳页面置换算法）**：所淘汰的页面将是以后永不使用的或是最长时间内不再被访问的页面，可以保证最低的缺页率，但是该算法没有实现。
- **FIFO（First In First Out） 页面置换算法（先进先出页面置换算法）**：总是淘汰最先进入内存的页面，即选择在内存中驻留时间最久的页面进行淘汰。
- **LRU （Least Recently Used）页面置换算法（最近最久未使用页面置换算法）**：LRU算法赋予每个页面一个访问字段，用来记录一个页面自上次被访问以来所经历的时间 T，当须淘汰一个页面时，选择现有页面中其 T 值最大的，即最近最久未使用的页面予以淘汰.
- **LFU （Least Frequently Used）页面置换算法（最少使用页面置换算法）**

# 框架

## 1、Spring框架的模块有哪些？

spring是一个开源的轻量级的java开发框架

**Spring core**：spring的核心模块，提供IOC功能的支持；

**Spring AOP**:面向切面编程

**data access:**包含4个模块，即spring_jdbc(不同的数据库有自己的api，想要操作数据库的话需要调用这些api，屏蔽了调用单个数据库API的独特性)，spring_orm(提供对 Hibernate 等 ORM 框架的支持),spring_oxm( 提供对 Castor 等 OXM 框架的支持),spring_tx(提供对事务的支持)

**spring web**: spring web（提供对web最基本的支持）;spring-webmvc (提供对webmvc的支持)；

**spring test**：junit单元测试

## 2、Spring IOC 和AOP

IOC是一种编程思想，控制反转，控制：创建对象的权力；反转：控制权交给外界环境去做（Spring框架）。这样我们在创建对象的时候，只需要配置好相应的配置文件/注解即可。



AOP是面向切面编程，通过预编译方式和运行期动态代理实现程序功能的统一维护的一种技术。目的是将那些与业务无关、却为业务模块共同调用的逻辑（如日志、安全、缓存、事务等）的代码封装起来。

动态代理分为两大类：基于接口的动态代理，基于类的动态代理

基于接口--JDK动态代理

基于类--cglib

## 3、Spring作用域

- 单例模式：唯一的bean实例，Spring中的bean默认都是单例模式
- 原型模式：每次请求都会创建一个新的bean实例
- request：每一次http请求都会产生一个新的bean，该bean仅在当前http request下有效
- session：每次来自新session的http请求都会产生一个新的bean，该bean仅在当前http session有效。

## 4、Spring的bean 的生命周期

![](https://img-blog.csdnimg.cn/20210201210855798.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQ1NjY1MTcy,size_16,color_FFFFFF,t_70)



# ==招聘要求==

==哔哩哔哩==

```
2、熟练掌握JAVA语言，熟练掌握面向对象的分析与设计方法，熟练掌握常见的设计模式，理解OOA/D理念和原则，掌握UML使用方法；
3、 良好的问题解决能力和逻辑思考能力，能够独立解决遇到的各种问题，良好的责任心和团队精神，能够做到及时补位，协助团队解决当前的困难；
4、 熟悉常见的主流框架的使用方法，比如Spring/SpingMVC/MyBatis/Hibernate/Jersey/Spring Boot等；
5、 熟悉常见前端技术框架（如HTML/CSS/JS/ React/vue/angularJS等），具备全栈开发能力，对用户体验和产品研发有经验者优先；
6、 熟练使用GIT版本管理工具并且理解其版本管理的理念和原则；
7、 热衷于追求代码的整洁优雅和高效实现，了解常见的代码编写规范（JAVADOC/Google code Style/阿里编码规范等）；
8、 熟悉常见的中间件、分布式解决方案及其原理：分布式缓存Redis、SOA、消息中间件，负载均衡、连接池等；
```

美团

```
1、本科学历，计算机相关专业，扎实的计算机专业基本功，强大的写码能力，3年以上开发经验；
2、熟悉Java 及面向对象设计开发，熟悉常见设计模式，对部分 Java 技术有深入研究，研究过优秀开源软件的源码并有心得者优先；
3、熟悉 Spring 框架、熟练使用至少一种 ORM 框架如 Hibernate、MyBatis；
4、熟悉MySQL，熟悉数据库相关原理及常用性能优化技术，熟悉 NoSQL的原理、使用场景及限制；
5、掌握http 协议、搜索引擎、MQ、jvm 调优、序列化、nio、RPC 调用框架等，并有相关实践经验；
6、参与过大型复杂分布式系统设计开发，对高并发、高可用、高性能以及大规模数据处理有实际经验，拥有和工作年限相称的广度和（或）深度；
7、具有较好的沟通能力，思路清晰、善于思考，能独立分析和解决问题，具备良好的团队合作精神；
8、有良好的自驱力和学习能力，对解决具有挑战性问题充满激情
```

Zoom(合肥)

```
岗位职责：
1. 负责Zoom产品线Java后端开发；
2. 根据项目计划，按时提交高质量代码，完成开发任务；
3. 深入理解业务需求，参与产品的方案讨论和相关的技术调研，完成系统的设计，开发或代码重构，并持续对系统进行优化；
4. 解决开发过程中和线上的技术问题。
任职要求：
1. 计算机相关专业本科及以上学历，5年以上Java开发经验；
2. Java基础扎实，深入理解IO、多线程、集合等基础框架和JVM原理，深入理解常用的设计模式及应用场景；
3. 熟练掌握Spring，Spring Boot，Spring Cloud，MyBatis等流行开源框架的使用，深入了解其原理和实现机制；
4. 熟练使用Linux，Nginx，Tomcat等进行开发和调优；
5. 掌握MySQL数据库设计和性能调优，熟悉DynamoDB，MongoDB等NoSQL数据库；
6. 熟悉Memcached，Redis，Kafka，ES等中间件的使用；
7. 具备良好的沟通表达和团队协作能力，积极主动，执行力强，责任心强；
8. 具备英文邮件、文档读写能力，适应全英文工作环境；具备英文流利沟通能力是加分项。

1、本科及以上学历，计算机、数学、通信、电子信息等理工科专业优先，CET-4及以上；
2、熟悉Linux系统，熟悉Java语言，熟悉HTTP协议和Servlet规范，了解Spring、SpringMVC、Mybatis 等Java开源框架；
3、了解数据库设计，了解Redis，MySQL，MongoDB基本使用；
4、对于Java基础技术体系（包括JVM、类装载机制、多线程并发、IO、网络）有一定的掌握和应用经验；
5、有互联网行业高并发、高稳定可用性、高性能、分布式、微服务、大数据处理相关的实习、开发设计经验者优先；
6、具备良好的理解、沟通、思考能力，主动学习、热爱技术，有团队协作精神。
```

中国电信

```
工作职责
﻿1、负责软件项目的详细设计、编码、测试、实施；
2、参与平台整体的架构设计与实现；
3、独立负责设计及实现系统核心模块，解决开发中遇到的各种问题；
4、解决软件维护、运营过程中各种技术问题；
5、确保程序开发的高质量，高可用性，并记录相关开发设计文档。
任职要求
﻿1、3年以上业务管理系统开发经验；
2、精通Java语言及常规开源组件框架（spring，mybatis等），熟悉JVM；
3、精通关系型数据库应用，mysql、oracle等，熟悉数据库各类优化手段；
4、熟练使用各类中间件，如redis、kafka、rabbitmq、es、阿波罗等；
5、熟悉微服务系统框架，对微服务组件原理有一定了解；
6、熟悉项目开发的各个流程，如版本管理，持续集成等；
7、乐于学习和分享新知识，有强烈的责任心和团队合作精神，对代码有追求，熟悉各类设计模式，并运用于工作中
```

==趋势科技==

```
方向一：SaaS 产品开发，熟练掌握 Docker 化的开发和部署，对AWS/Azure/阿里云有一定的了解者优先；
方向二：Android 开发，熟悉OS内核或者Android框架者优先

1.本科、研究生及以上学历，计算机，软件等相关专业；
2.自我驱动，具有优秀的沟通理解能力、学习能力以及团队协作精神；
3.精通Java编程语言，编程基础扎实，有良好的的编码习惯；
4.扎实的数据结构和算法基础，熟悉常用的设计模式和面向对象设计；
5.熟练掌握MySQL/PostgreSQL或任意一个NoSQL；
6.熟悉 SOA 架构理念、实现技术；
7.熟悉常见设计模式，熟练掌握 Spring、SpringMVC，myBatis 等框架；
8.能够熟练地读写英文论文和文档。
```

最右

```
职责
  •  负责最右后端业务的需求和架构开发
  •  保障最右各个系统承受不断增长的用户请求
  •  应对高并发的服务压力和海量数据的分析和处理
要求
  •  熟悉C++/Java/go等至少一门语言
  •  熟悉MySQL/Mongodb等数据库技术
  •  扎实的算法和数据结构功底
  •  熟悉常见设计模式
  •  熟悉unix/linux操作系统
  •  能自驱的学习最新的技术
加分项
  •  有独立个人网站、博客
  •  参与开源社区或项目
  •  能写出优雅简洁高效的代码
```

滴滴出行

```
岗位要求
1. 本科及以上学历优先，计算机相关专业；
2. 酷爱计算机以及互联网技术，热衷于解决挑战性的问题；
3. 具备扎实的编程功底，熟悉数据结构和算法，熟悉常用的设计模式；
4. 掌握java语言，熟悉常用的开发框架；
5. 热衷于数据库技术，能够熟练编写Sql脚本；
6. 具备较强的责任心，团队合作精神以及优秀的分析问题和解决问题的能力；具有较好的学习能力、思考能力、执行力、抗压力，积极主动；
7. 有互联网项目经验，有高可用、高并发经验以及spring、mysql、redis、mq、dubbo等经验优先。
```

用友

```
岗位要求
1、统招全日制硕士及以上学历，计算机、软件工程等相关专业； 
2、精通Java语言及J2EE体系结构，掌握面向对象、反射、多线程等基础知识，熟悉JVM调优、性能问题分析的方法；
3、掌握Spring、SpringMVC、MyBatis等开源框架，熟悉SpringCloud微服务技术栈及IoC、AOP、事务等核心组件； 
4、熟悉MySQL、Oracle等传统数据库原理，熟悉SQL调优和数据库性能优化方案，了解各种NoSQL的特性和使用场景； 
5、有良好的分析设计能力和表达沟通能力，以及较强的学习能力和自我驱动能力，具备较强的创新意识。
```

远景

```
1、硕士及以上学历，计算机或软件工程他，或相关专业方向

2、熟练掌握数据结构和常用算法；

3、 对Java语言特性有深入了解，如多线程并发编程，集合框架等；

4、熟悉数据库索引机制，对Rdb,Mongodb,Redis,Hbase等了解其中一种或多种；

5、熟悉Java Web开发技术，如Spring, JPA, MyBatis, JMS, REST WebService等；

6、了解分布式和hadoop等技术。

优秀团队合作精神，良好的沟通和抗压能力。
```



# 题目合集

## 蔚来提前批

n*m的矩阵，然后有一个长度为L的子方阵，该方阵的价值是4个角数字之和。现在想求价值最大的子方阵的价值。

```java
public class Main01 {
    public static int getRes(int[][] arr){
        int n = arr.length;
        int m = arr[0].length;
        int len = Math.min(m, n);
        int res = Integer.MIN_VALUE;
        for (int l = 2; l <= len ; l++) {//步长
            for (int i = 0; i <= n-l; i++) {
                for (int j = 0; j <= m-l; j++) {
                    int i1 = arr[i][j];
                    int i2 = arr[i][j+l-1];
                    int i3 = arr[i+l-1][j];
                    int i4 = arr[i+l-1][j+l-1];
                    res = Math.max(i1 + i2 + i3 + i4, res);
                }
            }
        }
        return res;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int[][] arr = new int[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                arr[i][j] = sc.nextInt();
            }
        }
        System.out.println(Main01.getRes(arr));
    }
}
```



## **蔚来**

==雪糕的最大数量==

夏日炎炎，小男孩 Tony 想买一些雪糕消消暑。

商店中新到 n 支雪糕，用长度为 n 的数组 costs 表示雪糕的定价，其中 costs[i] 表示第 i 支雪糕的现金价格。Tony 一共有 coins 现金可以用于消费，他想要买尽可能多的雪糕。

给你价格数组 costs 和现金量 coins ，请你计算并返回 Tony 用 coins 现金能够买到的雪糕的 最大数量 。

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/maximum-ice-cream-bars

分析：贪心算法，很简单。想要数量多的话，每次获取价格最低的。

```java
class Solution {
    public int maxIceCream(int[] costs, int coins) {
        Arrays.sort(costs);
        int res = 0,sum =0;
        for (int i = 0; i < costs.length; i++) {
            sum = sum + costs[i];
            if(sum <= coins){
                res += 1;
            }else {
                break;
            }
        }
        return res;
    }
}
```

==最大连续子数组的和平均数==

==最大连续的和==[53. 最大子数组和 - 力扣（LeetCode）](https://leetcode.cn/problems/maximum-subarray/)

给你一个整数数组 nums ，请你找出一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

子数组 是数组中的一个连续部分。

示例 1：

输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length,res = Integer.MIN_VALUE;
        int[] dp = new int[n];//以i为结尾最大的子数组和
        dp[0] = nums[0];
        if(n > 1){
            for (int i = 1; i < n; i++) {
                dp[i] = Math.max(dp[i-1]+nums[i],nums[i]);
                res = Math.max(dp[i],res);
            }
        }
        for (int i = 0; i < n; i++) {
            res = Math.max(res,dp[i]);
        }
        return res;
    }
}
```

给你一个由 `n` 个元素组成的整数数组 `nums` 和一个整数 `k` 。

请你找出平均数最大且 **长度为 `k`** 的连续子数组，并输出该最大平均数。【滚动数组】

```
输入：nums = [1,12,-5,-6,50,3], k = 4
输出：12.75
解释：最大平均数 (12-5-6+50)/4 = 51/4 = 12.75
```

```java
public double findMaxAverage(int[] nums, int k) {
        int sum = 0;
        int n = nums.length;
        for (int i = 0; i < k; i++) {
            sum += nums[i];
        }
        int res = sum;
        for (int i = k; i < n; i++) {
            sum = sum - nums[i-k] + nums[i];
            res = Math.max(res, sum);
        }
        return 1.0 * res / k;
    }
```

==最大连续平均数==

方法一：滑动数组【肯定是对的，但可能会超时】

```java
public double getMaxAve(int[] nums){
        double res = 0;
        int n = nums.length;
        for (int k = 1; k < n+1; k++) {
            res = Math.max(findMaxAverage(nums, k), res);
        }
        return res;
    }
public double findMaxAverage(int[] nums, int k) {
        int sum = 0;
        int n = nums.length;
        for (int i = 0; i < k; i++) {
            sum += nums[i];
        }
        int res = sum;
        for (int i = k; i < n; i++) {
            sum = sum - nums[i-k] + nums[i];
            res = Math.max(res, sum);
        }
        return 1.0 * res / k;
    }
```

方法二：动态规划

用一个二维数组存储和  和 数字【不知道能不能通过测试】

```java
public double getMaxAve(int[] nums){
    int n = nums.length;
    int[][] dp = new int[2][n];
    dp[0][0] = nums[0];
    dp[1][0] = 1;
    if(n > 1){
        for (int i = 1; i < n; i++) {
            dp[0][i] = Math.max(dp[0][i - 1] + nums[i], nums[i]);
            dp[1][i] = dp[0][i - 1] + nums[i] > nums[i] ? dp[1][i - 1] + 1 : 1;
        }
    }
    double res = 1.0*dp[0][0]/dp[1][0];
    for (int i = 1; i < n; i++) {
        res = Math.max(res, 1.0 * dp[0][i] / dp[1][i]);
    }
    return res;
}
```

**总结**

控制台的输入

1.输入字符串,换行输入。

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220712204518159.png" alt="image-20220712204518159" style="zoom:50%;" />

```java
import java.util.*;
public static void main(String[] args){
    Scanner sc = new Scanner(System.in);
    while(sc.hasNext()){
        String s1 = sc.nextLine();
        String s2 = sc.nextLine();
    }
}
```

2.接收一个正浮点数

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220712205357586.png" alt="image-20220712205357586" style="zoom: 80%;" />

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        double num = sc.nextDouble();
    }
}
```

3.接收一个int型的整数

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220712210029977.png" alt="image-20220712210029977" style="zoom:80%;" />

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int num = sc.nextInt();
    }
}
```

接收多个int类型的整数，输入包括两个正整数a,b(1 <= a, b <= 1000),输入数据包括多组。

输入：

```
1 5
10 20
```

输出：

```
6
30
```

```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()){
            int a = sc.nextInt();
            int b = sc.nextInt();
            System.out.println(a+b); 
        }
    }
}
```



4.接收一个字符串和整数k

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220712211454541.png" alt="image-20220712211454541" style="zoom:80%;" />

```java
import java.util.*;
public class Main{
public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        int k = sc.nextInt();
	}
}
```



```java
//带while判断效率会变慢，我也不知道为什么。
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()){
            String s1 = sc.next();
            int k = sc.nextInt();
            System.out.println(s1.substring(0,k));
        }
    }
}
```

```java
import java.util.*;
public class Main{
    public static String getS(String s,int k){
        return s.substring(0,k);
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        int k = sc.nextInt();
        System.out.print(Main.getS(s,k));
    }
}
```

5.输入数组

<img src="C:\Users\86188\AppData\Roaming\Typora\typora-user-images\image-20220712213506891.png" alt="image-20220712213506891" style="zoom:80%;" />

```java
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int k = sc.nextInt();
        int[] nums = new int[n];
        for(int i = 0;i<n;i++){
            nums[i] = sc.nextInt();
        }
    }
}
```



```java
import java.util.*;
public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int k = sc.nextInt();
        int[] nums = new int[n];
        for(int i = 0;i<n;i++){
            nums[i] = sc.nextInt();
        }
        Arrays.sort(nums);
        for(int i = 0 ;i<k;i++){
            System.out.print(nums[i]+" ");
        }
    }
}
```

6.输入二维数组

```java
public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int m = sc.nextInt();
        int[][] arr = new int[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                arr[i][j] = sc.nextInt();
            }
        }
    }
```

