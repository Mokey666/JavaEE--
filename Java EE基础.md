# Java EE基础

1. ### JDK&JRE&JVM

   - JDK：JDK相当于一个工具包，为我们提供了开发Java程序的工具。JDK中包含着JRE。
   - JRE：JRE则相当于一个API，为我们提供了核心类库，以及运行环境。
   - JVM：是Java跨平台的核心，它可将代码翻译成对应OS可以识别的机器码。

2. ### 基本数据类型

   - 数据类类型

     1. int ---Integer

     2. Byte ---byte

     3. boolean ---Boolean

     4. short ---Short

     5. long ---Long

     6. double ---Double

     7. float ---Float

     8. char ---Character

        - 自动装箱和拆箱：

          首先要知道为什么Java会为每一个基础数据类型都提供一个相应包装类的目的，在于将Java的所有东西都抽象成对象，可以更方便的控制和使用。这就是面向对象！

          int -->Integer 装箱      Integer -->int 拆箱

          例子：

          1.boolean是基础数据类型，而Boolean是一个类。
          2.boolean一般存在于栈空间中，而Boolean对象存在堆空间中。
          3.boolean有true和false俩种值，Boolean除了true和false外，还有null。

        - 注意：对于基本数据类型，空所代表的是它的类型的空值（int的空 就是0），而包装类的空是null。

   - 整型
     1. byte 8位 ---  127- (-128)
     2. short 16位
     3. int 32位
     4. long 64位
   - 浮点型
     1. float 32位（单精度浮点型）
     2. double 64位（双精度浮点型）
   - 布尔类型
     
     1.  boolean 8位(true/false)
   - 字符型
     1. char 16位
        - 注意：char本质上是整数型，代表的是字符所对应的ACALL码值。

   ![](C:\Users\侯泽明\Desktop\捕获.PNG)

   

   

   - 注意：运算注意 a+=4 & a = a+4 当a是byte的时候
     - a=a+4会报错：因为a+4会自动转换为int 类型 ，而a是byte类型，所以会报错；而a+=4，+=是一个运算符，所以会自动转换类型为byte/int

3. ### 类型转换

   - 自动类型转换：将小类型的变量赋值给大类型的变量（即所占字节数少的可以转换为占字节数大的类型）

   - 强制类型转换：把大类型的变量赋值给小类型的变量

     强转的语法： 目标类型 变量 =（目标类型）大类型变量; 实例： int i = 223；

4. ### 运算符

   - 单目运算符：+(正) -(负) ++(自增) -- 

   - 双目运算符：= - * / % += -= *= /=

   - 关系运算符：> < = >= <= !=

   - 逻辑运算符：& && | ||

     - 注意：&&(且) 是短路且。若是 &&前的判断为假，就不做后面的判断； || 短路与，若前面的为真，就不做后面的判断.

   - 位运算符：% | ~ ^

   - 位移运算符：>>(带符号左移) << >>>(不带符号左移)

     注意：移位运算符主要使用在对2的次幂进行乘除运算时，为了提高效率使用，所有的负数都用补码移位，存储，原码读值  左移多少位，等同于给原值乘2的多少次幂 	右移多少位，等同于给原值除以2的多少次幂

5. ### 数组

   - 用来容纳同一基本数据类型且大小固定的容器，长度固定，元素类型相同

   - 如果不对数组指定初值，默认初始化为相应数据类型的默认值。

   - 数组的访问，通过下标值，来访问数组里面的元素，当下标值大于或等于数组的长度时，会出现下标越界的错误。

   - 数组的应用：遍历和拷贝，拷贝：Arrays 中提供方法：

     public static int[] copyOf(int[] original, int newLength) :把源数组newlength 的长度拷贝

   - 可变长参数：用数组传递可变长参数
     - 传递规则：
     - 一个方法只能有一个可变长参数，并且这个可变长参数必须是该方法的最后一个参数
     - 在编译器中，实参个数可变的方法是最后被编译成一个数组形参的方法的
     - 在调用方法的时候，如果能够和固定参数的方法匹配，也能够与可变长参数的方法匹配，则选择固定参数的方法
     - 如果要调用的方法可以和两个可变参数匹配（就是另一个方法中也有可变长参数），则出现错误，因为系统不知道调用那个方法

6. ### String

   - 不属于基本类型，也不可被继承，因为被fianl修饰

   - 字符串常量池和不可变（Immutable）字符串

     - 字符串的分配，和其他的对象分配一样，耗费高昂的时间与空间代价。JVM为了提高性能和减少内存开销，在实例化字符串常量的时候进行了一些优化。为了减少在JVM中创建的字符串的数量，字符串类维护了一个字符串池，每当代码创建字符串常量时，JVM会首先检查字符串常量池。如果字符串已经存在池中，就返回池中的实例引用。如果字符串不在池中，就会实例化一个字符串并放到池中。Java能够进行这样的优化是因为字符串是不可变的，可以不用担心数据冲突进行共享。

   - String & StringBuffer & StringBuilder

     1. String的添加字符串的方式：

        - +号

          - 相当于：

            String a = "a";
            StringBuilder sb = new StringBuilder();
            sb.append(a).append("b");
            String str = sb.toString();

            由于每次都要创建一个StringBuilder对象，若是循环十万遍就是噩梦。

          - 注意：+号拼接的时候并不是所有情况都被jvm优化成了StringBuilder，只有在字符串变量拼接的时候才会优化成StringBuilder，如果是字符串的字面量拼接的时候，并不会用StringBuilder。

        - String的concat方法

          - public String concat(String str) {
                    int otherLen = str.length();
                    if (otherLen == 0) {
                        return this;
                    }
                    int len = value.length;
                    char buf[] = Arrays.copyOf(value, len + otherLen);
                    str.getChars(buf, len);
                    return new String(buf, true);
                }
          - 每次都会创建一个新的String 对象。

        - StringBuffer的append方法

          - ```java
            public AbstractStringBuilder append(String str) {
                if (str == null) str = "null";
                int len = str.length();
                ensureCapacityInternal(count + len);
                str.getChars(0, len, value, count);
                count += len;
                return this;
            }
            ```

        - StringBuilder的append方法

          - 同上

        - 注意：StringBuffer 是线程安全的， StringBuilder不是线程安全的(多线程)，适用于单线程.

     2. String.valueof()和toString()的不同

        - toString():在API文档中是这样说的，返回此对象本身（它已经是一个字符串了！！！）

        - 这个方法是静态的，直接通过String调用，当用Integer.valueof()时，是创建一个String对象

        - ```java
          public static String valueOf(Object obj) {
              return (obj == null) ? "null" : obj.toString();
          }
          public static String valueOf(char data[]) {
              return new String(data);
          }
          ```

   - String的分割

     - String[] split(String sign) ----使用指定的隔离字符进行分离，返回容纳子字符串对象的数组
     - split(String sign,int limit)----根据指定的分隔符对字符串进行拆分，并且限定拆分的次数，总是limit-1次

7. 关键字

   - main：主方法（主线程）

   - this

     - 代表本类当前对象的调用，被隐式地用于引用对象的成员变量和方法

     - 适用范围：这又在本类中才能使用。

     - 使用方式：

       this.属性：能访问类中的所有属性。

       this.方法：不能调用静态方法，因为this代表的是这个类的实例对象。

       this作为返回值对象。

   - super：代表父类对象的引用，于this大同小异

     注意：在调用子类构造器的时候，会先调用父类的在调用子类的。

   - statci：静态修饰符

     1. 静态可以修饰常量，方法，类， 会放到内存区域的方法区（Java8在堆中），属于类变量
     2. 静态属于类所有，使用类名直接访问 类名.静态成员名
     3. 虽然静态成员也可以通过对象调用，但是不建议以这样的形式调用， 会让人**混淆静态和非静态成员**，直接通过类名调用
     4. 静态成员中不可以使用this关键字
     5. 静态只能访问静态的
     6. static 修饰的方法可以被继承，不能被重写
     7. 类成员
        - 静态数据成员：类变量
        - 静态方法：方法的参数仅与参数有关和对象无关，属于类
        - 静态块：用来初始化静态资源（图片，视频，音频）
        - 静态内部类：不依赖外围类的对象

   - final

     可修饰属性，方法和类，分别表示**属性不可变，方法不可覆盖，被其修饰的类不可继承**

     - 类 ：该类不能是抽象类，不能被继承
     - 方法：该方法不能定义成抽象方法，不能被重写
     - 变量：该变量就会被变为常量，用 final 定义常量时使用大写字母，不可改变
     - 对象：final 对象的引用只能恒定指向唯一一个对象

     ###### 注意：final 修饰的属性必须在对象存在时给定值，或者必须在声明时给值或者在构造方法给值

     在声明时给值，产生的对象的该变量的值全部相等并且不能改变，在构造方法中赋值，产生的结果是不同的对象有该变量的不同值并且不能改变

     - 声明常量：static final 类型 常量 = 初始值；
     - static与final联合使用时必须在声明时赋值，因为static在声明是共享的，而且final不可被二次赋值，如果不在初始化时赋初值，则变量的值一直是默认值，并且不会改变
     - 如果在声明时没有赋值，称为空白 final

   - default 关键字

     用于修饰接口中声明的方法，java 8 新特性

     - 特性：被default关键字修饰的方法，必须有方法体，可以为空，也可以被重写

       ```java
       public default void ss(){
       	//可以为空
       };
       public void s21();
       ```

   - null关键字

     1. null 是Java中的关键字,它不属于任何类型,只是一种特殊的值
     2. 可以强转为任何包装器类型，调用静态方法（只能）
     3. 用八大基本类型转换后的null,不可以进行基本类型的运算,否则会出现编译或者运行错误
     4. null==null 返回true,被转换为同种类型的null,都返回true,不同类型直接编译报错
     5. 可以对 String 类型，进行拼接运算

     - 编译器对 null 进行了优化,其实就是实例化StringBuilder,在调用append()方法时对 null 的一个特别处理,当为null时,转化为“null”,最后调用toString()返回一个String对象

   - instanceof 关键字

     通过返回一个布尔值来表明这个对象**是否是这个特定类本身或者是它的子类的一个实例**

     - 语法： result = object instanceof class
     - 参数：
       - Result：布尔类型
       - Object：任意对象表达式
       - Class： 任意已定义的对象类
     - 说明： 如果 object 是 class 的一个实例，则 instanceof 运算符返回 true。如果 object 不是指定类的一个实例，或者 object 是 null，则返回 false

     ###### instanceof 在 Java的 编译状态和 运行状态是有区别的：

     - 在编译状态中，class可以是 object 对象的**父类，本生类，子类** 在这三种情况下Java编译时不会报错
     - 在运行转态中，class可以是object对象的**父类，本生类，不能是子类**，在前两种情况下result的结果为true，最后一种为false，但是class为子类时编译不会报错，运行结果为false

8. 面向对象思想

   1. 面向对象设计的三大特点：继承，封装，多态

      五大原则是"单一职责原则"、"开放封闭原则"、"里氏替换原则"、"依赖倒置原则"、"接口分离原则"

   2. 对象和类的关系：

      类是共同属性和行为的集合

      对象是具有这种属性和行为的实例

      类是对象的抽象化，对象是类的实例化。

   3. 类的高级特性：块，内部类

      - ###### 块：在大括号中的代码

        - 实例块： { //实例块代码 }
          - 实例块是在创建对象之前，默认去访问的代码块，每创建一个对象都会去默认执行，多个实例块按照声明顺序执行
        - 静态块： static { //静态块代码 }
        - 在 main 方法之前执行，类的初始化，如果在执行类时，希望先执行类的初始化动作，可以使用 static 定义一个静态块
        - 同步块：synchronized(class对象){ }
        - fianlly 块： finally{ }

        ###### 内部类 (Inner Class) 和 外围类，静态内部类 (Static Nested Class)

        - 静态内部类：
          - static，它不依赖于外部类实例被实例 ，new一个静态内部类不需要外部类成员
          - 静态内部类对象的创建：外围类名.内部类名 内部类变量名 = new 外围类类名.内部类的构造方法

        ```
        public class 	OutClass{
        	public static class InnerStaticClass{
        			
        	}
        }
        //创建内部类对象
        OutClass.InnerStaticClass innerclassname = new OutClass.InnerStaticClass();
        ```

        - 内部类：需要在外部类实例化后才能实例化，分为普通内部类，局部内部类，匿名内部类

        ###### 普通内部类：

        - 存在于一个类中的类，它里面可以有类体的所有元素，但是都不能被static修饰，能访问外围类中的所有元素
        - 普通内部类对象创建格式：
          - 外围类名.内部类名 内部类变量名 = new 外围类的构造方法.new 内部类的构造方法

        ###### 局部内部类：

        - 作用在一个方法中的内部类，只能访问其所在方法中 final 所修饰的变量
        - 通过创建外围类的对象，调用外围类的方法，来执行局部内部类的的方法

        ###### 匿名内部类：

        就是没有名字的局部内部类，不使用关键字class, extends, implements, 没有构造方法

        - 使用时：**如果想创建一个类的对象，并且该类只用一次**
          - 类在定义后马上用到
          - 匿名内部类不能有构造方法
          - 内部类不能定义任何静态的成员、方法和类
          - 只能创建匿名内部类的一个实例
          - 一个匿名内部类一定是在 new 的后面，用其隐含实现一个接口或实现一个类
        - 匿名内部类的两种实现方式：
          - 继承一个类，重写其方法
          - 实现一个接口，实现其方法

        ```
        //Object的子类
        new Object() {
            @Override
            void show() {
                System.out.println("show run");                
            }
        }.show();
        
        //创建一个子类对象，没有名字， 创建子类的对象，引用叫obj,大括号为子类类体
        Object obj = new Object() {
          @Override
          void show(){
            System.out.println("show run");
          }
        };
        obj.show();
        ```

   4. 创建对象的五种方式

      ![img](https://raw.githubusercontent.com/likang315/Java-and-Middleware/master/Java_note/2%EF%BC%9A%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1_OOP/%E5%88%9B%E5%BB%BA%E5%AF%B9%E8%B1%A1%E7%9A%845%20%E4%B8%AD%E6%96%B9%E5%BC%8F.jpg)

   5. 访问对象的两种方式

      ###### 1：使用句柄池

      Java堆划分一块内存作为句柄池，reference 中存储就是对象的句柄地址（含有两个地址）

      - 在堆中分配的对象实例数据的地址
      - 方法区的对象类型数据地址

      ###### 2：使用直接指针

      reference 中存储就是在**堆中分配的对象实例数据的地址**；而对象实例数据中需要有这个对象类型数据的相关信息（方法区）

9. 重载、重写

   - 重载

     在同一个类里一个方法只要重名，不重参（类型或者参数数量不同，参数顺序不同）就可以实现重载。一般用于重载构造方法。

   - 重写

     子类继承父类的方法，可以对该方法进行重写。

     - 必须发生在继承的父类与子类之间
     - 重写的方法要保持名称，参数列表完全相同
     - 重写之后访问权限不能缩小，可以变大
     - 重写之后，返回值类型保持不变，可以缩小 但是不能变大
     - 重写的方法不能比被重写方法声明的更广泛的强制性异常

10. 接口、抽象类

    - 抽象类

      用abstract 声明的类，增强代码的可塑性。

    - 抽象类和抽象方法的关系

      - 抽象类中不一定有抽象方法，但是有抽象方法的类一定是抽象类
      - 一个子类继承了一个抽象的父类，要么实现父类中的抽象方法，要么将自己变成抽象类（二选一，必须的）
      - 修饰符abstract(抽象) 注意：
        - 不能修饰常量
        - 不能修饰静态
        - 不能修饰final修饰的方法及类，final不能被重写和继承
        - 只能用来修饰类和方法

    - 接口

      用interface 声明的类，不能被实例化。

      - 意义：为了**解决Java单继承的缺陷**，而出现特殊的抽象类（接口）----是用来被实现的

      - 声明语法：

        - public inteface 接口名称 { 接口体 }
        - 接口体： 静态的常量，抽象方法

      - 注意：接口方法都是public abstract 的

        ​			接口“变量”都是public static final 的，必须赋予初值，否则一直位null。

11. 多态

    父类或接口定义的引用变量可以指向子类或具体实现类的实例对象，而程序调用的方法在运行期才动态绑定，就是引用变量所指向的具体实例对象的方法，而不是引用变量的类型中定义的方法

    - 多态分为
      1. 编译期的多态：由编译器决定的
      2. 运行期的多态：有JVM决定的
    - 方法的重载(overload)：是编译时的多态性（前绑定）
    - 方法的重写(override) （方法的覆盖）：是运行时的多态性（后绑定）
    - 特性：
      - 多态环境下，子父类之间出现同名的属性时，访问父类
      - 多态环境下，访问同名方法时，访问的子类的
      - 多态环境下，访问同名静态的方法时，访问父类
      - 多态环境下，父类不能访问子类新扩展的方法

    -   多态的实现方式：三种

    1. 普通类引用
    2. 抽象类引用
    3. 接口引用

    - 注意：父类不能访问子类新扩展的方法，多态环境下的对象造型

12. 异常处理

    - JVM 在执行代码的过程中若发现了一个异常，则会 new 一个异常对象，并将代码整个执行过程封装到异常对象中来表示错误信息，设置完毕后将该异常抛出，若抛出的语句被 try—catch 包围，则 JVM 会依次检查 catch 中是否有匹配该异常对象，若有则交给 catch 解决否则会将异常抛出当前方法外，由方法的调用者解决

      - 作用：异常处理机制能让程序在错误发生时，按照代码的预先设定的异常处理程序，针对性地处理错误

    - 异常处理的两种方式

      - try/catch/fianlly：将有可能发生异常的语句用try块包裹起来，在catch中捕获异常，避免因未捕获异常导致程序中断。

      - throw/throws：将方法有可能发生的异常“抛”给他的调用者。

        注意：当多个catch捕获不同异常时，这些异常间存在继承关系，那么子类异常要在上，先行捕获，父类异常在下，从上到下开始匹配

      - throw   throws的却别

        throw：在方法体中用于抛异常对象的关键字，当一个方法使用throw抛出异常时，就要在方法上使用throws声明该类异常抛出的类型，以通知调用者解决，RuntimeException（非检查异常） 及其子类异常使用throw抛出时，不强制要求使用throws声明，其他异常都是强制要求的，否则编译不通过

        throws：用在方法的参数列表之后，后跟异常类型列表，仅仅对该方法所出现异常进行抛给调用者，并不处理这些异常 当调用一个含有throws声明异常抛出的方法时，编译器要求上层必须处理该异常，如果是main函数则抛给调用者

      - error exception

        - error（unchecked，运行时的）：是程序无法处理的错误，通常发生于虚拟机自身，表示运行应用程序中比较严重的错误
        - exception（checked，编译时的）：Checked异常是Java特有的，在java设计哲学中，Checked异常被认为是可以被处理或者修复的异常，所以Java程序必须显式处理Checked异常，当我们使用或者出现Checked异常类的时候，程序中要么显式try- catch捕获该异常并修复，要么显式声明抛出该异常，否则程序无法通过编译。

      - finall块

        - 无论try/catch是否捕获异常，最后都会执行finally块。一般用于关闭流之类的清理工作

      - 含 throws 方法的重写原则

        继承父类，重写父类一个含有 throws 异常抛出声明的方法时

        - 可仅抛出父类方法中抛出的部分异常
        - 允许抛出父类方法抛出异常的子类型异常
        - 不能抛出比父类更大的异常，处理不了

      - 10：异常的方法

        - 异常最先发生的地方，叫做异常抛出点
        - printStackTrace()：追踪异常抛出点，方便我们处理异常
        - getMassage() ：显示出错原因，上层调用者可以调用此方法，获取下层的异常信息

13. 序列化和反序列化

    - 序列化：将对象转换位字节序列的过程

    - 反序列化：将字节序列恢复成对象的过程

    - 序列化用途：

      - 实现了数据的持久化：即把对象的字节序列永久地保存到硬盘上，通常存放在一个文件中，例如Session
      - 实现了远程通信：即在网络上传送对象的字节序列，例：两个进程远程通信时，传递对象信息

    - 实现序列化

      必须实现 Serializable 接口或 Externalizable 接口，Serializable 没有方法，只是为了标注该对象是可被序列化的

    - transient :

      用来修饰属性,当被修饰后，对象进行序列化时，该属性值（临时的）被忽略，从而达到瘦身的目的

    - 序列化的ID：

    - Java的序列化机制：通过判断类的serialVersionUID来验证版本一致性的

      在进行反序列化时，JVM会把传来的字节流中的serialVersionUID与相应实体类的serialVersionUID （编译时生成的版本号）进行比较，如果是一致的，反序列化成功，若不一致：反序列化直接抛出序列化版本不一致的异常 即：InvalidCastException

    - 序列化与反序列化的两种方式

      1：若User类仅仅实现了Serializable接口，则可以按照以下方式进行序列化和反序列化

      ObjectOutputStream 采用默认的序列化方式，对User对象的非transient的实例变量进行序列化 ObjcetInputStream 采用默认的反序列化方式，对User对象的非transient的实例变量进行反序列化

      2：若User类实现了Externalnalizable接口，且User类实现其方法

      ObjectOutputStream调用User对象的writeExternal(ObjectOutput out))的方法进行序列化 ObjectInputStream会调用User对象的readExternal(ObjectInput in)的方法进行反序列化

    - 特点

      1. 序列化时，只对对象的状态进行保存，而不管对象的方法
      2. 声明为 static 和 transient 类型的成员数据不能被序列化，因为static代表类的状态，transient代表对象的临时数据
      3. 当一个父类实现序列化，子类自动实现序列化，不需要显式实现 Serializable接口
      4. 当一个对象的成员变量为引用对象，序列化该对象时也把引用对象进行序列化
      5. Java有很多基础类已经实现了serializable接口，比如String,Collection等

    - 注意：通过序列化和反序列化能实现对象的深克隆。

14. 集合

    - ![Framework.png (1262Ã521)](https://raw.githubusercontent.com/likang315/Java-and-Middleware/master/Java_note/5%EF%BC%9A%E6%B3%9B%E5%9E%8B%EF%BC%8C%E9%9B%86%E5%90%88%EF%BC%8CMap/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/Framework.png)

    - List + Set + Queue

      - List：序列，可以包含重复元素，提供了按索引方式访问

      - Set： 集合，不包含重复的元素

      - Deque：双向队列，Queue 的子接口

      - list

        - Vector

          - ​	数组序列，Vector 线程安全，加了同步锁，效率低

          - 扩容机制：

            初始容量为10 ，就是根据 capacityIncrement（容量增长因子）确认扩容大小的，**若capacityIncrement = 0 则扩大一倍，否则在原来容量的基础上加上 capacityIncrement** ，当然这个容量的最大范围为 Integer.MAX_VALUE 即，2^32 - 1，所以 Vector 并不是可以无限扩充的

        - ArrayList是顺序表的体现，底层用数组实现。

          - 扩容机制

            ​	构造方法默认生成的空数组，并且第一次添加数据时，数组的容量会**从0扩容成10，而后的数组扩容按照当前容量的1.5倍进行扩容**，初始容量可以指定，但是扩容方式不可以

        - LinkedList是链表的体现，使用双向链表实现。（链表的三种形式：单向链表、双向链表、循环链表）

        - Stack是Vector的子类，而Vector实现了`List<E>`接口；是栈结构的代表。

      - Queue

        - 队列Queue直接继承自Collection接口，是队列结构的代表，使用链表结构实现。

      - Set

        - 直接继承自Collection接口，HashSet内部使用HashMap实现；

        - 特点是无序但是不包含重复的元素；

        - 元素存放方式为散列存放，即通过计算hash值存放元素。

        - Class HashSet ：散列集

          ​	元素唯一，因为Map.key 唯一，但不有序，线程不安全类

        - Class LinekdHashSet

          ​	继承 HashSet，源码更少、更简单，唯一的区别是LinkedHashSet 内部使用的是 LinkedHashMap，这样做的意义就是LinkedHashSet中的元素唯一，而且有序

        -  TreeSet：树集

          ​	保证 Set 集合的**元素唯一, 而且有序（元素值大小有序）**，底层是 TreeMap，元素被排序后放入该容器元素的类，必须实现 Comparator ，因为在元素进行排序时需要按照此原则本质是一个 TreeMap

        - 

      - Map

        - Map单独为一个接口，HashMap是基于哈希表的对Map接口的实现，而哈希表的底层数据结构是数组和链表；

        - 特点是能够根据key快速查找value；键必须唯一，put一个键相同的值时该键会被更新，即同一个键只能映射到一个值。

        - 键值对以Entry类型的对象实例存在（注：Entry是Map接口中定义的内部接口）

        - Class HashMap<K,V>：

          ​	基于哈希表的 Map 接口的实现类，非线程安全的类，并且不保证映射的顺序，但是查找高效，允许 null 值 和 null 键的存在

          1：实现原理

          - JDK1.7：数组+链表
          - JDK1.8：数组+链表+红黑树，引入红黑树来提高查找效率
          - 对 null健做了特殊处理，放在table[0]处

        - hash冲突

          ​	通过 key的 hashCode() 值，再进行位与运算产生分布相对均匀的位置，如果存储的对象对多了，就有可能不同的对象所算出来的hash值是相同的，这就出现了所谓的 hash 冲突

        - HashMap 底层是通过链表来解决hash冲突的，**拉链法（桶的深度）** ，开放地址法，再哈希法

        - 为什么要引入红黑树

          ​	因为之前hashmap底层结构是数组加链表，但是当数据大到一定程度的时候，用链表存储也比较长，难以查询，红黑树的查找效率高，相当于二分

        - 什么时候用红黑树什么时候用链表

          - 在桶元素（桶的深度）大于等于8个并且表长超过 64 会将链表转化为红黑树（两个条件），当红黑树中元素小于6个时、会将红黑树转化为链表
          - 因为红黑树需要进行左旋，右旋操作， 而单链表不需要，如果元**素小于8个**，查询成本高，新增成本低，如果**元素大于8个**，查询成本低，新增成本高

        

        

        - LinkedHashMap<K，V>：

          ​	为了解决 HashMap 不保证映射顺序的（无序）问题，迭代顺序

          - LinkedHashMap 是在 HashMap 的基础上维护了一个双向链表保证有序的HashMap，每次 **put 进来 Entry映射关系，除了将其保存到哈希表中对应的位置上之外，还会将其插入到双向链表的尾部**，内部类额外增加的两个属性来维护的一个双向链表**：before、After **

15. 反射机制

    - Java 反射机制

      - 在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法，对于任意一个对象，都能够调用它的任意方法和属性，这种动态获取类的信息和动态调用对象方法的功能称为 Java 的反射机制

      - 想获取一个类这些信息，就必须先获取到该类的字节码文件对象，即：Class对象

    - 获取 Class 对象的方式 (3种) ：

      - Class 对象是在加载类时，由 Java 虚拟机通过调用类加载器中的 defineClass() 自动构造的

        1. 通过类的静态属性，JVM 使用类装载器，将类装入内存，不做类的初始化工作，返回 Class 的对象

           ​	类.class

        2. 通过 Object 方法中，对类进行初始化工作

           对象名.getClass( ) ;

          3.	通过Class类中 forName (String className) ，装入类，并做类的静态初始化，返回 Class 的对象

        ​		Class.forName( 完全限定类名 )；

    - 反射的应用

      1. Spring IOC 通过反射实现的
      2. 通过反射越过泛型检查
      3. 动态的调用方法，或者修改其属性值
         - 使用 getDeclaredMethod（）获取方法, invoke（）调用

    - 反射的作用

      1. 动态地创建类的实例，将类绑定到现有的对象中
      2. 应用程序需要在运行时从某个特定的程序集中载入一个特定的类

16. IO

    - URL："/" ：根目录，"." ：当前目录，"/"：层级的分隔符，默认路径就是当前路径

    - 流：字节流（InputStream/OutputStrram）字符流（Reader/Writer）

    - 1：Java.io 包中 阻塞型 IO

      2：Java.nio 包中的非阻塞型IO，通常称为 New IO

      IO 流：把内存中的数据写到磁盘上(输出流) 或者把磁盘上的数据读到内存中的操作（输入流）

    - ![IOæµ.png (1262Ã521)](https://raw.githubusercontent.com/likang315/Java-and-Middleware/master/Java_note/7%EF%BC%9AFile%EF%BC%8CIO%E6%B5%81/photots/IO%E6%B5%81.png)

    - 同步阻塞型IO步骤

      - 封装File对象
      - 选择io对象
      - 加缓冲
      - 进行读写操作
      - 关闭IO

    - InputStreamReader ：在字符流封装了字节流

    - 根据封装的数据将 io 分为：节点流(低级流) + 处理流（高级流）

      - 节点流：真实负责读写数据的流
      - 处理流：封装了节点流的，用来处理数据的，不能独立存在，高级流处理其他流就形成了流的连接

    - 缓冲流

      BufferedInputStream :

      在创建 BufferedInputStream 时，会创建一个内部缓冲区，使用其可以加快读写效率

    - PrintWriter：

      具有自动刷新，换行功能的缓冲字符输出流，内部会创建 BufferedWriter 作为缓冲功能的叠加

    - ### 阻塞IO（Blocking） 和 非阻塞 IO (NonBlocking)

      判断数据是否准备就绪的方式：（IO线程和缓冲区之间）

      ​	读缓冲区有数据，写缓冲区有空闲字节空间

      - #### **阻塞：往往需要等待缓冲区中的数据准备好后才处理其他的事情，否则一直等待在那里**

      - #### **非阻塞：当线程访问数据缓冲区的时候，如果数据没有准备好则直接返回，去处理其他的事情，不会等待**，如果数据已经准备好，读写完也直接返回

    - NIO：同步非阻塞性 IO

      通常将非阻塞IO的（数据没有准备好时）空闲时间用于在其它通道上执行IO操作，所以一个单独的线程管理多个输入和输出通道

    - Channel 机制（通道）

      Channel 是数据源和数据归宿之间通道的抽象，通过通道把数据读入或者到 Buffer

      在NIO中，提供了多种通道对象，而**所有的通道对象都实现了Channel接口**