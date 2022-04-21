## 调用Matplotlib库绘制图像

#### 调用Matplotlib库

1. `import matplotlib.pyplot as plt`

#### matplotlib 三层结构

1. 容器层
   1. Canvas 底层系统层  充当画板用于放置画布
   2. Figure 需要用户来操作的应用层第一层 在绘图过程中充当画布
   3. Axes 应用层的第二层  在绘图过程中相当于画布上的绘图区/坐标系角色
      - 创建绘图区：`plt.subplots()`
      - 辅助显示层和图像层都是位于绘图区之上

2. 辅助显示层
   1. 绘图区除了图像显示外，用来帮助用户理解

3. 图像层
   1. 用函数绘制出图像



#### 图像绘制

##### 创建画布

​	`plt.figure(figsize=(宽，高)，dpi=像素大小)`

##### 折线图

1. 创建折线图

   ​	`plt.plot(x, y)`	设置点坐标

##### 柱状图

1. 创建柱状图

   ​	`plt.bar(x，y，width=宽度)`

##### 散点图

1. 创建散点图

   ​	`plt.scatter(x，y)`

##### 直方图

1. `plt.hist(x，组数，density=布尔值（判断是否显示频率，默认不显示）)`

##### 饼图

1. `plt.pie(数据，数据对应名称，autopct="%1.2%%"，colors=对应颜色)`
2. `plt.axis("equal")`    保证长宽一致，维持圆形



#### 丰富图像层

###### 修改下x，y轴的刻度值

1. `plt.xticks(要显示的x轴刻度值，相关x轴的说明)`
2. `plt.yticks(要显示的y轴刻度值，相关y轴的说明)`

###### 图像展示与保存

1. 图像展示    `plt.show()`

2. 图像保存    `plt.savefig("保存路径")`    注意：`plt.show()`会释放figure资源，如果显示图像后在保存，只能保存空图片

###### 辅助显示层完善

1. 添加网格	`plt.(linestyle=""，alpha=透明度)`
2. 描述x轴的详细信息    `plt.xlabel("")`
3. 描述y轴的详细信息    `plt.ylabe("")`
4. 添加图像标题    `plt.title("")`
5. 添加图例    `plt.legend(loc="0-6")`    添加图例之前需要在绘制图像时，使用label给予图像名称

###### 创建多个图像

1. `figure，axes = plt.subplots(nrows=行数，ncols=列数)`    该方法为面向对象，会获得两个对象figure与axes，修改不同的axes使用索引方式

###### 解决中文显示问题

`plt.rcParams['font.sans-serif'] = ['KaiTi'] # 指定默认字体`
`plt.rcParams['axes.unicode_minus'] = False # 解决保存图像是负号'-'显示为方块的问题`



## 使用Numpy库进行运算

#### 调用Numpy库

1. `import numpy as np`

#### ndarray属性

1. shape    数组维度的元组
   1. ndim    数组维数
   2. size    数组中元素的数量
2. dtype    元素数据的类型
   1. itemsize    一个数组元素的长度(字节)

#### 创建ndarray

1. `np.ndarray(列表，dtype=np.类型/dtype="类型")`

#### 生成数组

1. 生成0或1数组
   1. `np.zeros(shape=)`    默认float64
   2. `np.ones(shape=)`    默认float64
2. 从现有数据生成
   1. 深拷贝
      1. `np.array()`
      2. `np.copy()`
   2. 浅拷贝
      1. `np.asarray()`
3. 生成固定范围的数组
   1. `np.linspace(起点，终点，取多少个)`    左闭右闭区间，等距离取长
   2. `np.arange(起点，终点，步长)`    左闭右闭区间

#### 生成随机数组

1. 均匀分布
   1. `np.random.uniform(low=，high=，size=)`    low：采取下界，最小值  high：采取上界，最大值  size：数组形状
2. 正态分布
   1. `np.random.normal(loc=μ，scale=σ，size)`    μ：均值，用于确认位置  σ：标准差，标准差=方差开根号，标准差越大，波动越小、图像越平缓、离散程度越大  size：数组形状

#### 数组修改

###### 数组形状修改

1. ndarray.reshape(形状)    返回新的ndarray，原始数据没有改变
2. ndarray.resize(形状)    没有返回值，对原始的ndarray进行了修改
3. ndarray.T    行列转置，返回新的ndarray，原始数据没有改变

###### 数组类型修改

1. ndarray.astype(type)
2. ndarray.tostring()    序列化到本地

###### 数组去重

1. np.unique(数组名)    去重后为一维数组
2. set(数组名.flatten())    利用set方法创建集合的性质来强制去重，set()只能作用与一维数组，.flatten()为不去重转化原数组为一维数组

#### 数组运算

###### 逻辑运算

1. 判断ndarray
   - 直接使用逻辑判断符    例：ndarray > 0 或ndarray < 0 满足条件则返回true，否则返回false
   - 复合判断式
     - 并且    np.logical_and()    例：np.logical_and(ndarray > 0，ndarray < 1)
     - 或者    np.logical_or()    例：相同

2. 通用判断函数
   - np.all()    例：np.all(ndarray > 0)    全部满足条件时返回true，否则返回false
   - np.any()    任意一个满足条件时返回true，否则返回false

3. 三元运算符    np.where()
   - np.where(ndarray + 判断式，满足true时改成什么，满足false时改成什么)    例：np.where(ndarray > 0, 1, 0)

###### 统计运算

1. 统计指标
   - min最小值、max最大值、mean平均值、median中位数、std标准差、var方差    分别对应相同名的函数和方法
     - 参数axis使用方法，在不同的dpi中代表的意思可能不同，在这里0代表按列运算、1代表按行运算    例：np.min(ndarray，axis=0) 代表按列取数字求最大值
   - 返回最大值、最小值所在位置的索引
     - np.argmax(tamp，axis=)
     - np.argmin(tamp，axis=)

###### 数组间运算  

1. 数组与数运算
   - 直接运算    例：ndarray + 1
2. 数组与数组间运算
   - 形状相同时
     - 相同索引值进行运算
   - 形状不相同时
     - 必须符合广播机制
       1. 维度相等
       2. shape (对应的地方有一个为1)

###### 矩阵运算

1. 矩阵 matrix

   - 矩阵一定是二维数组，二维数组不一定是矩阵

2. 创建矩阵

   - 用ndarray创建二维数组
   - 用np.mat()创建矩阵

3. 矩阵的运算

   - 乘法运算

     1. 形状

        - (m，n) * (n，l) = (m，l)

     2. 运算规则

        - A(2，2) * B(2，3) = (2，3)    用A的每一行的每一个数分别去乘B的每一列对应的数

          例：A[[1，2]，[3，4]] * B[[1，2，3]，[4，5，6]]

          A * B = C

          C = [[1 * 1 + 2 * 4，1 * 2 + 2 * 5，1 * 3 + 2 * 6]，[3 * 1 + 4 * 4，3 * 2 + 4 * 5，3 * 3 + 4 * 6]]

          C = [[9，12，15]，[19，26，33]]

     3. ndarray要进行矩阵运算时

        - 例：ndarray：A，B

          np.dot(A，B)

          np.matmul(A，B)

          A @ B

#### 合并与分割

###### 合并

1. 横向合并
   - np.hstack((A，B))    列需要对齐，列数需要相等
2. 竖直合并
   - np.vstack((A，B))
3. np.concatenate((A，B)，axis=)    参数  axis=   0代表竖直、1代表横向

###### 分割

1. np.split(ndarray，x)    x为要分成几份
2. np.split(ndarray，[])    []内填索引    例：[3，5，7]  代表分成三份，分别为0-2、3-4、5-7索引代表的数

#### IO操作与数据处理

- np.genfromtxt("路径"，delimiter="分隔符")    读取数据

  注意：缺失值与字符串会标记为nan，nan的类型为float64



## 使用Pandas库处理数据

#### 调用Pandas库

- import pandas as pd

#### Pandas 三大核心数据结构

###### 1.DataFrame

1. 结构：既有行索引，又有列索引的二维数组

2. 操作：

   - 创建DataFrame：

     - pd.DataFrame(数据，index=行索引，columns=列索引)
     - pd.DataFrame(字典)  每一对键值对为一列，键为列索引，值为列元素，行索引默认为标准索引

   - 补充创建时间数据方法

     pd.date_range(start="起始时间"，end="结束时间") # 有待补充

3. DataFrame的属性与方法

   1. 属性
      - shape  形状
      - index  行索引
      - columns  列索引
      - values  抛弃行列索引后的数据值(ndarray)
      - T  行列转置
   2. 方法
      - head(需要获得的几行)  前几行

      - tail(需要获得的几行)  后几行

      - drop(需要删除的索引名称，axis=0/1)    1为按列索引，0为按行索引

      - 补充方法

        1. get_indexer([行或列索引名称])  用于获取行或列索引名称对应的索引值

           例：DataFrame.index.get_indexer([行索引名称])

           ​		DataFrame.columns.get_indexer([列索引名称])

4. DataFrame的索引设置

   1. 行列索引修改

      - 行索引修改

        DataFrame.index = [新的行索引]

      - 列索引修改

        DataFrame.columns = [新的列索引]

      - 注意：行列索引不能通过索引的方式单独修改某一个，必须整体修改

   2. 重设行索引

      - DataFrame.reset_index(drop=布尔值)  

        True ：删除原索引

        False ：保留原索引为新列

        默认为False

   3. 以某列值设置为新的行索引

      - DataFrame.set_index("keys"，drop=布尔值)

        keys ：列索引名或列索引名列表

        drop ：True删除原索引，False保留原索引

5. 补充  MultiIndex

   - 可以用于存储三维数据
   - 属性
     - names ：每个levels的名称(每一个索引名称)
     - levels ：每个levels的值(每一个索引名称对应的值)

###### 2.Panel

- 结构 ：存储三维结构的面板数据
- 注：Pandas从版本0.20.0开始弃用Panel，推荐使用表示3D数据方法的是DataFrame上的MultiIndex方法

###### 3.Series

1. 结构 ：带索引的一维数组
2. 属性
   - index  索引
   - values  抛弃行列索引后的数据值(ndarray) 
3. 创建 ：
   - pd.Series(一维数组，index=索引列表)
     - index默认为标准索引
   - pd.Series(字典)
     - 字典键为索引，值为数组值

###### 4.总结

Panel是DataFrame的容器

DataFrame是Series的容器

#### 基本数据操作

###### 索引操作

1. 直接索引
   - DataFrame['列索引名']+['行索引名']  注：先列后行，无需加号连接
2. 按名字索引
   - DataFrame.loc['行索引名']+['列索引名']  注：先行后列，无需加号连接
   - DataFrame.loc['行索引名'，'列索引名']  
3. 按数字索引
   - DataFrame.iloc[行索引，列索引]
4. 组合索引
   - DataFrame.ix[行索引，列索引]  注：可以一边是索引值，一边是索引名的混合使用
   - 注意：该方法已被移除
5.   注：DataFrame不可像ndarray直接通过数字索引，如：ndarray[1,2]

###### 赋值与排序

1. 赋值

   - 可直接赋值  如：DataFrame.iloc[0，1] = 100
   - 如果遇到直接赋值没有这个列索引时，会自动创建一个新的列索引进行赋值，数据数量必须对应原来的行索引数量

2. 排序

   1. DataFrame

      - 按值进行排序：

        DataFrame.sort_values(by="列索引名"，ascending=布尔值) True为升序，False为降序，默认为降序

        如果想按多个索引名来排序 如下：

        DataFrame.sort_values(by=["1列索引名"，"2列索引名"])  注：表示，先按1列索引名进行排序，遇到值相同时，在按2列索引名上的值进行排序

      - 按索引进行排序：

        DataFtame.sort_index(ascen=布尔值)    按行索引名进行排序

   2. Series

      - 按值进行排序

        Series.sort_values(ascending=布尔值)

      - 按索引进行排序

        Series.sort_index(ascending=布尔值)

#### DataFrame运算

Series运算类似

###### 算数运算

- 相加    add()  或  直接使用加号

- 相减    sub()  或  直接使用减号

- 相乘    直接使用乘号

- 相除    直接使用除号    或   div()  可选参数axis

- 注：可以通过索引的方式，让DataFrame中的某一列，一一对应与另一列做算数运算

  如：DataFrame['0'].add(DataFrame['1'])

###### 逻辑运算

- 逻辑运算符

  - <、>、|、&

    如：(DataFrame['0'] > 1) & (DataFrame['1'] < 2)    注：0和1为列索引名称

  - 直接使用逻辑运算符，满足条件返回true，否则为false。可以使用布尔索引

    如：DataFrame[Dataframe['0'] < 1]  当列索引名为0的该列数据小于1时，返回该值所在的行的所有值。

- 逻辑运算函数

  - 复合判断函数    

    - DataFrame.query("判断式子")    返回的为符合要求的所有值，而非布尔值

    ​       如：DataFrame.query("0 < 2 & 1  > 3")    注：0和1为列索引名称

    - DataFrame.isin([需要判断的值])    返回的为布尔值，符合条件为true否则为false

      isin可以判断所有列，如：DataFrame.isin([需要判断的值])，也可以判断指定列，如：DataFrame['0'].isin([需要判断的值])

      例1：DataFrame.isin([0，1])  表示在整个DataFrame中，所有满足等于0或1的值，返回true

      例2：DataFrame['0'].isin([0，1])  道理类似，表示在索引名为0的这一列中

###### 统计运算

axis=       0表示按列    1表示按行

1. min最小值、max最大值、mean平均值、median中位数、std标准差、var方差、sum相加和    、count统计数量和、分别对应相同名的函数和方法

2. DataFrame.describe()    同时进行多种运算。平均值，最大值最小值，标准差。

3. 获取索引

   - idxmax(axis=)   获取最大值所在的索引
   - idxmin(axis=)    获取最小值所在的索引

4. 累计统计函数

   - cumsum()    计算前1/2/3/.../n个数的和
   - cummax()    计算前1/2/3/.../n个数的最大值
   - cummin()    计算前1/2/3/.../n个数的最小值
   - cumprod()    计算前1/2/3/.../n个数的积

5. 自定义运算

   - apply(自定义函数，axis=)

     例：DataFrame.apply(lambda x: x.max() - x.min())

     表示按列将DataFrame中的每一个值，当作参数x传入自定义的函数中，进行自定义的函数运算，然后再返回运算后的结果。

#### pandas画图

DataFrame.plot(x='列索引名'，y='列索引名'，kind='需要绘制的图片类型'，stacked=布尔值)    stacked用于判断图像是否堆叠      不填x，y会将DataFrame中所有的列数据都进行画图

图片类型名称与matplotlib的名字相同

#### 文件的读取与存储

###### CSV文件

1. 读取
   - 当文件有字段时：pd.read_csv("地址"，usecols=["字段  (需要获取的列索引名)"])
   - 当文件没有字段时：pd.read_csv("地址"，names=["字段  (自定义字段，一一对应列索引名)"])
2. 存储
   - DataFrame.to_csv("地址"，columns=["填入需要保存的列索引名"]，index=布尔值，mode="w/a"，header=布尔值)
     - index   表示是否需要保留行索引
     - header    表示是否需要保留列索引
     - mode    表示对文件进行重写还是追加，w为重写，a为追加

###### HDF5文件(二进制文件)

1. 读取
2. 存储

###### JSON文件

1. 读取

   - pd.read_json("路径"，orient="records"，lines=布尔值)

     orient  保存格式，默认都填records

     lines  是否按行作为样本  默认False

2. 存储

   - DataFrame.to_json("路径"，orient="records"，lines=布尔值)

     orient  保存格式，默认都填records

     lines  是否按行作为样本  默认False

#### 高级处理

###### 缺失值处理

1. 判断数据中是否有NaN

   - pd.isnull(DataFrame)

     在缺失值所在位置返回true，否则返回false

   - pd.notnull(DataFrame)

     在缺失值所在位置返回false，否则返回true

2. 删除缺失值

   - DataFrame.dropna(axis=""，inplace=布尔值)

     axis：默认按行 0    按列  1  

     inplace：True删除原数据中的缺失值，False返回一个被删除缺失值的数据，默认是False

3. 替换/插补 缺失值

   - DataFrame.fillna(value，inplase=布尔值)

     value：要被替换的值

     inplace：True删除原数据中的缺失值，False返回一个被删除缺失值的数据，默认是False

4. 处理其他标记的缺失值(如："?" 这样的标记)

   - 以"?"为例，首先将"?"替换成np.nan，然后再将其进行nan处理

   - 替换：DataFrame.replace(to_replace=，value=)

     to_replace：替换前的值

     value=替换后的值

     例：DataFrame.replace(to_replace="?"，value=np.nan)

###### 数据离散化

one-hot编码/哑变量

1. 分组

   分组后返回一个series

   分组后的sr查看分组情况，sr.value_counts()

   - 自动分组

     pd.qcut(data，bins)

     data：数据

     bins：需要分的组数

   - 自定义分组

     pd.cut(data，[])

     data：数据

     []：自定义分组的数组  例：以身高为例[165，180，195]表示分为两组，(165，180]，(180，195]

2. 将分组好的结果转化为one-hot编码/哑变量

   - pd.get_dummies(data，prefix="")

     data：分组好的series

     prefix：分组的前缀名

###### 合并

1. 按方向合并

   - pd.concat([data1，data2]，axis=)

     data：需要进行拼接的数据

     axis：按行或列进行拼接，0按列，1按行

2. 按索引合并

   - pd.merge(left，right，how=""，on=[])

     left：需要拼接的左数据

     right：需要拼接的右数据

     how：拼接模式

     on：指定按什么索引进行拼接

   - 扩展拼接模式：
     - left：左连接，保留左表中的所有数据与右表中和左表相同指定索引的数据进行拼接
     - right：右连接，保留右表中的所有数据与左表中和右表相同指定索引的数据进行拼接
     - inner：内连接，将左右两表中指定索引相同的数据进行拼接
     - outer：外连接，将左右两表中所有指定的索引数据进行拼接

###### 交叉表与透视表

作用：寻找两列之间的关系

扩展：转化pandas的日期类型    pd.to_datetime(数据)    转化为日期类型后拥有多种属性，如weekday，year等

1. 交叉表

   - pd.crosstab(value1，value2)

     value：列数据

2. 透视表

   - DataFrame.pivot_table([]，index=[])

     表示：把[]中的字段索引，按照index=[]里面的索引进行分组

###### 分组与聚合

1. DataFrame
   - DataFrame.groupby(by="")
   - by：按那个索引进行分组
   - 注意：分组后并不能直接看到结果，只会返回一个对象，进行聚合后才能看到结果
   - 例：DataFrame.groupby(by="索引1")["索引2"].max    表示按索引1进行分组后，再按索引2进行聚合，分别得出分组后每一组在索引2中的最大值。
2. Series
   - 举例：设一个DataFrame为dt    
   - dt["索引1"].groupby(dt["索引2"]).max()
   - dt["索引1"]得出一个series    再dt["索引2"]得出一个series    表示按dt["索引2"]进行分组，按dt["索引1"]进行聚合

