# 黑马Java基础学习笔记
主要参考资料：

[黑马程序员Java+AI智能辅助编程全套视频教程](https://www.bilibili.com/video/BV1gb42177hm/?spm_id_from=333.337.search-card.all.click&vd_source=5a9892c5685e5b7e1d5cbd33baa8869e)

## Java基础环境配置
java三大平台：javaSE（标准版）、javaEE（企业版）、javaME（小型版）

jdk：java开发者工具包（lts：长期支持版）

jdk文件夹中的bin文件夹里面java.exe为执行工具，javac.exe为编译工具

jdk包含
* jvm：java虚拟机，真正运行java程序的地方
* 核心类库：java自己写好的程序，给程序员自己的程序调用的
* jre：java的运行环境

![](images/1.jpg)

基础开发步骤：1.编写代码（java后缀的源代码文件） 2.编译代码（命令：javac + 程序名.java） 3.运行代码（命令：java + 程序名）

注意：1.文件名称必须与代码中的类名称一致 2.建议代码文件名全英文，首字母大写，满足驼峰模式

### java工程结构

1.project、module、package、class的关系

* 项目是一个完整的软件解决方案，它包含了实现某个特定功能或目标所需的所有代码、配置文件、资源等。就好比一个在线书店，它有用户管理、书籍管理、订单管理等多个功能，整个在线书店系统就是一个项目
* 模块是项目中相对独立的部分，它具有特定的功能，可将项目按功能或业务逻辑划分成多个模块，方便开发和维护。在在线书店项目中，可以把它划分成用户模块、书籍模块、订单模块。用户模块专门处理用户注册、登录、信息修改等操作；书籍模块负责书籍的添加、删除、查询等；订单模块处理订单的创建、支付、取消等
* 包是用来组织类的一种方式，类似于文件夹，可将相关的类放在同一个包中，避免类名冲突，也方便管理和查找。在用户模块中，可以创建以下几个包：
  * com.example.bookstore.user.dao：存放与用户数据访问相关的类，像与数据库交互的类
  * com.example.bookstore.user.service：存放用户业务逻辑的类，例如用户注册、登录的逻辑
  * com.example.bookstore.user.controller：存放处理用户请求的类，比如接收用户登录请求并调用相应的服务
* 类是 Java 程序的基本组成单元，它封装了数据和方法，代表了一个具体的实体或功能。在 com.example.bookstore.user.service 包中，可以有以下类：
  * UserService 类：负责处理用户的业务逻辑，像注册、登录等
  * UserServiceImpl 类：实现 UserService 接口，具体实现注册、登录的方法

2.IDEA常见的四个包的作用
* .idea 包：这个包是 IntelliJ IDEA 用来存储项目配置信息的隐藏文件夹。它包含项目的设置、插件信息、历史记录、版本控制信息等。此文件夹对于开发者来说是不可见的，IDEA 会自动管理这个文件夹中的内容。当工程被导入到其他电脑上的 IDEA 时，这个文件夹也会被导入，以确保项目的配置一致性
* out 包：这个包主要用来存放项目编译生成的文件，包括 class 文件、打包生成的 jar 文件等。当你编译项目时，IDEA 会把编译的结果放在这个目录下。此目录下的内容在构建过程中会被更新，但通常不需要开发者手动管理
* src 包：这是源代码目录，通常包含了项目中所有的 Java 源文件。在 src 目录下，你可以创建多个子包，用来组织不同的功能模块。例如：
  * bean：存放 JavaBean 类，通常被用来封装数据，如模型类
  * dao：存放数据访问对象（Data Access Objects），这些类负责与数据库进行交互，执行增删改查等操作
  * service：存放业务逻辑代码，处理业务流程
  * controller：存放控制器类，负责处理 HTTP 请求，将请求转发到其他模块处理
* web 包：这个包通常用于存放与 Web 有关的资源，如 JSP 文件、HTML 文件、CSS 样式表、JavaScript 文件等。在开发 Web 应用时，这个包会包含 Web 服务器上的静态资源

![](images/2.jpg)
## 基础知识
引用数据类型中类名、变量名建议采用驼峰命名模式，前者首字母大写，后者首字母小写

输入：导包`import java.util.Scanner`，创建对象`Scanner sc = new Scanner(System.in)`，输入：`int age = sc.nextInt()`，输入字符串用:`sc.next()`

导包配置：settings->Auto import->勾选：Add unambiguous imports on the fly和Optimize imports on the fly

+符号做运算符还是连接符？例如：`int a = 5; a + 'a' + "123"`结果为"102123"，也就是能算则算，算不了就连接

逻辑运算符有：`& | ! ^ && ||`

### 数组初始化
```java
String[] names = {"john", "jack"};
double[] scores = new double[8];
String[] names = {
    {"a", "b", "c"},
    {"d", "e", "f"}
};
int [][] nums = new int[6][6];
```

## 面向对象
this是一个变量，可以用在方法中，其值等于当前对象的地址，作用：解决变量名称冲突的问题
```java
public class Person {
    private String name;
    private int age;
    public Person(String name, int age) {
        // 这里的局部变量name和age与成员变量同名
        // 使用this.name和this.age来访问成员变量
        this.name = name; 
        this.age = age; 
    }
    public void introduce() {
        System.out.println("我叫" + name + "，今年" + age + "岁。");
        // 这里的name和age虽然没写this，但默认就是访问成员变量
    }
}
```
### 封装
如何隐藏(private有关变量和方法）、如何暴露（可以使用get、set方法进行合理暴露）。自动生成getter、setter？在IDEA中：右键-->generate-->getter and setter

实体类javabean：1.成员变量全部为私有、并提供public修饰的getter/setter方法 2.类中需要提供一个无参数构造器、有参数构造器可选，一般这种类只负责对数据的存储，对数据的操作，可以单独使用其它的类来进行处理

static修饰的变量（静态变量or类变量）在计算机中只有一份、会被类的全部对象共享，建议用类访问而不是实例访问
```java
// Counter.java
public class Counter {
    // 用static修饰count变量，使其成为静态变量，属于类，被所有对象共享
    public static int count = 0; 

    public Counter() {
        // 每次创建Counter对象，count就自增1
        count++; 
    }
}
// Main.java
public class Main {
    public static void main(String[] args) {
        Counter counter1 = new Counter();
        Counter counter2 = new Counter();
        System.out.println("对象创建个数: " + Counter.count); 
    }
}
```
静态方法：如果一个方法只是为了完成一项功能，而不需要直接访问对象的数据，则定义为静态方法，应用场景：工具类（***Util），可以提高代码复用性，工具类没有创建对象的需求，建议将其构造器进行私有。
注意事项：1.静态方法中可以直接访问静态成员，不可以直接访问实例成员 2.实例方法中既可以直接访问静态成员，也可以直接访问实例成员 3.实例方法中可以出现this关键字，静态方法中不可以出现this关键字
```java
// ArrayUtils.java
public class ArrayUtils {
    // 静态方法：判断数组中的元素是否都为偶数
    public static boolean allEven(int[] arr) {
        for (int num : arr) {
            if (num % 2 != 0) {
                return false;
            }
        }
        return true;
    }
}
// Main.java
public class Main {
    public static void main(String[] args) {
        int[] arr1 = {2, 4, 6, 8};
        int[] arr2 = {2, 3, 4, 6};

        // 直接使用类名调用静态方法
        boolean result1 = ArrayUtils.allEven(arr1);
        boolean result2 = ArrayUtils.allEven(arr2);

        System.out.println("arr1 中的元素是否都为偶数: " + result1);
        System.out.println("arr2 中的元素是否都为偶数: " + result2);
    }
}
```
### 继承

![](images/3.jpg)
权限修饰符：

* private：只能在本类内部访问
* 缺省：可以在本类内部、同一个包中的其它类中访问
  ![](images/4.jpg)
* protected：本类、同一个包中的类、子孙类中
* public：任意位置

super：可以强制访问父类变量/方法

方法重写：1.方法名称、形参列表必须和被重写方法相同 2.子类重写父类方法时，访问权限必须大于等于父类该方法的权限  3.私有方法、静态方法不能被重写  4.最好在重写的方法上加上重写校验标志：`@Override`  5.返回值类型相对于被重写的范围更小，或者类型相同。常见的场景有：子类重写Object类的toString方法，以适应对象内容，如下图所示
![](images/5.jpg)

this(...)可以调用该类的其它构造器，如下图所示
![](images/6.jpg)

### 多态
![](images/7.jpg)

多态的好处：1.多态形势下，右边对象是解耦合的，更便于扩展、维护  2.定义方法时，直接使用父类的形参，可以接受一切子类对象，扩展性更强、更便利，如下图
![](images/8.jpg)

多态下不能调用子类的独有功能，一种思路是强制转换，具体如下图所示
![](images/9.jpg)

了解--lombok技术
## 高级面向对象
final：修饰类-->不能再被继承  修饰方法-->不能被重写  修饰变量-->有且能被赋值一次

final修饰基本类型的变量，变量存储的数据不能改变；final修饰引用类型的变量，变量存储的地址不能被改变

常量：使用static final修饰的成员变量；作用：常用于记录系统的配置信息，一般使用大写英文、单词间用下划线连接；代码可读性更好，在程序编译后，常量会被“宏替换”：出现常量的地方会被全部替换成其记住的字面量，使其性能与直接使用字面量性能相同

### 单例设计模式
作用：确保某一个类只能创建一个对象

饿汉式实现步骤：1.把类的构造器私有化  2.定义一个类变量记住类的一个对象  3.定义一个类方法，返回对象

懒汉式实现步骤：1.把类的构造器私有化  2.定义一个静态变量用于存储对象  3.提供一个静态方法，保证返回的是同一个对象
```java
//饿汉式单例
public class A {
    private static A a = new A();
    
    private A() {
        
    }
    public static A getObject() {
        return a;
    }
}
```
```java
//懒汉式单例
public class B {
    private static B b;
    private B() {
        
    }
    public staitc B getObject() {
        if (b == null) {
            b = new B();
        }
        return b;
    }
}
```
### 枚举类
特点：1.枚举类的第一行，只能写枚举类的对象名称，用逗号隔开  2.这些名称，本质是常来，且每个常量都记住了枚举类的一个对象，如下图的反编译案例
![](images/10.jpg)

枚举类都是final类，不能被继承，枚举类都继承java.lang.enum类；枚举类的构造器都是私有的，因此，枚举类对外不可以创建对象；使用枚举类是一种多例设计模式，如果里面只写一个名称，那么就是一种很好的单例设计方法

使用案例
![](images/11.jpg)

### 抽象类
```java
修饰符 abstract class 类名 {
    修饰符 abstract 返回值类型 方法名称(形参列表);
}
public abstract class A {
    public abstract void test();
}
```
特点：1.抽象类中不一定要有抽象方法，有抽象方法的类必须是抽象类  2.类有的成员：成员变量、方法、构造器、抽象类都可以有  3.抽象类最主要的特点：抽象类不能创建对象，仅作为一种特殊的父类，让子类继承并实现  4.一个类继承抽象类，必须重写完抽象类的全部抽象方法，否则这个类也必须定义成抽象类

抽象类的好处：为了更好地使用多态
![](images/12.jpg)

### 模板方法设计模式
提供一个方法作为完成某类功能的模板，模板方法封装了每个实现步骤，但运行子类提供特定步骤的实现

实现：1.定义一个抽象类  2.在里面定义两个方法，一个是模板方法：把共同的实现步骤放里面；另一个是抽象方法：不确定的实现步骤，交给具体的子类实现
![](images/13.jpg)

### 接口
jdk8及之前接口只有常量和抽象方法，接口中定义常量可以省略public static final，定义抽象方法可以省略public abstract不写，默认会加上去

实现类写好之后，可以把光标放在红线上面，使用alt+回车+回车全部重写相关全部重写相关类

接口的好处：弥补了类单继承的不足，一个类同时可以实现多个接口，使类的角色更多，功能更强大，同时让程序可以面向接口编程，程序要可以灵活方便地切换各种业务实现，更利于程序的解耦合
![](images/14.jpg)

接口和抽象类对比：
* 相同点：
  * 都是抽象形式，都可以有抽象方法，都不能创建对象
  * 都是派生子类形式，抽象类是被子类继承使用，接口是被实现类实现
  * 一个类继承抽象类或者实现接口都必须重写完它们的抽象方法，否则自己成为抽象类或者报错
  * 都能支持多态、都能实现解耦合
* 不同点
  * 抽象类中可以定义类的全部普通成员，接口只能定义常量和抽象方法（jdk8之后新增三种方法）
  * 抽象类只能被类单继承，接口可以被类多实现
  * 一个类继承抽象类不能继承其它类，一个类实现了接口还可以继承其它类或者实现其它接口
  * 抽象类体现模板思想，更利于做父类，实现代码复用性（如：io流）
  * 接口更适合做功能的解耦合，解耦合性更强更灵活（如：集合）

### 代码块
静态代码块：static{}类加载时自动执行，只会执行一次，优先加载；作用：完成类的初始化，比如对静态变量的初始化赋值

实例代码块：{}每次创建对象时，执行实例代码块，并在构造器前执行

### 内部类
成员内部类：就是类中的一个普通成员：
```java
public class Outer {
    public class Inner {

    }
}
```
创建对象的格式：外部类名.内部类名 对象名 = new 外部类(...).new 内部类(...);如`Outer.Inner in = new Outer().new Inner()`

特点：1.成员内部类中可以直接访问外部类的实例成员、静态成员  2.成员内部类的实例方法中，可以直接拿到当前外部类对象，格式是`外部类名.this`，一个例子见下面代码
```java
// Outer.java
class Outer {
    private int outerValue = 10;
    
    class Inner {
        private int innerValue = 20;
        
        public void printValues() {
            // 获取外部类实例
            Outer outer = Outer.this;
            
            // 访问外部类的私有成员
            System.out.println("外部类的outerValue: " + outer.outerValue);
            System.out.println("内部类的innerValue: " + this.innerValue);
            
            // 直接通过外部类名.this访问外部成员
            System.out.println("直接访问外部类的outerValue: " + Outer.this.outerValue);
        }
    }
    
    public void createInner() {
        Inner inner = new Inner();
        inner.printValues();
    }
}
// InnerClassExample.java
public class InnerClassExample {
    public static void main(String[] args) {
        Outer outer = new Outer();
        outer.createInner();
    }
}
```
静态内部类
```java
public class Outer {
    public static class Inner {

    }
}
```
创建格式与成员内部类一样，静态内部类可以直接访问外部类的静态成员，不可以直接访问外部类的实例成员

局部内部类：略

匿名内部类：
![](images/15.jpg)

```java
//使用comparator接口的匿名内部类实现对数组进行排序
public class Test {
    public static void main(String[] args) {
        Student[] students = new Student[3];
        students[0] = new Student("name1", 16, 170.1);
        students[1] = new Student("name2", 18, 180.0);
        students[2] = new Student("name3", 19, 174.3);

        Arrays.sort(students, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                return o1.getAge() - o2.getAge();
            }
        });

        System.out.println(Arrays.toString(students));
    }
}
```
### Lambda
使用lambda函数替代某些匿名内部类对象，从而让程序代码更简洁、可读性更好。下面是一个错误示范，lambda并不是可以简化全部的匿名内部类，lambda只能简化函数式接口的匿名内部类
![](images/16.jpg)

什么是函数式接口：有且仅有一个抽象方法的接口，一个例子如下图所示
![](images/17.jpg)

用lambda简化函数式接口：comparator
![](images/18.jpg)

lambda表达式的省略规则：
* 参数类型可以全部省略不写
* 如果只有一个参数，参数类型省略的同时"()"也可以省略，但多个参数不能省略"()"
* 如果lambda表达式中只有一行代码，可以不写大括号，但同时要省略分号";"，如果这行代码是return语句，必须去掉return

### 方法引用

静态方法引用
![](images/19.jpg)

实例方法引用
![](images/20.jpg)

特定类型方法引用：`特定类的名称::方法` 使用场景：如果某个lambda表达式只是调用一个特定类型的实例方法，并且前面参数列表中的第一个参数是作为方法主调，后面的所有参数都是作为该实例方法的输入参数，这时可以使用特定类型的方法引用
![](images/21.jpg)

构造器引用：`类名::new` 如果某个lambda表达式里只是在创建对象，并且"->"前后参数情况一致，就可以使用构造器引用
![](images/22.jpg)

### String

创建字符串：方法一：`String name = "123";`  方法二：调用String类的构造器初始化字符串对象
```java
public String() //创建一个空白字符串对象，不含有任何内容
public String(String original) //根据传入的字符串内容，来创建字符串对象
public String(char[] chars) //根据字符数组的内容，来创建字符串对象
public String(byte[] bytes) //根据字节数组的内容，来创建字符串对象
```
两种创建方式的区别
```java
String t1 = "abc";
String t2 = "abc";
System.out.printlin(t1 == t2);
String t3 = new String("abc");
String t4 = new String("abc");
System.out.println(t3 == t4);
```
String提供的常用方法
```java
public int length() //获取字符串的长度并返回（就是字符的个数）
public char charAt(int index) //获取某个索引位置处的字符返回
public char[] toCharArray() //将当前字符串转换成字符数组返回
public boolean equals(Object anObject) //判断当前字符串与另一个字符串的内容是否一样，若一样，返回true
public boolean equalsIgnoreCase(String anotherString) //判断当前字符串与另一个字符串的内容是否一样（忽略大小写）
public String substring(int beginIndex, int endIndex) //根据开始和结束索引进行子串截取（左闭右开）
public String substring(int beginIndex) //从传入的索引处截取，截取到末尾
public String replace(CharSequence old, CharSequence new) //使用新值取代旧值，返回新的字符串
public boolean contains(CharSequence s) //判断字符串是否包含某一个字符串
public boolean startsWith(String prefix) //判断字符串是否以某个字符串内容开头，若是，返回true
public String[] split(String regex) //把字符串按照某个字符串内容分割，并返回字符串数组回来
```
### ArrayList
```java
public ArrayList() //创建一个空的集合对象
eg：ArrayList<E> objectName = new ArrayList<>();//初始化；E：泛数据类型，只能为引用数据类型
public boodean add(E e) //将指定的元素添加到此集合的末尾
public void add(int index, E element) //在此集合中的指定位置插入指定的元素
public E get(int index) //返回指定索引处的元素
public int size() //返回集合中的元素的个数
public E remove(int index) //删除指定索引处的元素，返回被删除的元素
public boolean remove(Object o) //删除指定的元素，返回删除是否成功
public E set(int index, E element) //修改指定索引处的元素，返回被修改的元素
```
简单例子
```java
ArrayList<String> list = new ArrayList<>();
list.add("java");
list.add("java2");
list.add("java3");
System.out.println(list);//[java, java2, java3]
System.out.println(list.get(0));
System.out.println(list.get(1));
System.out.println(list.get(2));
```
如果想往集合里面放入任意数据类型的元素：`ArrayList list = new ArrayList<>()`

### GUI

java的GUI编程包：
* AWT（Abstract Window Toolkit）：提供了一组原生的GUI组件，依赖于操作系统的本地窗口系统
* Swing：基于AWT，提供了更丰富的GUI组件，轻量级组件，不依赖于本地窗口系统

常用的Swing组件
* JFrame：窗口
* JPanel：用于组织其他组件的容器
* JButton：按钮组件
* JTextField：输入框
* JTable：表格

例子：
```java
public static void main(String[] args) {
    JFrame frame = new JFrame("Simple GUI");
    frame.setSize(400, 300);
    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    JButton button = new JButton("Click Me");
    frame.add(button);
    frame.setVisible(true);
}
```
布局管理器（Layout Manager）它们可以决定组件在容器中的布局方式，避免了手动设置每个组件的位置和大小，从而简化了GUI设计过程
常见的布局管理器：
* FlowLayout
* BorderLayout
* GridLayout
* BoxLayout

GUI编程中，事件的处理是通过事件监听器（Event Listener）来完成，常用的事件监听器对象：
* 点击事件监听器ActionListener
* 按键事件监听器KeyListener
* 鼠标行为监听器MouseListener
* ......

下面是一个使用事件监听器的超级简单例子：

step1.定义事件监听器接口
```java
//监听器接口：声明事件发生时的回调方法
interface MyListener {
    void onEvent(String message);
}
```
step2.定义事件源（触发事件的类）
```java
class Event {
    private MyListener listener;
    //注册监听器
    public void setListener(MyListener listener) {
        this.listener = listener;
    }
    //触发事件的方法
    public void doSomething() {
        //模拟事件发生
        if (listener != null) {
            listener.onEvent("事件触发了");
        }
    }
}
```
step3.使用事件监听器
```java
public class Main {
    public static void main(String[] args) {
        EventSource source = new EventSource();
        //注册监听器（使用匿名内部类）
        source.setListener(new MyListener() {
            @Override
            public void onEvent(String message) {
                System.out.println("收到事件：" + message);
            }
        });
        //触发事件
        source.doSomething();//输出：收到事件：事件触发了！
    }
}
```
事件的几种写法：
* 直接提供实现类，用于创建事件监听对象
* 直接使用匿名内部类对象，代表事件监听对象
* 自定义窗口，让窗口对象实现事件接口

## Java加强
### 异常

异常代表程序出现的问题，如数组越界、除数为0、读取的文件不存在了

java的异常体系：

顶级父类Java.lang.Throwable
* Error：代表系统级别的严重错误，Error是给sun公司自己用的，开发人员不用管
* Exception：代表程序可能出现的问题
  * RuntimeException：运行时异常，该类及其子类，如索引越界
  * 编译时异常：编译阶段就会出现提醒的，如日期解析异常

异常的基本处理：
* 抛出异常throws：在方法上使用throws关键字，可以将方法内部出现的异常抛出去给调用者处理
* 捕获异常try...catch：直接捕获程序出现的异常
  ```java
  try {
      // 监视可能出现异常的代码
  } catch (异常类型1 变量) {
      // 处理异常
  } catch (异常类型2 变量) {
      // 处理异常
  } ...
  ```
异常的作用：
* 用来定位程序的bug
* 可以作为方法内部的一种特殊返回值，以便通知上层调用者，方法的执行问题，如下面的代码
  ```java
  public class ExceptionDemo {
      public static void main(String[] args) {
          try {
              System.out.println(div(10, 0));
              System.out.println("底层方法执行成功");
          } catch (Exception e) {
              e.printStackTrace();
              System.out.println("底层方法执行失败");
          }
      }
      //除数为0时抛出一个编译时异常，而不是返回-1，因为无法判断这个-1是答案还是错误
      public static int div(int a, int b) throws Exception {
          if (b == 0) {
              throw new Exception("除数不能为0");
          }
          int res = a / b;
          return res;
      }
  }
  ```

自定义异常：java无法为这个世界上全部的问题提供异常类代表，如果企业自己的某种问题想通过异常表示，需要自定义异常类，包含运行时和编译时
```java
// 自定义编译时异常（继承Exception）
class InvalidInputException extends Exception {
    public InvalidInputException(String message) {
        super(message);
    }
}

// 使用该异常的类
class Calculator {
    public static int divide(int a, int b) throws InvalidInputException {
        if (b == 0) {
            throw new InvalidInputException("除数不能为零");
        }
        return a / b;
    }
}

// 主类
public class Main {
    public static void main(String[] args) {
        try {
            int result = Calculator.divide(10, 0);
            System.out.println("结果: " + result);
        } catch (InvalidInputException e) {
            System.out.println("错误: " + e.getMessage());
        }
    }
}
```
自定义运行时，把继承Exception变成RuntimeException，此外在divide中，不用手写throws，因为运行时异常会自动抛出

异常的处理方案
* 底层异常层层往上抛出，最外层捕获异常，记录下异常信息，并响应给合适用户观看提示（常用）
* 最外层捕获异常后，尝试重新修复
  ```java
  // 循环直到用户输入有效整数
  while (!validInput) {
      try {
          System.out.print("请输入一个整数: ");
          number = scanner.nextInt();
          validInput = true; // 输入成功，退出循环
      } catch (InputMismatchException e) {
          System.out.println("输入无效！请输入一个整数。");
          scanner.nextLine(); // 清除错误输入
      }
  }
  ```

### 泛型

定义类、接口、方法时，同时声明了一个或者多个类型变量（如：<E>）这种成为泛型类、泛型接口、泛型方法、它们统称为泛型

```java
public class ArrayList<E> {
    ...
}
```
作用：泛型提供了在编译阶段约束所能操作的数据类型，并自动进行检查的能力，这样可以避免强制类型转换以及可能出现的异常

```java
ArrayList list = new ArrayList();
list.add("java");
list.add(123);
list.add(99.9);
list.add('a');
list.add(new Object());

//获取数据
for (int i = 0; i < list.size(); i ++ ) {
    Object rs = list.get(i);
    //不使用泛型的话，在进行转换的时候会出现强制转换异常（比如这里整数转字符串）
    String s = (String) rs;
    System.out.println(s);
}
```

java是强类型语言，事先要统一类型，比如要统一装字符串，那么：`ArrayList<String> list = new ArrayList<String>();`，这样在编译阶段就只能往里面加入字符串的数据，JDK7之后，后面的"String"不用写，只写一个尖括号即可

泛型的本质：把具体的数据类型作为参数传递给变量

泛型类
```java
修饰符 class 类名<类型变量,类型变量,...> {

}
例如：
public class ArrayList<E>{
    ...
}
```
注意：类型变量建议用大写的英文字母，常用的有：E、T、K、V
实例：
```java
public class Box<T> {
    private T content;

    // 构造方法
    public Box(T content) {
        this.content = content;
    }

    // 获取内容
    public T getContent() {
        return content;
    }

    // 设置内容
    public void setContent(T content) {
        this.content = content;
    }

    public static void main(String[] args) {
        // 存储整数的盒子
        Box<Integer> intBox = new Box<>(10);
        System.out.println("Integer Box Content: " + intBox.getContent());

        // 存储字符串的盒子
        Box<String> strBox = new Box<>("Hello, Generics!");
        System.out.println("String Box Content: " + strBox.getContent());

        // 泛型类型检查（编译时）
        // strBox.setContent(123); // 编译错误：无法将Integer类型传递给String类型的Box
    }
}
```
举一个泛型的例子，泛型类通过包装一个ArrayList来实现一个MyArrayList
```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.Objects;
import java.util.function.Consumer;
import java.util.function.Predicate;

public class MyArrayList<E> implements Iterable<E> {
    private final ArrayList<E> list;

    // 构造方法
    public MyArrayList() {
        this.list = new ArrayList<>();
    }

    public MyArrayList(int initialCapacity) {
        this.list = new ArrayList<>(initialCapacity);
    }

    // 添加元素
    public void add(E element) {
        list.add(element);
    }

    public void add(int index, E element) {
        list.add(index, element);
    }

    // 获取元素
    public E get(int index) {
        return list.get(index);
    }

    // 删除元素
    public E remove(int index) {
        return list.remove(index);
    }

    public boolean remove(E element) {
        return list.remove(element);
    }

    // 批量操作
    public void forEach(Consumer<? super E> action) {
        list.forEach(action);
    }

    public boolean removeIf(Predicate<? super E> filter) {
        return list.removeIf(filter);
    }

    // 集合信息
    public int size() {
        return list.size();
    }

    public boolean isEmpty() {
        return list.isEmpty();
    }

    // 迭代器
    @Override
    public Iterator<E> iterator() {
        return list.iterator();
    }

    // 重写 toString
    @Override
    public String toString() {
        return list.toString();
    }

    // 类型安全示例
    public static void main(String[] args) {
        // 创建字符串列表
        MyArrayList<String> stringList = new MyArrayList<>();
        stringList.add("Apple");
        stringList.add("Banana");
        // stringList.add(123); // 编译错误：无法添加 Integer 到 MyArrayList<String>

        // 创建整数列表
        MyArrayList<Integer> intList = new MyArrayList<>();
        intList.add(100);
        intList.add(200);

        // 使用 forEach 和 Lambda
        stringList.forEach(item -> System.out.println("Item: " + item));

        // 删除符合条件的元素
        intList.removeIf(num -> num > 150);
        System.out.println("After remove: " + intList);
    }
}
```
泛型接口
```java
修饰符 interface 接口名<类型变量,类型变量,...>{

}
```
类型变量一般依然用大写英文字母
举一个例子：
```java
// 泛型接口定义（需要创建一个接口文件Container.java）
interface Container<T> {
    void add(T item);
    T get();
    boolean isEmpty();
}

// 字符串容器实现（创建一个类文件StringContainer.java）
class StringContainer implements Container<String> {
    private String value;

    @Override
    public void add(String item) {
        this.value = item;
    }

    @Override
    public String get() {
        return value;
    }

    @Override
    public boolean isEmpty() {
        return value == null;
    }
}

// 整数容器实现（创建一个类文件IntegerContainer.java）
class IntegerContainer implements Container<Integer> {
    private Integer value;

    @Override
    public void add(Integer item) {
        this.value = item;
    }

    @Override
    public Integer get() {
        return value;
    }

    @Override
    public boolean isEmpty() {
        return value == null;
    }
}

// 通用容器实现（创建一个类文件GenericContainer.java）
class GenericContainer<T> implements Container<T> {
    private T item;

    @Override
    public void add(T item) {
        this.item = item;
    }

    @Override
    public T get() {
        return item;
    }

    @Override
    public boolean isEmpty() {
        return item == null;
    }
}

// 使用示例（创建一个类文件GenericInterfaceExample.java）
public class GenericInterfaceExample {
    public static void main(String[] args) {
        // 使用特定类型的容器
        Container<String> stringContainer = new StringContainer();
        stringContainer.add("Hello");
        System.out.println("String Container: " + stringContainer.get());

        // 使用通用容器
        Container<Integer> intContainer = new GenericContainer<>();
        intContainer.add(123);
        System.out.println("Integer Container: " + intContainer.get());

        // 类型安全检查
        // stringContainer.add(123); // 编译错误：无法添加 Integer 到 Container<String>
    }
}
```
泛型方法
```java
修饰符 <类型变量,类型变量,...> 返回值类型 方法名（形参列表）{

}
public static <T> void test(T t) {

}
```
举例子：
```java
public class GenericMethodExample {
    public static <T> T getValue(T input) {
        return input;
    }

    public static void main(String[] args) {
        // 传入整数
        Integer intValue = getValue(10);
        System.out.println("整数值: " + intValue);

        // 传入字符串
        String strValue = getValue("Hello, World!");
        System.out.println("字符串值: " + strValue);

        // 传入布尔值
        Boolean boolValue = getValue(true);
        System.out.println("布尔值: " + boolValue);
    }
}
```
通配符：就是“？”，可以在使用泛型的时候代表一切类型

泛型的上下限：
* 泛型上限：`? extends Car` ？能接受的必须是Car或者其子类
* 泛型下限：`? super Car` ？能接受的必须是Car或者其父类
```java
import java.util.ArrayList;
import java.util.List;

public class GenericMethodWithWildcard {
    // 泛型方法：将源列表中的元素复制到目标列表
    public static <T> void copyList(List<? extends T> source, List<? super T> destination) {
        for (T item : source) {
            destination.add(item);
        }
    }

    public static void main(String[] args) {
        // 创建一个Integer类型的源列表
        List<Integer> integerSource = new ArrayList<>();
        integerSource.add(10);
        integerSource.add(20);
        integerSource.add(30);

        // 创建一个Number类型的目标列表（因为Integer是Number的子类）
        List<Number> numberDestination = new ArrayList<>();

        // 调用泛型方法进行复制
        copyList(integerSource, numberDestination);

        // 打印目标列表
        System.out.println("复制后的目标列表: " + numberDestination);

        // 创建一个Number类型的源列表
        List<Number> numberSource = new ArrayList<>();
        numberSource.add(1.5);
        numberSource.add(2.5);

        // 创建一个Object类型的目标列表（因为Number是Object的子类）
        List<Object> objectDestination = new ArrayList<>();

        // 再次调用泛型方法进行复制
        copyList(numberSource, objectDestination);

        // 打印目标列表
        System.out.println("再次复制后的目标列表: " + objectDestination);
    }
}
```

泛型不支持基本数据类型，只能支持对象类型（引用数据类型），为什么？“泛型擦除”：泛型工作在编译阶段，等编译后泛型就没用了，所有泛型在编译后都会被擦除，所有类型会恢复成Object类型，如过支持基本数据类型，下面代码是错误的，因为Object不能接收一个基本数据类型
```java
ArrayList<int> list = new ArrayList<>();
list.add(123);
```
包装类：就是把基本类型数据包装成对象的类型
| 基本数据类型 | 对应的包装类（引用数据类型） |
|:----:|:----:|
|byte|Byte| 
|short|Short|
|int|Integer|
|long|Long|
|char|Character|
|float|Float|
|double|Double|
|boolean|Boolean|
基本类型的数据包装成对象的方案：
```
public Integer(int value):已过时
public static Integer valueOf(int i)
```
自动装箱：基本数据类型可以自动转换为包装类型
自动拆箱：包装类型可以自动转换为基本数据类型
```java
Integer it1 = 10;
Integer it2 = 10;
Integer it3 = 200;
Integer it4 = 200;
System.out.println(it1 == it2);//true
System.out.println(it3 == it4);//false
//解释：默认情况下，Java 缓存了从-128到127之间的所有Integer对象，这些缓存的对象存储在Integer类内部的一个静态数组中（IntegerCache.cache）。当自动装箱的数值在这个范围内时，直接返回缓存的对象，而不是创建新对象
```
包装类具备的其它功能

1.可以把基本类型的数据转换为字符串类型
```java
public static String toString(double d)
public String toString()
//例子如下
int j = 23;
String rs1 = Integer.toString(j);
System.out.println(rs1 + 1);//231

Integer i2 = j;
String rs2 = i2.toString();
System.out.println(rs2 + 1);//231

String rs3 = j + "";
```
2.把字符串类型转换成基本数据类型
```java
public static int parseint(String s)
public static Integer valueOf(String s)
//例子如下
String str = "98";
int i1 = Integer.parseInt(str);
System.out.println(i1 + 2);

String str2 = "98.8";
double d = Double.valueOf(str2);
System.println(d + 2);
```
