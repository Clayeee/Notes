## JavaScript组成部分

- ECMAScript   <!-- 基础语法（核心）-->       

  + 语法
  + 类型
  + 语句
  + 关键字
  + 保留字
  + 操作符
  + 对象

- DOM <!--Document Object Model 文档对象模型-->

  > 提供访问和操作网页内容的方法和接口

  + DOM1级

    > 主要是映射文档的结构

    + DOM核心 <!--映射基于XML文档结构-->

    + DOM HTML<!--基于DOM核心，添加对HTML的对象和方法-->

  + DOM2级

    > 在原来DOM的基础上又扩充了鼠标和用户界面事件、范围、遍历（迭代DOM文档的方法）等细分模块，通过对象接口增加了对CSS的支持

    + DOM视图（DOM Views）：定义了跟踪不同文档视图的接口
    + DOM事件（DOM Events）：定义了事件和事件处理的接口
    + DOM样式（DOM Style）：定义了基于CSS为元素应用样式的接口
    + DOM遍历和范围（DOM Traversal and Range）：定义了遍历和操作文档树的接口

  + DOM3级

    > 进一步扩展了DOM，引入了以统一方式加载和保存文档的方法；新增了验证文档的方法

 - BOM<!--Browser Object Model 浏览器对象模型-->

   > 提供与浏览器交互的方法和接口

## 数据类型

简单数据类型：Undefined、Null、Boolean、Number、String

复杂数据类型：Object

+ Array

+ Function

+ Date

+ RegExp

+ ...........

  ##### typeof操作符 <!--返回变量数据类型-->

  ### Undefined

  > 表示初始化但未声明的变量，一般不显式赋值，多用于比较

  ### NULL

  > 表示一个空指针**对象** ，多以typeof会显示"object",实际上Undefined是派生自NULL，所以 `null == undefined` 的返回值是`true`

  ### Boolean

  > `true`和`false`区分大小写，`True`和`False`不是`Boolean`值，只是标识符	

  #### 	转化Boolean值 ：`boolean();`函数

  | **数据类型** |        转换为true的值        | 转换为false的值 |
  | :----------: | :--------------------------: | :-------------: |
  |   Boolean    |             true             |      false      |
  |    String    |        任何非空字符串        | “”（空字符串）  |
  |    Number    | 任何非零数字值（包括无穷大） |     0和NaN      |
  |    Object    |           任何对象           |      null       |
  |  Undefined   |                              |    undefined    |

  ### Number 

  > 使用IEEE754格式来表示整数和浮点

  + 整型

    - 十进制    `var num = 10;`
    - 八进制    `var num = 070;`
    - 十六进制    `var num = 0x5f；`

    > 在进行算术计算时，所有的八进制和十六进制都被转化为十进制

  + 浮点型

    > 浮点数最高精度为17位

    `0.1 + 0.2 = 0.30000000000000004` <!--js浮点运算会产生误差-->

  + 数值范围

    最大值： `Number.MIN_VALUE`

    最小值： `Number.MAX_VALUE`

    > 超出数值范围的数会被自动转换成为特殊的`Infinity`值，`Infinity`表示正无穷，`-Infinity`表示负无穷，`Infinity`值无法参加运算，可以用`isFinite();`函数判断数值是否是有穷的。

  + NaN <!--Not a Number-->

    > 表示一个本来要返回数值的操作数未返回数值的情况。

    + 特点

      1. 任何涉及NaN的操作都会返回NaN，除以0的操作也返回NaN

         > 实际上只有NaN / NaN才返回NaN，整数除以NaN返回Infinity，负数除以NaN返回-Infinity

      2. NaN与任何值都不相等，包括他本身

    + 判定：`isNaN();`函数

      + `isNaN( NaN ) == true`
      + `isNaN( 10 ) == false`
      + `isNaN( "10" ) == false` <!--可以被转换成数值10-->
      + `isNaN( "blue" ) == true`
      + `isNaN( true )  == false` <!--可以被转换成数值1-->

  + 数值转换

    1. Number();

       + 如果是布尔值，true和false将分别转为1和0.
       + 如果是数字值，只是简单地传入和返回。
       + 如果是NULL值，返回0.
       + 如果是undefined，返回NaN
       + 如果是字符串：
         1. 如果字符串只包含数字，则将其转化为十进制数值
         2. 如果字符串中包含有效的浮点格式，则将其转化为对应的浮点数值
         3. 如果字符串中包含有效的十六进制格式，则转化为相同大小的十进制形式
         4. 如果字符是空的，则将其转化为0
         5. 如果字符串包含上述格式之外的字符，则将其转化为NaN
       + 如果是对象，则调用valueOf()方法，然后依照前面的规则返回值。如果转换得是NaN，则调用toString();方法。

    2. parseInt();

       > 忽略字符串前面的空格，直到找到第一个非空字符，如果第一个字符不是数字字符或者符号，则返回NaN。否则会直接解析完最后一个数字字符

    3. parsefloat();

       > 与parseInt();类似

  ### String

  + 特点

    > ECMAScript中的字符串是不可变的，要改变，只能先销毁再赋值，也就是覆盖。

  + 转换字符串

    1. `toString();`方法

       > `null`和`undefined`没有这个方法

       参数：null，2，8，10，16     `改变进制`

    2. `String();`方法

  ### Object

  > ECMAScript中的对象其实就是一组数据和功能的集合。

  + 创建对象
    1. `var obj = new Object();`
    2. `var obj = { ... };`
  + Object属性和方法
    + `constructor`：保存着用于创建当前对象的函数
    + `hasOwnProperty( propertyName )`：用于检查给定的属性在当前的对象实例中是否存在
    + `isPropertypeOf( object )`：用于检查传入的对象是否是传入对象的原型
    + `propertyIsEnumerable( propertyName )`：用于检查给定的属性是否能够使用for-in语句来枚举
    + `toLocaleString()`：返回对象的字符串表示，该字符串与执行环境的地区对应
    + `toString()`：返回对象的字符串表示
    + `valueOf()`：返回对象的字符串数值或布尔值表示，通常与`toString()`方法返回的值相同

  ### 语句

  + for-in语句

    + 迭代语句，循环显示BOM中对象的所有属性（无序的）

      > 如果对象中属性值为null或者undefined，则会终止循环

  + with语句

    + 将代码的作用域设置到一个特定的对象中（严格模式不支持）

  ### 函数

  ​	参数：函数可以传入多个参数，而且不需要定义形参接受，他们会被存入伪数组arguments中。

  ​	重载：js函数没有重载，只能覆盖。

  ## 变量、作用域及内存问题

### 