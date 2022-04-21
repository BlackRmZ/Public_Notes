# 数据类型

1. 基本数据类型
   1. 整数类型：（byte[1]，short[2]，int[4]，long[8]）
   2. 浮点类型：（float[4]，double[8]）
   3. 字符型：（char[2]）
   4. 布尔型：（boolean[1]）
2. 引用数据类型
   1. 类：（class）
   2. 接口：（interface）
   3. 数组：（[]）

3. 自动类型转换：
   1. 当Java程序进行赋值或者运算时，精度小的类型自动转换为精度大的数据类型.
   2. byte，short 和 char之间不会相互自动转换
   3. byte，short，char可以进行计算，计算时会先自动将类型转换为int
   4. 自动提升原则：表达式结果的类型自动提升为操作数中最大的类型
4. 强制类型转换：
   1. 强制类型转换将容量大的数据类型转换为容量小的数据类型，可能会造成精度降低或溢出。
   2. char类型可以保存int的常量值，但不能保存int的变量值，需要强转
5. 基本数据类型和String类型的转换
   1. String转基本数据类型：
      - 通过基本数据类型对应的包装类调用`parseXxx()`方法即可
   2. 基本数据类型转字符串：
      - `基本数据类型 + ""`即可

# 运算符

1. %取模，取余
   - **本质公式：`a % b = a - a / b * b`**      注意：公式采用java的计算方式 
   - 拓展：`a % b`  当a是小数时，公式等于：`a - (int)a / b * b`
   - 注意：小数参与运算，得到的结果是近似值，所以判断时不应当用==，应该用实际值和期望值差值的绝对值进行精度判断。可以使用`Math.abs(数据)`来求绝对值
   
2. 复合赋值运算符会进行类型转换

   - 如：

   - ```java
      byte b = 3;
      b += 2;
      等价于：b = (byte)(b + 2);
      b++
      等价于：b = (byte)(b + 1);
      ```
   
3. 自增自减（注意点）

   - 例：`i = i++;`按照运算步骤为：
      1. 由于是`i++`,所以是将自增之前的值赋给左边。先将右边的`i`储存到一个临时变量中。
      2. 然后再进行`i++`的操作
      3. 最后再将临时变量中所储存的值赋给左边的`i`

   - 例：`i = ++i;`
      1. 由于是`++i`所以是将自增后的值赋给左边。先将进行右边`++i`的操作
      2. 然后将`++i`的值储存到临时变量中
      3. 最后再将临时变量中的值赋给左边的`i`


4. 三元运算符

   - 基本语法：`条件表达式 ? 表达式1 : 表达式2;`
      - 运算规则：

         1. 如果条件表达式为true，运算后的结果是表达式1
         2. 如果条件表达式为false，运算后的结果是表达式2


   - 如

      - ```java
        int a = 10;
        int b = 99;
        int result = a > b ? a++ : b--;
        ```


### 进制

1. 二进制：0，1。满2进1。以0b或0B开头。例：`int n = 0b1010;`
2. 十进制：0 - 9。满10进1.
3. 八进制：0 - 7。满8进1.以数字0开头表示。例：`int n = 01010;`
4. 十六进制：0 - 9 及 A（10）-  F（15）。满16进1.以0x或0X开头表示。此处A-F不分大小写。例：`int n = 0x10101;`

##### 进制转换

###### 其它进制转十进制

1. 二进制转十进制：从最低位开始，将每一位上的数提取出来，乘以2的（位数-1）次方，然后求和
2. 八进制转十进制：从最低位开始，将每个位上的数提取出来，乘以8的（位数-1）次方，然后求和

3. 十六进制转十进制：从最低位开始，将每个位上的数提取出来，乘以16的（位数-1）次方，然后求和

###### 十进制转其它进制

1. 十进制转二进制：将该数不断除以2，直到商为0为止，然后将每步得到的余数倒过来，就是对应的二进制。
2. 十进制转八进制：将该数不断除以8，直到商为0为止，然后将每步得到的余数倒过来，就是对应的八进制。
3. 十进制转十六进制：将该数不断除以16，直到商为0为止，然后将每步得到的余数倒过来，就是对应的十六进制。

###### 其它进制互相转换

1. 二进制转八进制：从低位开始，将二进制的每三位一组，转换成对应的八进制数即可。
2. 二进制转十六进制：从低位开始，将二进制每四位一组，转换成对应的十六进制即可。
3. 十六进制转二进制与八进制转二进制为逆向操作

### 位运算

- Java中有7个位运算符（&，|，^，~，>>，<<和>>>）
  - **按位与&**，**按位或|**，**按位异或^**，**按位取反~**
  - 运算规则：
    - **&**：两位全为1，结果为1，否则为0
    - **|**：两位有一个为1，结果为1，否则为0
    - **^**：两位一个为0，一个为1，结果为1，否则为0
    - **~**：0 -> 1，1 -> 0
  - **算术右移>>**，**算术左移<<**，**逻辑右移（无符号右移）>>>**
  - 运算规则：
    - **>>**：低位溢出，符号位不变，并用符号位补溢出的高位
    - **<<**：符号位不变，低位补0
    - **>>>**：低位溢出，高位补0

### 原码，反码，补码（重点 难点）

- 对于有符号的而言：

  - 二进制的最高位是符号位：0表示正数，1表示负数

  - 正数的原码，反码，补码都一样（三码合一）

  - 负数的反码=它的原码符号位不变，其它位取反

  - 负数的补码=它的反码+1，负数的反码=负数的补码-1

  - 0的反码，补码都是0

  - java没有无符号数，换言之，java中的数都是有符号的

  - 在计算机运算的时候，都是**以补码的方式来运算**的

  - 当外面看运算结果的时候，要看它的原码

# 控制结构

### switch

1. **case代码块中的穿透执行**
   - 但进入case代码块后，如果没有break结束语句，则会按顺序进入下一个case的代码块中运行，直到下面的所有代码块都运行完，或者是遇到break结束为止。

   2. `switch(表达式)`中表达式的返回值必须是：（byte，short，int，char，enum，String）
   2. `case`子句中的值不能是变量，必须是常量

# 数组

### 基本数组

- 定义方式：
  - 动态初始化(1)
    - `数据类型[] 数组名 = new 数据类型[大小]` 
  - 动态初始化(2)
    - 先声明数组`数据类型[] 数组名`，然后再创建数组`数组名 = new 数据类型[大小]`
  - 静态初始化
    - `数据类型[] 数组名 = {元素值, 元素值, ...}`
- 注意点：
  - 数组中的数据必须是同类型数据。数组中的元素可以是如何数据类型，包括引用数据类型
  - 数组创建后，如果没有赋值，不同是数据类型有不同的默认值
  - 数组属引用数据类型，数组形数据是对象(object)
  - **基本数据类型赋值，赋值的方式为值拷贝。数组在默认情况下是引用传递，赋的值是地址，赋值方式为引用传递**

### 二维数组

- 定义方式：

  - 静态初始化

    - 略

  - 动态初始化(1)

    - `数据类型[][] 数组名 = new 类型[大小][大小]`

  - 动态初始化(2)

    - 先声明数组`数据类型[][] 数组名`，然后再创建数组`数组名 = new 数据类型[大小][大小]`

  - 动态初始化(3)

    - 先确定行，使用`new`来开辟行空间，然后再使用`new`来一个个开辟列空间。

      - 如：

        ```java
        int[][] arr;
        arr = new int[3][];
        arr[0] = new int[5]
        ```

        

- 注意点：

  - 外层数组指向一个地址，这个地址中存放的又是每一个内层一维数组的地址，内层数组的地址指向一个空间，该空间存放数据

# 面向对象基础

- 成员变量都有自己的默认值，与数组默认值相同。局部变量没有默认值，使用之前需要先初始化对象

### 方法递归调用

### 方法重载

- 方法名：必须相同
- 形参列表：必须不同（参数类型或个数或顺序，至少有一样不同，参数名无要求）
- 返回类型：无要求

### 可变参数

- 概念：java允许将同一个类中多个同名同功能但参数个数不同的方法，封装成一个方法
- 基本语法：`访问修饰符 返回类型 方法名(数据类型... 形参名){}`
  - 表示接收参数为 （0 - 多）即可以不接收参数
  - 使用可变参数时，可以当做数组来使用，即 “参数名”可以当作数组
  - 可变参数的实参可以为数组
  - 可变参数可以和普通类型的参数一起放在形参列表，但必须保证可变参数再最后
  - 一个形参列表中只能出现一个可变参数

### 作用域

- 全局变量：
  - 可以在本类使用，或者其他类中通过对象调用使用
  - 可以加修饰符
- 局部变量
  - 只能在本类对应的方法中使用
  - 不可以加修饰符

### 构造方法/构造器

- 基本介绍：构造器的主要作用是完成对新对象的初始化，创建对象时会自动调用构造器，完成对对象的初始化

  - 构造器的修饰符可以默认，也可以是其他的

  - 构造器没有返回值

  - 方法名和类名字必须一样

  - 参数列表和成员方法的规则一样

  - 构造器的调用，由系统完成
  - 构造器是完成对象的初始化，并不是创建对象
  - 一个类可以定义多个不同的构造器，即构造器的重载
  - 对象初始化步骤，默认初始化 -> 显示初始化 -> 构造器初始化

### javap的使用

- javap是JDK提供的一个命令行工具，javap能对给定的class文件提供的字节代码进行反编译
- 通过它，可以对照源代码和字节码，从而了解很多编译器内部的工作
- 使用格式：`javap <options> <classes>`

### this关键字

- this关键字可以用来访问本类的属性，方法，构造器
- this访问本类的属性和方法时，如果本类没有，则从父类中继续查找
- this用于区分当前类的属性和局部变量
- 访问构造器语法：`this(参数列表);`注意只能在构造器中使用（即只能在构造器中访问另一个构造器），调用构造器只能在当前构造器的第一句使用。
- this不能在类定义的外部使用，只能在类定义的方法中使用

# 面向对象中级

### 访问修饰符

- 公开级别：用`public`修饰，对外公开
- 受保护级别：用`protected`修饰，对子类和同一个包中的类公开
- 默认级别：没有修饰符号，向同一个包的类公开，如果子类和父类在同一个包中，那么子类依然可以访问父类的默认成员
- 私有级别：用`private`修饰只有类本身可以访问，不对外公开

### 封装

- **封装的理解和好处**
  - 隐藏使用细节
  - 可以对数据进行验证，保证安全合理

### 继承

- 子类必须调用父类的构造方法，完成父类的初始化，子类的所有构造器第一行总有默认代码`super();`来调用父类构造器
- 如果父类没提供无参构造器，则必须要在子类构造器的第一行使用`super`去指定调用父类的哪个构造器，来完成对父类的初始化
- 父类有无参构造器的情况下，也可以使用`super`去指定调用哪个构造器
- `super()`和`this()`都只能放在构造器的第一行，所以这两个方法不能共存在一个构造器
- 如果使用了`this()`在当前子类构造器调用另一个子类构造器，那么当前子类构造器将不会自动调用父类构造器，而是在调用的另一个子类构造器中调用父类构造器
- Java所有的类都是`Object`类的子类
- 父类构造器的调用不限于直接父类，将一直向上追溯到Object类
- 子类最多只能继承一个类，java是单继承机制
- 子类的查找方式，采取就近原则。查找不会跳过`private`进行上一级父类查找，碰到私有属性将报错

### super关键字

- `super`代表父类的引用，用于访问父类的属性，方法，构造器

### 方法重写

- 定义：如果子类中有一个方法，和父类的某个方法的名称，返回类型，参数一样，那么这个方法就是父类方法的重写
  - 注意：
    - 子类方法必须要和父类方法的名称和参数一样，但是返回类型可以是父类返回类型的子类，如`Object`和`String`
    - 子类方法不能缩小父类方法的访问权限，但是可以扩大

### 多态

- 多态的前提是：两个对象（类）存在继承关系

- 对象的多态（核心，重点）
  - 一个对象的编译类型和运行类型可以不一致
  - 编译类型在定义对象时，就确定了，不能改变
  - 运行类型可以变化

- 向上转型
  - 本质：父类的引用指向了子类的对象
  - 语法：`父类类型 引用名 = new 子类类型();`
  - 向上转型后，可以调用父类中的所有成员（需要遵守访问权限），但是不可以调用子类的特有成员，因为在编译阶段，能调用哪些成员，是由编译类型决定的
- 向下转型
  - 语法：`子类类型 引用名 = (子类类型) 父类引用`
  - 只能强转父类的引用，不能强转父类的对象
  - 要求父类的引用必须原本就是指向当前目标类型的对象
  - 当向下转型后，可以调用子类类型中所有的成员
  - 向下转型后，相当于创建了两个引用指向一个对象，一个是转型前的引用，一个是转型后的引用

- 注意：
  - 属性没有重写之说，属性的值看编译类型
  - `instanceof`：比较操作符，用于判断当前对象的运行类型是否为某个类型或者为某个类型的子类型

##### **多态-JAVA的动态绑定机制（重要）**

- 当调用对象方法的时候，该方法会和该对象的内存地址/运行类型绑定
- 当调用对象属性时，没有动态绑定机制，哪里声明，哪里使用

##### **多态数组**

- 定义：数组的定义类型为父类类型，里面保存的实际元素类型为子类类型

##### 多态参数

- 定义：方法定义的形参类型为父类类型，实参类型允许为子类类型

### Object

- 判断
  - `equals()`:只能判断引用类型，默认判断的是地址是否相等，子类中往往重写该方法，用于判断内容是否相等。
  - `==`：如果判断基本数据类型，判断的是值是否相等。如果判断引用数据类型，判断的是地址是否相等。
- `hashCode()`
  - 提高具有哈希结构的容器的效率
  - 两个引用，如果指向的是同一个对象，则哈希值肯定是一样的
  - 两个引用，如果指向的不是同一个对象，则哈希值是不一样的(不一定完全，有很小的概率)
  - 哈希值主要根据地址来的，但是不能完全将哈希值等价于地址
- `toString()`
  - 默认返回：全类名 + @ + 哈希值的十六进制 
  - 当直接输出一个对象时，`toString()`方法会被默认调用
- `finalize()`：实际开发基本上不会使用，主要应付面试
  - 当对象被回收时，系统自动调用该对象的`finalize()`方法，子类可以重写该方法，做一些释放资源的操作
  - 垃圾回收机制：垃圾回收机制有自己的GC算法
    - ![image-20220312114030698](图片/image-20220312114030698.png)