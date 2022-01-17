# JDK选型、安装与配置

## JAVA抽象层
### JVM（JAVA虚拟机）
&JVM有很多组件，最开始用户的代码时通过BAD CODE写成，然后被CLASS LOADER加载，加载完之后就是JVM可以识别的内部数据结构。 
BAD CODE可以被执行，也定义了一些数据的类型。 
JAVA的执行引擎通过ATM接口和最底层的操作系统进行交互。

### JRE（JAVA的执行环境）
JRE和JVM几乎是一体的，但是JRE在组织上包括一些基础的类库，比如java.net可以保护网络，java.io可以保护文件，j.u.c可以帮助构建并发的应用程序，这也是JAVA流行的重要原因。
### JDK（开发工具包）
各种语言都有相应的开发工具包，JDK就是JAVA的开发工具包，里面包含了开发工具。如果需要开发JAVA程序，则需要开发包里面拥有JAVA的编译器。
## “正统”OpenJDK
Hotspot是OpenJDK里面默认的JAVA虚拟机实现。OpenJDK是由JSP这个组织去规划它的路线，进而实现它。在OpenJDK基础上加上Oracle特性就是可以在Oracle官网上下载下俩的Oracle JDK。
第三方厂商也会基于OpenJDK去构建自己的构造，比如自己的发行版，例如亚马逊的Corretto、Azul的Zulu,阿里巴巴也提供了JAVA发行版，在OpenJDK的基础上加上阿里巴巴云原生特性，形成了阿里的Dragonwell。

## JDK选型小结
1. 优先选择OpenJDK
2. Oracle不再免费提供最新的OpenJDk
3. AdoptOpenJDK下的Dragonwell是一个好的替代品。
# JAVA语法基础
## JAVA编程入门
### 初识java开发
定义第一个程序代码  
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```
Java程序是需要经过两次处理后才可以执行的：
（1）对源代码程序进行编译：javac HelloWorld.java，会出现一个HelloWorld.class的字节码文件——利用JVM进行编译，编译出一套与平台无关的字节码文件*.class；
（2）在JVM上进行程序的解释执行：java HelloWorld——解释的即使字节码文件，字节码文件的后缀是不需要编写的。

为了更加方便的理解java程序的主要结构，下面针对第一个程序进行完整的解释：
在java程序开发之中的最基础的单元是类，所有的程序都必须封装在类中执行，类的基本定义语法如下：`[public] class 类名称 {}`  

在本程序中定义的类名称为 “HelloWorld”，而类的定义有两种形式：
`public class 类名称 {}`：类名称必须与文件名称保持一致，一个.java文件只能有一个public class;
`class 类名称 {}`: 类名称可以与文件名称不一致，但是编译后的.class名称class是定义的类名称，要求解析的是生成的.class名称文件；在一个.java文件里面可以有多个class定义，并且编译之后会形成不同的*.class文件。

主方法：主方法是所有的程序执行的起点，并且一定要定义在类之中  
```java
public class HelloWorld {
    public static void main(String[] args){
        //程序的代码由此开始执行
    }
}
```
java的主方法名称定义非常长，主方法所在的类都成为“主类”，所有的主类都将采用public class来定义。

屏幕打印（系统输出）可以直接在命令行方式下进行内容的显示，有两类语法形式:
（1）输出之后追加换行:System.out.println（输出内容）
（2）输出之后不追加换行:System.out.print（输出内容）、ln（line 换行）
### Java基本概念
#### 注释
注释是程序开发中的一项重要组成技术。合理的注释可以使项目维护更加方便，但是很多公司由于技术管理问题，注释不尽合理，使得项目维护非常不便，在人员更换时期非常痛苦，对后续工作造成了很大的困扰。特别是新人在项目维护的时候，发现只有若干行代码，没有一个注释，给新人带来了巨大的工作压力。所以注释是一个非常重要的概念。

Java中注释共有三类：
（1）单行注释：//，即双斜线之后到当前行结尾的内容被注释。
（2）多行注释：/*  ……/，则/ 和/之间的内容被注释掉，可以跨多行注释。
（3）文档注释：/** …/；（文档注释需要很多选项，一般建议通过开发工具控制，因为采取手写的方式较为麻烦。）

#### 标识符与关键字
在任何一个程序之中实际上都是一个结构的整合体，在Java语言里面有不同的结构，例如：类、方法、变量结构等，那么对于不同的结构一定要有不同的说明。那么对于结构的说明实际上就是标识符，是有命名要求的，但是一般都要求有意义的单词所组成的，同时对于标识符的组成在Java之中的定义如下：由字母、数字、下划线、$所组成，其中不能使用数字开头，不能使用Java中的保留字（关键字）。

最简单的定义形式：是用英文字母开头，例如Student_Name、StudentName，而且对于”＄“一般都有特殊的含义，不建议出现在你自己所编写的代码上。

关键字是系统对于一些结构的描述处理，有着特殊的含义。例如public、class等就有特殊含义，这些就是关键字，不可以把它作为标识符使用。

JDK 1.4的时候出现有assert 关键字，用于异常处理上;
JDK 1.5的时候出现有enum关键字，用于枚举定义上;
未使用到的关键字:goto、const; .
有一些属于特殊含义的单词，严格来讲不算是关键字:true、false、null。
### Java数据类型
#### Java数据类型简介
在Java语言之中对于数据类型一共分为两类:
- 基本数据类型：描述的是一些具体的数字单元，例如：1、1.1
    - 数值型：
        - 整形：byte、short、int、long；默认值：0
        - 浮点型：float、double；默认值：0.0
    - 布尔型：boolean；默认值：false
    - 字符型：char；默认值：‘\u0000’
- 引用数据类型：牵扯到内存关系的使用；
    - 数组、类、接口。默认值：null

而本次讨论的主要是基本数据类型，这里不牵扯到复杂的内存关系的匹配操作。每一种数据类型都有每一种类型保存的数据范围

![image-20220117123159277](https://s2.loli.net/2022/01/17/o8a2Wunm3hiG9pB.png)

不同的类型保存有不同范围的数据，但是这里面实际上就牵扯到了数据类型的选择上，这里给出一些使用原则：

- 如果要是描述数字首选的一定是int（整数）、double（小数）；
- 如果要进行数据传输或者是进行文字编辑转换使用byte类型（二进制处理操作）；
- 处理中文的时候最方便的操作使用的是字符char来完成（可选概念）；
- 描述内存或文件大小、描述表的主键列（自动增长）可以使用long；

#### 整型数据

整型数据一共有四种，按照保存的范围由小到大分别是：duet、short、int 、long ，在Java里面任何一个的整形常量（例：10 不会改变）其默认的类型都是int型（只要是整数就是int类型的数据）。

```java
public class JavaDemo {
    public static void main(String[] args) {
        //int 变量名称=常量（10是一个常量，整数类型为int）
        int x = 10;//定义了一个整型变量x
        x = 20;//改变了x的现有内容
        //int型变量*int型变量=int型变量
        System.out.println(x * x);
    }
}
```

10永远不会改变，但是x是一个变量，x的内容是可以发生改变的。

任何的数据类型都是有其可以保存的数据范围的（正常使用下很少会出现此范围的数据）

```java
public class JavaDemo {
    public static void main(String[] args) {
        int max = Integer.MAX_VALUE;//获取int的最大值
        int min = Integer.MIN_VALUE;//获取int的最小值
        System.out.println(max);//2147483647
        System.out.println(min);//-2147483648
        System.out.println("--------------无以言表的分割线------------------");
        //int型变量+int型常量=int型计算结果
        System.out.println(max + 1);//-2147483648
        System.out.println(max + 2);//-2147483647
        //int型变量+int型常量=int型计算结果
        System.out.println(min - 1);//2147483647
    }
}
```

通过此时的执行结果可以发现这些数字在进行处理得时候如果超过了其最大的保存范围，那么将出现有循环的问题，而这些问题在Java中被称之为数据溢出，如果想解决这种溢出，就可以继续扩大使用范围，比int更大的范围是long。

- 在操作的时候预估数据范围，如果返现范围不够就是用更大范围

```Java
public class JavaDemo {
    public static void main(String[] args) {
        //long long变量=int的数值
        long max = Integer.MAX_VALUE;//获取int的最大值
        long min = Integer.MIN_VALUE;//获取int的最小值
        System.out.println(max);//2147483647
        System.out.println(min);//-2147483648
        System.out.println("--------------无以言表的分割线------------------");
        //long型变量+int型常量=long型计算结果
        System.out.println(max + 1);//2147483648
        System.out.println(max + 2);//2147483649
        //long型变量+int型常量=long型计算结果
        System.out.println(min - 1);//-2147483649
    }
}
```

- 除了可以定义long型的变量之外，也可以直接在常量上进行处理，默认的整数常量都是int型，那么可以为他追加字母“L”或者直接使用“long”转换。

```Java
public class JavaDemo {
    public static void main(String[] args) {
        int max = Integer.MAX_VALUE;//获取int的最大值
        int min = Integer.MIN_VALUE;//获取int的最小值
        System.out.println(max);//2147483647
        System.out.println(min);//-2147483648
        System.out.println("--------------无以言表的分割线------------------");
        //int型变量+long型常量=long型计算结果
        System.out.println(max + 1L);//2147483648
        System.out.println(max + 2l);//2147483649
        //int型变量+long型常量=long型计算结果
        System.out.println((long) min - 1);//-2147483649
    }
}
```

现在发现数据类型之间是可以转换的，即：范围小的数据类型可以自动转换为范围大的数据类型，如果反过来范围大的数据类型要转为范围小的数据类型，那么就必须采用强制性的处理模式，同时还需要考虑可能带来的数据溢出。

```java
public class JavaDemo {
    public static void main(String[] args) {
        long num = 2147483649L;//此数据已经超过了int范围,故需要在后面加L
        //int temp = num;//long范围比int范围大，不能够直接转换,不兼容的类型: 从long转换到int可能会有损失
        int temp = (int) num;//-2147483647
        System.out.println(temp);
    }
}
```

程序支持有数据转换处理，但是如果不是必须的情况下不建议这种转换。

在进行整型处理的时候，还有一个byte类型特别需要注意，首先这个类型的范围很小：-128~127

```Java
public class JavaDemo {
    public static void main(String[] args) {
        byte num = 20;
        System.out.println(num);
    }
}
```

正常来讲在Java程序里面20这个数字应该是int型，但是在为byte赋值的时候并没有因为是int型而发生强制类型转换，这是因为Java对byte做了特殊处理，即：如果没超过byte范围的常量可以自动由int变成byte，如果超过了就必须强制转换。

```java
public class JavaDemo {
    public static void main(String[] args) {
        byte num = (byte)200;
        System.out.println(num);//-56
    }
}
```

由于现在200已经超过了byte的范围，所以产生了数据溢出的情况。

#### 浮点型数据

浮点型数据描述的是小数，而在java里面任意的一个小数常量其对应的类型为double，所以在以后描述小数的时候都建议直接使用double进行定义。

