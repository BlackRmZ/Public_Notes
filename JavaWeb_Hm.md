##    Junit单元测试

- 测试分类：
  1. 黑盒测试：不需要写代码，给输入值，看程序是否能够输出期望的值。
  2. 白盒测试：需要些代码的。关注程序具体的执行流程
- Junit使用：白盒测试
  - 步骤：
    1. 定义一个测试类（测试用例）
       - 建议：
         1. 测试类名：被测试的类名 + Test		如：`CalcutorTest`
         2. 包名：`xxx.xxx.xx.test`	    如：`cn.itcast.test`
    2. 定义测试方法：可以独立运行
       - 建议：
         1. 方法名：test测试的方法名        如：`testAdd()`
         2. 返回值：void
         3. 参数列表：空参
    3. 给方法加@Test
  - 判定结果：
    - 红色：失败
    - 绿色：成功
    - 一般我们会使用断言操作来处理结果
      - `Assert.assertEquals(预期值, 运算值)`
  - 补充：
    - `@Befor`
      - 修饰的方法会在测试方法之前被自动执行。初始化方法，用于资源申请，所有测试方法在执行之前都会先执行该方法
    - `@After`
      - 修饰的方法会在测试方法执行之后自动被执行。释放资源方法，在所有测试方法执行完之后，都会自动执行该方法。即使被测试方法出现异常，该释放资源的方法仍然会执行。

### 反射：框架设计的灵魂

- 框架：半成品软件。可以在框架的基础上进行软件开发，简化编码

- 反射：将类的各个组成部分封装为其他对象，这就是反射机制

  - 好处：
    1. 可以在程序运行过程中，操作这些对象
    2. 可以解耦，提高程序的可扩展性

- 获取class对象的方式：

  1. `Class.forName("全类名")`：将字节码文件加载进内存，返回Class对象

     - 多用于配置文件，将类名定义在配置文件中。读取文件，加载类

  2. `类名.class`：通过类名的熟悉class获取

     - 多用于参数的传递

  3. `对象.getClass()`：`getClass()`方法在object类中定义着。

     - 多用于对象的获取字节码方式

       

  4. 结论：

     - 同一个字节码文件(*.class)在一次程序运行过程中，只会被加载一次，无论通过哪一种方式获取的class对象都是同一个。

- Class对象功能：

  - 获取功能：
    1. 获取成员变量们
       - `Field[] getFields()`：获取所有public修饰的成员变量
       - `Field getField(String name)`：获取指定名称的public修饰的成员变量
       - `Field[] getDeclaredFields()`：获取所有的成员变量，不考虑修饰符
       - `Field getDeclaredField(String name)`
    2. 获取构造方法们
       - `Constructor<?>[] getConstructors()`
       - `Constructor<T> getConstructor(类<?>... parameterTypes)`
       - `Constructor<?>[] getDeclaredConstructors()`
       - `Constructor<T> getDeclaredConstructor(类<?>... parameterTypes)`
    3. 获取成员方法们：
       - `Method[] getMethods()`
       - `Method getMethod(String name, 类<?>... parameterTypes)`
       - `Method[] getDeclaredMethods()`
       - `Method getDeclaredMethod(String name, 类<?>... parameterTypes)`
    4. 获取类名
       - `String getName()`
  - Field：成员变量
    - 操作：
      1. 设置值
         - `void set(Object obj, Object value)`
      2. 获取值
         - `get(Object obj)`
      3. 忽略访问权限修饰符的安全检查
         - `setAccessible(true)`：暴力反射

## 注解

- JDK中预定义的一些注解

  - `@Override`：检测被该注解标注的方法是否是继承自父类(接口)的
  - `@Deprecated`：该注解标注的内容，表示已过时
  - `@SuppressWarnings`：压制警告
    - 一般传递参数all：`@SuppressWarnings("all")`

- 自定义注解

  - 格式：

    - ```java
      元注解
      public @interface 注解名称{}
      ```

  - 本质：注解本质上就是一个接口，接口默认继承Annotation接口

  - 属性：接口中的抽象方法

    - 要求：
      - 属性的返回值类型有下列取值
        - 基本数据类型
        - String
        - 枚举
        - 注解
        - 以上类型的数组
      - 定义了属性，在使用时需要给属性赋值
        1. 如果定义属性时，使用default关键字给属性默认初始化值，则使用注解时，可以不进行属性的赋值。
           - 例子：`String name() default "张三";`
        2. 如果只有一个属性需要赋值，并且属性的名称是value，则value可以省略，直接定义值即可。
        3. 数组赋值时，值使用{}包裹。如果数组中只有一个值，则{}省略

## 数据库

1. MySQL服务
   - 启动：`net start mysql`
   - 关闭：`net stop mysql`

#### SQL

1. 三种注释
   1. 单行注释：
      - `-- 注释内容`
      - `# 注释内容(mysql独有)`
   2. 多行注释：
      - `/* 注释 */`
2. SQL分类
   1. DDL：操作数据库、表
   2. DQL：查询表中的数据
   3. DML：增删改表中的数据
   4. DCL：授权

###### DDL

1. 操作数据库：CRUD
   1. C(Create)：创建
      - 创建数据库：`create database 数据库名称;`
      - 创建数据库，判断不存在，再创建：`create database if not exists 数据库名称;`
      - 创建数据库，并指定字符集：`create database 数据库名称 character set 字符集名;`
      - 创建数据库，判断不存在，再创建，并指定字符集：`create database if not exists 数据库名 character set 字符集名`
   2. R(Retrieve)：查询
      - 查询所有数据库的名称：`show databases;`
      - 查询某个数据库的创建语句：`show create database 数据库名称;`
   3. U(Update)：修改
      - 修改数据库的字符集：`alter database 数据库名称 character set 字符集名称;`
   4. D(Delete)：删除
      - 删除数据库：`drop database 数据库名称;`
      - 判断数据库存在，存在，再删除：`drop database if exists 数据库名称;`
   5. 使用数据库
      - 查询正在使用的数据库名称：`select database();`
      - 使用数据库：`use 数据库名称;`
2. 操作表
   1. C(Create)：创建

      1. 语法：

         ​	

         ```sql
         create table 表名(
         	列名1 数据类型1,
             列名2 数据类型2,
             ....
             列名n 数据类型n
         );
         -- 注意：最后一列，不需要加逗号
         ```

      2. 数据库类型

         - `int`：整数类型
         - `double`：小数类型
            - score double(5,2)：表示最大5位数，并且保留2位小数
         - `data`：日期，只包含年月日，`yyyy-MM-dd`
         - `datatime`：日期，包含年月日时分秒，`yyyy-MM-dd HH:mm:ss`
         - `timestamp`：时间错类型，包含年月日时分秒，`yyyy-MM-dd HH:mm:ss`
            - 如果将来不给这个字段赋值，或赋值为null，则默认使用当前的系统时间，来自动赋值
         - `varchar`：字符串
            - 例子：`name varchar(20):姓名最大20个字符`

      3. 补充：复制表，`create table 表名 like 被复制的表名;`

   2. R(Retrieve)：查询
      - 查询某个数据库中所有的表名称：`show tables;`
      - 查询表结构：`desc 表名;`

   3. U(Update)：修改

      - 修改表名：`alter table 表名 rename to 新的表名;`
      - 修改表的字符集：`alter table 表名 character set 新字符集;`
      - 添加一列：`alter table 表名 add 列名 数据类型;`
      - 修改列名称，类型：
         - 名称类型一起修改：`alter table 表名 change 列名 修改后的列名 数据类型;`
         - 只改类型：`alter table 表名 modify 列名 数据类型`
      - 删除列：`alter table 表名 drop 列名;`

   4. D(Delete)：删除

      - `drop table 表名;`
      - `drop table if exists 表名;`

###### DML：增删改表中数据

1. 添加数据：
   - `insert into 表名(列名1,列名2,列名3,...列名n) values(值1,值2,值3,..值n);`
     - 如果表名后，不定义列名，则默认给所有列添加值
2. 删除数据：
   - `delete from 表名 where 条件;`
   - 注意：
     1. 如果不加条件，则删除表中所有记录
     2. 如果要删除所有记录
        1. `delete from 表名;` -- 不推荐使用。有多少条记录就会执行多少次删除操作。
        2. `truncate table 表名` -- 先删除表，然后再创建一个一样的表。
3. 修改数据：
   - `updata 表名 set 列名1 = 值1,列名2 = 值2,...列名n = 值n where 条件;`
      - 如果不加条件，则会将表中该列的所有记录全部修改

###### DQL：查询表中的记录

1. 语法

   - ```sql
     select
     	字段列表
     from
     	表名列表
     where
     	条件列表
     group by
     	分组字段
     having
     	分组之后的条件
     order by
     	排序
     limit
     	分页限定
     ```

   - 

2. 基础查询
   1. 多个字段的查询

      - ```SQL
        select 字段名1, 字段名2, ... from 表名;
        ```

        

      - 如果查询所有字段，可以使用*来代替字段列表

   2. 去除重复

      - `distinct`

   3. 计算列

      - 一半可以使用四则运算计算一些列的值。(一般只会进行数值型的计算)
      - `ifnull(表达式1,表达式2)`：null参与的运算，计算结果都为null
        - 表达式1：哪个字段需要判断是否为null
        - 如果该字段为null后的替代值

   4. 起别名

      - `as`

3. 条件查询

   1. where子句后面跟条件

   2. 运算符

      - ```sql
        >, <, <=, >=, =, <>, !=
        between ... and(在什么与什么之间)
        in(集合)
        like
        is null, is not null
        and 
        or
        not
        ```

      - `like`：模糊查询

        - 占位符：
          - _：单个任意字符
          - %：多个任意字符

4. 排序查询

   - 语法：`order by 子句`
     - `order by 排序字段1 排序方式1, 排序字段2 排序方式2 ...`
   - 排序方式：
     - ASC：升序，默认的。
     - DESC：降序。
   - 注意：
     - 如果有多个排序条件，则当前面的条件值一样时，才会判断第二条件。

5. 聚合函数：将一列数据作为一个整体，进行纵向的计算。

   1. count：计算个数
      1. 一般选择非空的列：主键
   2. max：计算最大值
   3. min：计算最小值
   4. sum：计算和
   5. avg：计算平均值

6. 分组查询

   1. 语法：`group by`分组字段；
   2. 注意：
      1. 分组之后查询的字段：分组字段、聚合函数
      2. where和having的区别
         1. where在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如果不满足结果，则不会被查询出来
         2. where后不可以跟聚合函数，having可以进行聚合函数的判断

7. 分页查询

   1. 语法：`limit 开始的索引, 每页查询的条数`
   2. 公式：开始的索引 = (当前的页码 - 1) * 每页显示的条数
   3. 该分页操作是`mysql`的一个"方言"

###### 约束

- 概念：对表中的数据进行限定，保证数据的正确性、有效性和完整性。
- 分类
  1. 主键约束：`primary key`
     1. 含义：非空且唯一
     2. 一张表只能一个字段为主键
     3. 主键就是表中记录的唯一标识
     4. 删除主键：`alter table stu drop primary key`
        - 注意：删除主键后，会保留一个非空约束，需手动删除
     5. 自动增长
        1. 概念：如果某一列是数值类型的，使用`auto_increment` 可以来完成值的自动增长
        2. 在创建表时，添加主键约束，并完成自动增长：`列名 数据类型 primary key auto_increment`
        3. 删除自动增长：`alter table 表名 modify 需要被删除的列名 该列的数据类型`
        4. 添加自动增长：`alter table 表名 modify 需要被添加的列名 该列的数据类型 auto_increment`
     
  2. 非空约束：`not null`
  
  3. 唯一约束：`unique`
     - 注意：
       - 唯一约束的删除不同于其他约束`alter table 表名 drop index 需要被删除约束的列名;`
       - 创建表之后添加唯一约束时，需要注意被添加列当前有无重复数据，如果有则添加约束失败
     
  4. 外键约束：`foreign key`
  
     - 语法：
  
        - ```sql
           create table 表名(
           	...
               外键列
               constraint 外键名称(自定义) foreign key (外键列名称) references 主表名称(主表列名称)
           );
           ```
  
     - 删除外键
  
        - `alter table 需要被删除的外键的表名 drop foreign key 外键名;`
  
     - 创建表后添加外键
  
        - `alter table 需要被添加的外键的表名 add constraint 外键名 foreign key (外键列名) references 主表名称(主表列名)`
  
     - 级联操作
  
        - 更新：`on update cascade`
        - 删除：`on delete cascade`

###### 多表查询

- 多表查询的分类
  1. 内连接查询：
     1. 隐式内连接：使用where条件消除无用数据
     2. 显示内连接：`select 字段列表 from 表名1 [inner] join 表名2 on 条件;`
  2. 外连接查询：
     1. 左外连接：`select 字段列表 from 表1 left [outer] join 表2 on 条件;`
     2. 右外连接：`select 字段列表 from 表1 right [outer] join 表2 on 条件;`
     3. 查询的是(左表/右表)的所有数据以及其交集部分
  3. 子查询：
     1. 子查询的不同情况
        1. 子查询的结果是单行单列的：
           - 子查询可以作为条件，使用运算符去判断。运算符：> >= < <= =
        2. 子查询的结果是多行单列的：
           - 子查询可以作为条件，使用运算符in来判断
        3. 子查询的结果是多行多列的：
           - 子查询可以作为一张虚拟表参与查询

###### 事务

1. 概念：
   - 如果一个包含多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败。
2. 操作：
   1. 开启事务：`start transaction;`
   2. 回滚：`rollback;`
   3. 提交：`commit;`
3. MySQL数据库中事物是默认自动提交
   1. 修改事物的默认提交方式
      1. 查看事务的默认提交方式：`select @@autocommit;` -- 1 代表自动提交    0 代表手动提交
      2. 修改默认提交方式：`set @@autocommit = 0;`
4. 事务的四大特征

###### DCL

1. 管理用户：

   1. 添加用户：

      - `create user '用户名'@'主机名' identified  by '密码';`

   2. 删除用户：

      - `drop user '用户名'@'主机名';`

   3. 修改用户密码

      - `update user set password = password('新密码') where user = '用户名';`
      - `set password for '用户名'@'主机名' = password('新密码');`

   4. 查询用户：

      - 

        ```sql
        --- 切换到mysql数据库后
        select * from user;
        ```

2. 权限管理

   1. 查询权限：`show grants for '用户名'@'主机名';`
   2. 授予权限：`grant 权限列表 on 数据库名.表名 to '用户名'@'主机名'；`
   3. 撤销权限：`revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名';`

# JDBC

###### JDBC操作

1. 快速入门（示例）

   - ```java
     		// 1.注册驱动
             Class.forName("com.mysql.jdbc.Driver");
             // 2.获取数据库连接对象
             Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/test_one", "root", "root");
             // 3.定义一个sql语句
             String sql = "update account set balance = 600 where id = 1";
             // 4.获取执行sql的对象
             Statement statement = connection.createStatement();
             // 5.执行sql
             int count = statement.executeUpdate(sql);
             // 6.处理结果
             System.out.println(count);
             // 7.释放资源
             statement.close();
             connection.close();
     ```

2. 详解各个对象：

   1. `DriverManager`：驱动管理对象
      1. 注册驱动
      2. 获取数据库连接：`getConnection`
   2. `Connection`：数据库连接对象
      1. 获取执行sql的对象
         1. `Statement createStatement()`
         2. `PreparedStatement prepareStatement(String sql)`
      2. 管理事务
         1. 开启事务：`setAutoCommit(boolean autoCommit)`：调用该方法设置参数为false，即开启事务
         2. 提交事务：`commit()`
         3. 回滚事务：`rollback()`
   3. `Statement`：执行sql对象
      1. 执行sql
         1. `boolean execute(String sql)`：可以执行任意的sql，一般不使用
         2. `int executeUpdate(String sql)`：执行DML（insert, update, delete）语句，DDL（create, alter, drop）语句
            - 返回值：影响的行数，可以通过这个影响的行数判断DML语句是否执行成功，返回值大于0则执行成功
         3. `ResultSet executeQuery(String sql)`：执行DQL（select）语句
   4. `ResultSet`：结果集对象，封装查询结果
      1. `boolean next()`：游标向下移动一行，判断当前行是否是最后一行末尾（是否有数据），如果是，则返回false，如果不是则返回true
      2. `getXxx(参数)`：获取数据
         - Xxx：代表数据类型	如：`int getInt()`
         - 参数：
            - int：代表列的编号，从1开始		如：`getString(1)`
            - String：代表列名称          如：`getDouble("balance")`
   5. `PreparedStatement`：执行sql的对象
      1. 预编译的sql：参数作为?作为占位符，用来解决sql注入问题
      2. 给?赋值：
         1. 方法：`setXxx(参数1, 参数2)`
            1. 参数1：?的位置编号，编号从1开始
            2. 参数2：?的值
      3. 使用`PreparedStatement`执行sql时，不需要传递参数，只需要接受返回结果
         1. 如：`preparedstatement.executeQuery()`

###### 数据库连接池

1. 实现
   1. 标准接口：`DataSource`
      1. 方法：
         - 获取连接：`getConnection()`
         - 归还连接：如果连接对象`Connection`是从连接池中获取的，那么调用`Connection.close()`方法，则不会再关闭连接，而是归还连接。
2. C3P0：数据库连接池技术
   1. 定义配置文件：
      - 名称：`c3p0.properties`或者`c3p0-config.xml`
      - 路径：直接放在src目录下即可
   2. 创建核心对象，数据库连接池对象：`ComboPooledDataSource`
3. Druid：数据库连接池实现技术，由阿里巴巴提供
   1. 定义配置文件：
      1. 是properties形式的
      2. 可以叫任意名称，放在任意目录下
   2. 加载配置文件。Properties
   3. 获取数据库连接池对象：通过工厂来获取：`DruidDataSourceFactory`

###### Spring JDBC

- `Spring`框架对JDBC的简单封装，提供了一个`JDBCTemplate`对象简化JDBC的开发
- 步骤：
  1. 创建`JdbcTemplate`对象。依赖于数据源`DataSource`：`JdbcTemplate template = new JdbcTemplate(datasource);`
  2. 调用`JdbcTemplate`的方法来完成CRUD的操作
     1. `update()`：执行DML语句。增、删、改语句
     2. `queryForMap()`：查询结果，将结果集封装为map集合
        - 注意：这个方法查询的结果集长度只能为1（封装一条记录）
     3. `queryForList()`：查询结果，将结果集封装为list集合
        - 注意：将每一条记录封装成一个Map集合，再将Map集合装载到List集合
     4. `query()`：查询结果，将结果封装为`JavaBean`对象
     5. `queryForObject`：查询结果，将结果封装为对象

## Web相关概念回顾

1. 软件架构
   1. C/S：客户端/服务器端
   2. B/S：浏览器/服务器端
2. 资源分类
   1. 静态资源：所有用户访问后，得到的结果都是一样的，称为静态资源。静态资源可以直接被浏览器解析
   2. 动态资源：每个用户访问相同资源后，得到的结果可能不一样。称为动态资源。动态资源被访问后，需要先转换为静态资源，再返回给浏览器。
3. 网络通信三要素
   1. IP：电子设备（计算机）在网络中的唯一标识。
   2. 端口：应用程序在计算机中的唯一标识。0~65536
   3. 传输协议：规定了数据传输的规则
      1. 基础协议
         1. tcp：安全协议，三次握手。速度稍慢
         2. udp：不安全协议，速度快

## Web服务器软件

- 服务器：安装了服务器软件的计算机

- 服务器软件：接受用户的请求，处理请求，做出响应

- web服务器软件：接受用户的请求，处理请求，做出响应

  - 在web服务器软件中，可以部署web项目，让用户通过浏览器来访问这些项目
  - 也被称为web容器

- 常见的java相关的web服务器软件

  - weblogic：oracle公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
  - webSphere：IBM公司，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
  - JBOSS：JBOSS公司的，大型的JavaEE服务器，支持所有的JavaEE规范，收费的。
  - Tomcat：Apache基金组织，中小型的JavaEE服务器，仅仅支持少量的JavaEE规范。开源的，免费的。

- JavaEE：Java语言在企业级开发中使用的技术规范的综合，一共规定了13项大的规范。

- Tomcat：web服务器软件

  1. 目录结构
     1. bin：可执行文件
     2. conf：配置文件
     3. lib：依赖jar包
     4. logs：日志文件
     5. temp：临时文件
     6. webapps：存放web项目
     7. work：存放运行时的数据

  2. 配置：

     1. 部署项目的方式

        1. 直接将项目放到webapps目录下即可

           - 简化部署：将项目打成一个war包，再将war包放置到webapps目录下。

        2. 配置conf/server.xml文件

           - 在<Host>标签体中配置

             <Context docBase="D:\Hello" path="/hehe" />

             docBase:项目存放的路径

             path：虚拟目录

        3. (热部署)在conf/Catalina\localhost创建任意名称的xml文件。在文件中编写

           <Context docBase="D:\Hello" />

           虚拟目录：xml文件的名称

           卸载项目只需要把后缀从xml改成xml_bak

     2. 静态项目和动态项目（有WEB-INF目录，说明是动态项目）
        - 目录结构
          - java动态项目的目录结构：
            - 项目的根目录
              - WEB-INF目录：
                - web.xml：web项目的核心配置文件
                - classes目录：放置字节码文件的目录
                - lib目录：放置依赖的jar包

## Servlet：(server applet)

- 概念：运行在服务器端的小程序
  - Servlet就是一个接口，定义了Java类被浏览器访问到(tomcat识别)的规则。
  - 将来我们自定义一个类，实现Servlet接口，复写方法。

- 快速入门

  1. 创建JavaEE项目

  2. 定义一个类，实现Servlet接口 

  3. 实现接口中的抽象方法

  4. 配置Servlet

     - 在web.xml中配置：

       - ```xml
         <!-- 配置servlet -->
             <servlet>
                 <servlet-name>demo1</servlet-name>
                 <servlet-class>cn.itcast.web.servlet.ServletDemo1</servlet-class>
             </servlet>
             <servlet-mapping>
                 <servlet-name>demo1</servlet-name>
                 <url-pattern>/demo1</url-pattern>
             </servlet-mapping>
         ```

- 执行原理：
  1. 当服务器接收到客户端浏览器的请求后，会解析请求URL路径，获取访问的Servlet资源路径
  2. 查找web.xml文件，是否有对应的<url-pattern>标签体内容
  3. 如果有，则在找到对应的<servlet-class>全类名
  4. tomcat会将字节码文件加载进内存，并且创建其对象
  5. 调用其方法

- Servlet中的生命周期：
  1. 被创建：执行init方法，只执行一次。用于加载资源
     - 默认情况下，第一次访问时，Servlet被创建
     - 可以配置执行Servlet的创建时机
       - 在<servlet>标签下配置
         1. 第一次访问时，创建
            - <load-on-startup>的值为负数
         2. 在服务器启动时，创建
            - <load-on-startup>的值为0或正整数
     - Servlet的init方法，只执行一次，说明一个Servlet在内存中只存在一个对象，Servlet是单例的
       - 多个用户同时访问时，可能存在线程安全问题。
       - 解决：尽量不要在Servlet中定义成员变量。即使定义了成员变量，也不要对其修改值
  2. 提供服务：执行service方法，执行多次
     - 每次访问Servlet时，Servlet方法都会被调用一次
  3. 被销毁：执行destroy方法，只执行一次
     - Servlet被销毁时执行，服务器关闭时，Servlet被销毁
     - 只有服务器正常关闭时，才会执行destroy方法
     - destroy方法在Servlet被销毁之前执行，一般用于释放资源

- Servlet3.0：
  - 好处：
    - 支持注解配置，可以不需要web.xml了。
  - 步骤：
    1. 创建JavaEE项目，选择Servlet的版本3.0以上，可以不创建web.xml
    2. 定义一个类，实现Servlet接口
    3. 复写方法
    4. 在类伤上使用@WebServlet注解，进行配置

- Servlet的体系结构

  - ```html
    Servlet -- 接口
    	|
    GenericServlet -- 抽象类
    	|
    HttpServlet -- 抽象类
    ```

    

  - GenericServlet：将Servlet接口中其他的方法做了默认空实现，只将service()方法作为抽象

  - HttpServlet：对http协议的一种封装，简化操作

    - 复写doGet/doPost方法

- Servlet相关配置
  - urlpartten：servlet访问路径
    - 一个Servlet可以定义多个访问路径：`@WebServlet({"/d1", "/d2", "d3"})`
    - 路径定义规则：
      1. /xxx
      2. /xxx/xxx：多层路径，目录结构
      3. *.do：后缀名式路径

## HTTP---请求

- 概念：Hyper Text Transfer Protocol 超文本传输协议
  - 传输协议：定义了，客户端和服务器端通信时，发生数据的格式
  - 特点：
    1. 基于TCP/IP的高级协议
    2. 默认端口号：80
    3. 基于请求/响应模型的：一次请求对应一次响应
    4. 无状态的：每次请求之间相互独立，不能交互数据

- 请求消息数据格式

  1. 请求行

     - 请求方式 请求URL 请求协议/版本

       例子：GET /login.html HTTP/1.1

  2. 请求头：客户端浏览器告诉服务器一些信息
    - 常用请求头：
      1. User-Agent：浏览器告诉服务器，我访问你使用的浏览器版本信息
         - 可以在服务端获取该头信息，解决浏览器兼容性问题
      2. Referer：浏览器告诉服务器，我(当前请求)从哪里来？
         - 作用：
           1. 防盗链：
           2. 统计工作：

  3. 请求空行

     - 空行

  4. 请求体（正文）

     - GET方式没有请求体
     - 请求体存放参数

## Request

- request对象和response对象的原理
  1. request和response对象是由服务器创建的。我们来使用它们
  2. request对象是来获取请求消息，response对象是来设置响应消息

* request对象继承体系结构：

  * ```html
    ServletRequest		--		接口
    		|	继承
    HttpServletRequest		--		接口
    		|	实现
    tomcat实现类，并创建对象
    ```

    

* request功能：
  1. 获取请求消息数据
     1. 获取请求行数据
        - `GET /day/demo1?name=zhangsan HTTP/1.1`
        - 方法
          1. 获取请求方式：GET
             - `String getMethod()`
          2. （*）获取虚拟目录：/day
             - `String getContextPath()`
          3. 获取Servlet路径：/demo1
             - `String getServletPath()`
          4. 获取get方式请求参数：name=zhangsan
             - `String getQueryString()`
          5. （*）获取请求URI：/day/demo1
             - `String getRequestURI()`
          6. （*）获取请求URL：http://localhost:8080/day/demo1
             - `StringBuffer getRequestURL()`
          7. 获取协议及版本：HTTP/1.1
             - `String getProtocol()`
          8. 获取客户机的IP地址
             - `String getRemoteAddr()`
     2. 获取请求头数据
        - 方法：
           1. （*）通过请求头的名称获取请求头的值
              - `String getHeader(String name)`
           2. 获取所有请求头名称
              - `Enumeration<String> getHeaderNames()`
     3. 获取请求体数据
  2. 其他功能：
     1. 获取请求参数通用方式：不论get还是post都可以使用
        1. `String getParameter(String name)`:根据参数名称获取参数值
        2. `String[] getParameterValues(String name)`:根据参数名称获取参数值的数组
        3. `Enumeration<String> getParameterNames()`:获取所有请求的参数名称
        4. `Map<String,String[]> getParameterMap`:获取所有参数的map集合
        5. 中文乱码问题：
           - get方式：tomcat8已经将get方式乱码问题解决了
           - post方式：会乱码
             - 解决：在获取参数前，设置request的编码`request.setCharacterEncoding("utf-8")`
     2. 请求转发：一种在服务器内部的资源跳转方式
        1. 步骤：
           1. 通过request对象获取请求转发器对象：`RequestDispatcher getRequestDispatcher(String path)`
           2. 使用RequestDispatcher对象来进行转发：`forward(ServletRequest request, ServletResponse response)`
        2. 特点
           1. 浏览器地址栏路径不发生变化
           2. 只能转发到当前服务器内部资源中
           3. 转发是同一次请求
     3. 共享数据
        - 域对象：一个有作用范围的对象，可以在范围内共享数据
        - request域：代表一次请求的范围，一般用于请求转发的多个资源中共享数据
        - 方法：
          1. `void setAttribute(String name, Object obj)`：储存数据
          2. `Object getAttitude(String name)`：通过键获取值
          3. `void removeAttribute(String name)`：通过键移除键值对  
     4. 获取ServletContext
        - `ServletContext getServletContext()`

###### BeanUtils工具类----简化数据封装

- 用于封装JavaBean

- JavaBean：标准的java类

  1. 要求：
     1. 类必须被public修饰
     2. 必须提供空参的构造器
     3. 成员变量必须使用private修饰
     4. 提供公共setter和getter方法
  2. 功能：封装数据

- 概念：

  1. 成员变量：

  2. 属性：setter和getter方法截取后的产物

     例如：getUsername() --> Username --> username

- 方法：
  1. `setProperty()`：设置属性值
  2. `getProperty()`：获取属性值
  3. `populate(Object obj, Map map)`：将map集合的键值对信息，封装到对应的JavaBean对象中

## Response

- 功能：设置响应消息
  1. 设置响应行
     - 设置状态码：`setStatus(int sc)`
  2. 设置响应头：
     - `setHeader(String name, String value)`
  3. 设置响应体：
     - 使用步骤：
       1. 获取输出流：
          - 字符输出流：`PrintWriter getWriter()`
          - 字节输出流：`ServletOutputStream getOutputStream()`
       2. 使用输出流，将数据输出到客户端浏览器
  4. 重定向方法：`sendRedirect(String path)`
     1. 重定向与转发的区别：
        1. 重定向的特点：
           1. 地址栏发生变化
           2. 重定向可以访问其他站点(服务器)的资源
           3. 重定向是两次请求。不能使用request对象来共享数据
        2. 转发的特点：
           1. 转发地址栏路径不变
           2. 转发只能访问当前服务器下的资源
           3. 转发是一次请求，可以使用request对象来共享数据

## ServletContext对象

1. 概念：代表整个web应用，可以和程序的容器(服务器)来通信
2. 获取：
   1. 通过`request`对象来获取：`request.getServletContext()`
   2. 通过`HttpServlet`获取：`this.getServletContext()`
   3. 注意：两种方式获取的是同一个`servletcontext`
3. 功能：
   1. 获取MIME类型：
      1. 格式：大类型/小类型     `text/html`
      2. 获取：`String getMimeType(String file)`：通过文件名，文件的后缀名来获取类型
   2. 域对象：共享数据
      1. `setAttribute(String name, Object value)`
      2. `getAttribute(String name)`
      3. `removeAttribute(String name)`
      4. 注意：ServletContext对象范围：所有用户所有请求的数据
   3. 获取文件的真实(服务器)路径
      1. `String getRealPath(String path)`：默认是在web目录下进行访问。

## Cookie

1. 概念：客户端会话技术，将数据保存到客户端
2. 使用步骤：
   1. 创建Cookie对象，绑定数据：`new Cookie(String name, String value)`
   2. 发送Cookie对象：`response.addCookie(Cookie cookie)`
   3. 获取Cookie，拿到数据：`Cookie[] request.getCookies()`
3. Cookie在浏览器中的保存时间
   1. 默认情况下，当浏览器关闭后，Cookie数据被销毁
   2. 持久化存储：
      - `Cookie cookie.setMaxAge(int seconds)`
         1. 正数：将cookie数据写到硬盘的文件中，持久化储存，填写的数据单位为秒
         2. 负数：默认值
         3. 零：删除cookie信息
4. Cookie的共享问题
   1. 在同一个tomcat服务器中，部署了多个web项目，在这些项目中能否共享cookie
      1. 默认情况下cookie不能共享
      2. `setPath(String path)`：设置cookie的获取范围。默认情况下，设置为当前的虚拟目录。如果需要共享，则可以将path设置为"/"
   2. 不同的tomcat服务器间cookie共享问题
      - `setDomain(String path)`：如果设置一级域名相同，那么多个服务器之间cookie可以共享
        - 示例：`setDomain(".baidu.com")`，那么`tieba.baidu.com`和`news.baidu.com`中的cookie可以共享

## JSP

- JSP本质上就是一个servlet
- JSP的脚本：JSP定义Java代码的方式
  1. <% 代码 %>：定义的java代码，在service方法中。service方法中可以定义什么，该脚本就可以定义什么。
  2. <%! 代码 %>：定义的java代码，在jsp转换后的java类的成员位置
  3. <%= 代码 %>：定义的java代码，会输出到页面上，输出语句可以定义什么，该脚本就可以定义什么，代码也在被写在service方法中。
- JSP的内置对象：9个
  1. request
  2. response
  3. out：字符输出流对象。可以将数据输出到页面上。

## Session

- 概念：服务器端会话技术，在一次会话的多次请求间共享数据，将数据保存在服务器端的对象中。`HttpSession`
- `HttpSession`对象：
  1. `Object getAttribute(String name)`
  2. `void setAttribute(String name, Object value)`
  3. `void removeAttribute(String name)`
  4. `request.getSession()`：获取HttpSession对象
