# 读书笔记 | JavaScript 高级程序设计（第四版）




我对自己的定位仍旧是一个后端工程师，学习了解 JavaScript 的原因是，我自己开发项目需要写一些前端。

**就主打一个实用，能实现功能即可**。



## 第1章 什么是JavaScript

❑ JavaScript历史回顾

❑ JavaScript是什么

❑ JavaScript与ECMAScript的关系

❑ JavaScript的不同版本

### 历史

1995年，JavaScript问世。当时，它的主要用途是代替Perl等服务器端语言处理输入验证

它很简单，学会用只要几分钟；它又很复杂，掌握它要很多年。

> Java 和 JavaScript 的关系
>
> 在Netscape Navigator 2正式发布前，网景把 LiveScript 改名为 JavaScript，以便搭上媒体当时热烈炒作Java的顺风车。

### JavaScript 是什么

完整的JavaScript实现包含以下几个部分

![](https://pic.imgdb.cn/item/65a8a008871b83018a4b8d83.jpg)

![image-20240118115119518](JavaScript高级程序设计(第四版).assets/image-20240118115119518.png)

❑ 核心（ECMAScript）

❑ 文档对象模型（DOM）

❑ 浏览器对象模型（BOM）



**ECMAScript**

ECMA-262将这门语言作为一个基准来定义，以便在它之上再构建更稳健的脚本语言

**宿主环境**提供ECMAScript的基准实现和与环境自身交互必需的扩展

Web 浏览器是 ECMAScript 的宿主环境，服务端JavaScript平台Node.js也是宿主环境



不涉及浏览器的话，ECMA-262到底定义了什么？

❑ 语法❑ 类型❑ 语句❑ 关键字❑ 保留字❑ 操作符❑ 全局对象

**ECMAScript只是对实现这个规范描述的所有方面的一门语言的称呼**

> JavaScript实现了ECMAScript，而Adobe ActionScript同样也实现了ECMAScript。



**DOM**

文档对象模型（DOM, Document Object Model）是一个应用编程接口（API），用于在HTML中使用扩展的XML。

DOM将整个页面抽象为一组分层节点。HTML或XML页面的每个组成部分都是一种节点，包含不同的数据

```html
    <html>
        <head>
            <title>Sample Page</title>
        </head>
        <body>
            <p> Hello World! </p>
        </body>
    </html>
```

<img src="https://pic.imgdb.cn/item/65a8a21f871b83018a524f26.jpg" style="zoom: 50%;" />

<u>DOM 的作用</u>

DOM通过创建表示文档的树，让开发者可以随心所欲地控制网页的内容和结构。使用DOM API，可以轻松地删除、添加、替换、修改节点。



**BOM**

浏览器对象模型（BOM）API，用于支持访问和操作浏览器的窗口

使用BOM，开发者可以操控浏览器显示页面之外的部分。

BOM主要针对浏览器窗口和子窗口（frame），不过人们通常会把任何特定于浏览器的扩展都归在BOM的范畴内。比如，下面就是这样一些扩展：

❑ 弹出新浏览器窗口的能力；

❑ 移动、缩放和关闭浏览器窗口的能力；

❑ 对cookie的支持；

❑ 其他自定义对象，如XMLHttpRequest和IE的ActiveXObject。

### 小结

❑ ECMAScript：由ECMA-262定义并提供核心功能。

❑ 文档对象模型（DOM）：提供与网页内容交互的方法和接口。

❑ 浏览器对象模型（BOM）：提供与浏览器交互的方法和接口。

## 第2章 HTML中的JavaScript





## 第3章 语言基础-基于ES6

> ECMA-262第5版（ES5）定义的ECMAScript，是目前为止实现得最为广泛（即受浏览器支持最好）的一个版本。
>
> 第6版（ES6）在浏览器中的实现（即受支持）程度次之。到2017年底，大多数主流浏览器几乎或全部实现了这一版的规范。
>
> 为此，本章接下来的内容==**主要基于ECMAScript第6版**==。

### 语法

ECMAScript的语法很大程度上借鉴了C语言和其他类C语言，如Java和Perl。

#### 区分大小写

ECMAScript中一切都区分大小写。无论是变量、函数名还是操作符，都区分大小写

**变量test和变量Test是两个不同的变量**

#### 标识符

标识符，就是变量、函数、属性或函数参数的名称



规则

❑ 第一个字符必须是一个字母、下划线（_）或美元符号（$）；

❑ 剩下的其他字符可以是字母、下划线、美元符号或数字。



按照惯例，ECMAScript标识符使用驼峰大小写形式

```
    firstSecond
    myCar
    doSomethingImportant
```

⚠注意：关键字、保留字、true、false和null不能作为标识符

#### 注释

```js
// 单行注释

/＊ 这是多行
   注释
＊/
```

#### 严格模式

启用了严格模式，不规范写法会被处理，不安全活动将抛出错误

> ECMAScript 5增加了严格模式（strict mode）的概念



对整个脚本启用严格模式，在脚本开头加上

```js
    "use strict";
```

这是一个预处理指令



指定一个函数启用严格模式

```js
    function doSomething() {
      "use strict";
      // 函数体
    }
```



#### 语句-推荐加分号

**分号**

ECMAScript中的语句以分号结尾。省略分号意味着由解析器确定语句在哪里结尾

```js
    let sum = a + b        // 没有分号也有效，但不推荐
    let diff = a - b;     // 加分号有效，推荐
```



**代码块**

代码块由一个左花括号（{）标识开始，一个右花括号（}）标识结束

```js
    if (test) {
      test = false;
      console.log(test);
    }
```



#### 关键字与保留字

ECMA-262第6版规定的所有关键字如下

```js
    break         do             in               typeof
    case          else          instanceof     var
    catch         export        new              void
    class         extends      return          while
    const         finally      super           with
    continue     for           switch          yield
    debugger     function     this
    default      if             throw
    delete        import        try
```



规范中也描述了一组未来的保留字

```js
    始终保留：
    enum
    严格模式下保留：
    implements   package      public
    interface    protected    static
    let           private
    模块代码中保留：
    await
```

> 这些词汇不能用作标识符，但现在还可以用作对象的属性名。一般来说，最好还是不要使用关键字和保留字作为标识符和属性名，以确保兼容过去和未来的ECMAScript版本。

### 变量

ECMAScript变量是松散类型的，意思是变量可以用于保存任何类型的数据

> 不是强类型

有3个关键字可以声明变量：var、const和let。

其中，var在ECMAScript的所有版本中都可以使用，而**const和let**只能在ECMAScript 6及更晚的版本中使用。



#### var 关键字

```js
    var message;
```

这行代码定义了一个名为message的变量，可以用它**保存任何类型的值**。（不初始化的情况下，变量会保存一个特殊值undefined）



```js
    var message = "hi";
```

> 可以自动推断类型



随后，不仅可以改变保存的值，也可以改变值的类型：

```js
    var message = "hi";
    message=100;  //合法，但不推荐
```



**var声明作用域**

关键的问题在于，使用var操作符定义的变量会成为包含它的函数的**局部变量。**

```js
    function test() {
      var message = "hi"; // 局部变量
    }
    test();
    console.log(message); // 出错！
```



在函数内定义变量时省略var操作符，可以创建一个**全局变量**

```js
    function test() {
      message="hi";     //全局变量
    }
    test();
    console.log(message); // "hi"
```

⚠注意 虽然可以通过省略var操作符定义全局变量，但**不推荐这么做**。在局部作用域中定义的全局变量很难维护，也会造成困惑。这是因为不能一下子断定省略var是不是有意而为之。在严格模式下，如果像这样给未声明的变量赋值，则会导致抛出ReferenceError。



**定义多个变量**

```js
    var message = "hi",
        found = false,
        age = 29;
```

> 插入换行和空格缩进并不是必需的，但这样有利于阅读理解。



**var声明提升**

使用这个关键字声明的变量会自动提升到函数作用域顶部：

```js
    function foo() {
      console.log(age);
      var age = 26;
    }
    foo();   // undefined
```

之所以不会报错，是因为ECMAScript运行时把它看成等价于如下代码：

```js
    function foo() {
      var age;
      console.log(age);
      age = 26;
    }
    foo();   // undefined
```

反复多次使用var声明同一个变量也没有问题：

```js
    function foo() {
      var age = 16;
      var age = 26;
      var age = 36;
      console.log(age);
    }
    foo();   // 36
```

#### let声明

let跟var的作用差不多

**最明显的区别是**，let声明的范围是块作用域，而var声明的范围是函数作用域。

```js
    if (true) {
      var name = 'Matt';
      console.log(name); // Matt
    }
    console.log(name);    // Matt
    if (true) {
      let age = 26;
      console.log(age);    // 26
    }
    console.log(age);      // ReferenceError: age没有定义
```

**另一个重要的区别**，就是let声明的变量不会在作用域中被提升

```js
    // name会被提升
    console.log(name); // undefined
    var name = 'Matt';
    // age不会被提升
    console.log(age); // ReferenceError:age没有定义
    let age = 26;
```

---



let也不允许同一个块作用域中出现**冗余声明**。这样会导致报错

```js
    var name;
    var name;
    let age;
    let age;   // SyntaxError；标识符age已经声明过了
```



**嵌套使用**相同的标识符不会报错

```js
    var name = 'Nicholas';
    console.log(name);     // 'Nicholas'
    if (true) {
      var name = 'Matt';
      console.log(name);   // 'Matt'
    }
    let age = 30;
    console.log(age);     // 30
    if (true) {
      let age = 26;
      console.log(age);   // 26
    }
```



对声明冗余报错不会因**混用let和var**而受影响。这两个关键字声明的并不是不同类型的变量，它们只是指出变量在相关作用域如何存在。

```js
    var name;
    let name; // SyntaxError
    let age;
    var age; // SyntaxError
```



**全局声明**

使用let在全局作用域中声明的变量不会成为window对象的属性（var声明的变量则会）。

```js
    var name = 'Matt';
    console.log(window.name); // 'Matt'
    let age = 26;
    console.log(window.age);   // undefined
```



**条件声明**

> 在使用var声明变量时，由于声明会被提升，JavaScript引擎会自动将多余的声明在作用域顶部合并为一个声明。因为let的作用域是块，所以不可能检查前面是否已经使用let声明过同名变量，同时也就不可能在没有声明的情况下声明它。

```js
    <script>
      var name = 'Nicholas';
      let age = 26;
    </script>
    <script>
      // 假设脚本不确定页面中是否已经声明了同名变量
      // 那它可以假设还没有声明过
      var name = 'Matt';
      // 这里没问题，因为可以被作为一个提升声明来处理
      // 不需要检查之前是否声明过同名变量
      let age = 36;
      // 如果age之前声明过，这里会报错
    </script>
```



**for循环中的let声明**

在let出现之前，迭代变量可以在外面被访问到

```js
    for (var i = 0; i < 5; ++i) {
      // 循环逻辑
    }
    console.log(i); // 5
```

改成使用let之后，这个问题就消失了，因为迭代变量的作用域仅限于for循环块内部：

```js
    for (let i = 0; i < 5; ++i) {
      // 循环逻辑
    }
    console.log(i); // ReferenceError: i没有定义
```



在使用var的时候，最常见的问题就是对迭代变量的奇特声明和修改：

```js
    for (var i = 0; i < 5; ++i) {
        setTimeout(() => console.log(i), 0)
    }
    // 你可能以为会输出0、1、2、3、4
    // 实际上会输出5、5、5、5、5
```

```js
    for (let i = 0; i < 5; ++i) {
        setTimeout(() => console.log(i), 0)
    }
    // 会输出0、1、2、3、4
```

#### const声明

const的行为与let基本相同，唯一一个重要的区别是用它**声明变量时必须同时初始化变量**，且尝试**修改const声明的变量会导致运行时错误**。

```js
    const age = 26;
    age = 36; // TypeError：给常量赋值
    // const也不允许重复声明
    const name = 'Matt';
    const name = 'Nicholas'; // SyntaxError
    // const声明的作用域也是块
    const name = 'Matt';
    if (true) {
      const name = 'Nicholas';
    }
    console.log(name); // Matt
```



const声明的限制只适用于它指向的变量的引用。换句话说，**如果const变量引用的是一个对象，那么修改这个对象内部的属性并不违反const的限制**。

```js
    const person = {};
    person.name = 'Matt';   // ok
```



虽然const变量跟let变量很相似，但是不能用const来声明迭代变量（因为迭代变量会自增）

```js
    for (const i = 0; i < 10; ++i) {} // TypeError：给常量赋值
```

#### ⭐声明风格及最佳实践

- **不使用var**
- **const优先，let次之**

对变量有修改的话使用 let，当然修改的是对象内部属性还是继续用 const

### 数据类型

ECMAScript有6种简单数据类型（也称为原始类型）: Undefined、Null、Boolean、Number、String和Symbol。Symbol（符号）是ECMAScript 6新增的。

还有一种复杂数据类型叫Object（对象）。Object是一种无序名值对的集合

#### typeof操作符

**确定任意变量数据类型**

对一个值使用typeof操作符会返回下列字符串之一：❑ "undefined"表示值未定义；❑ "boolean"表示值为布尔值；❑ "string"表示值为字符串；❑ "number"表示值为数值；❑ "object"表示值为对象（而不是函数）或null；❑ "function"表示值为函数；❑ "symbol"表示值为符号。

```js
    let message = "some string";
    console.log(typeof message);     // "string"
    console.log(typeof(message));    // "string"
    console.log(typeof 95);           // "number"
```

注意，因为typeof是一个操作符而不是函数，所以不需要参数（但可以使用参数）。

注意typeof在某些情况下返回的结果可能会让人费解，但技术上讲还是正确的。比如，调用typeof null返回的是"object"。这是因为特殊值null被认为是一个对空对象的引用。

#### Undefined类型

Undefined类型只有一个值，就是特殊值undefined。

当使用var或let声明了变量但没有初始化时，就相当于给变量赋予了undefined值：

```js
    let message;
    console.log(message == undefined); // true
```



**undefined是一个假值。因此，如果需要，可以用更简洁的方式检测它**

> 不过要记住，也有很多其他可能的值同样是假值。所以一定要明确自己想检测的就是undefined这个字面值，而不仅仅是假值。

```js
    let message; // 这个变量被声明了，只是值为undefined
    // age没有声明
    if (message) {
      // 这个块不会执行-----------有数据返回时的处理
    }
    if (! message) {
      // 这个块会执行
    }
    if (age) {
      // 这里会报错
    }
```

#### Null类型-对象类型

Null类型同样只有一个值，即特殊值null。逻辑上讲，**null值表示一个空对象指针**，这也是给typeof传一个null会返回"object"的原因：

```js
    let car = null;
    console.log(typeof car);   // "object"
```

**在定义将来要保存对象值的变量时，建议使用null来初始化，不要使用其他值**

这样，只要检查这个变量的值是不是null就可以知道这个变量是否在后来被重新赋予了一个对象的引用，比如：

```js
    if (car ! = null) {
      // car是一个对象的引用
    }
```

**用等于操作符（==）比较null和undefined始终返回true**。但要注意，这个操作符会为了比较而转换它的操作数



**假值检测**

```js
    let message = null;
    let age;
    if (message) {
      // 这个块不会执行
    }
    if (! message) {
      // 这个块会执行
    }
    if (age) {
      // 这个块不会执行
    }
    if (! age) {
      // 这个块会执行
    }
```



##### null和undefined

永远不必显式地将变量值设置为undefined。

任何时候，只要变量要保存对象，而当时又没有那个对象可保存，就要用null来填充该变量。这样就可以保持null是空对象指针的语义，并进一步将其与undefined区分开来。



#### Boolean类型

有两个字面值：true和false。这两个布尔值不同于数值，因此true不等于1，false不等于0。

```js
    let found = true;
    let lost = false;
```

⚠注意：区分大小写



转换布尔值

```js
    let message = "Hello world! ";
    let messageAsBoolean = Boolean(message);
```

**不同类型与布尔值之间的转换规则**

![](https://pic.imgdb.cn/item/65a8af10871b83018a7bed67.jpg)

![image-20240118125417737](JavaScript高级程序设计(第四版).assets/image-20240118125417737.png)



#### Number类型

Number类型使用IEEE 754格式表示整数和浮点值（在某些语言中也叫双精度值）

```js
    let octalNum1 = 070;   // 八进制的56
    let octalNum2 = 079;   // 无效的八进制值，当成79 处理
    let octalNum3 = 08;    // 无效的八进制值，当成8 处理
```



**浮点值**

要定义浮点值，数值中必须包含小数点，而且小数点后面必须至少有一个数字

```js
    let floatNum1 = 1.1;
    let floatNum2 = 0.1;
    let floatNum3 = .1;    // 有效，但不推荐
```

科学计数法

```js
    let floatNum = 3.125e7; // 等于31250000
```



**永远不要测试某个特定的浮点值**。

```js
    if (a + b == 0.3) {        // 别这么干！
      console.log("You got 0.3.");
    }
```

如果两个数值分别是0.05和0.25，或者0.15和0.15，那没问题。但如果是0.1和0.2，如前所述，测试将失败



**值的范围**

ECMAScript可以表示的最小数值保存在Number.MIN_VALUE中，这个值在多数浏览器中是5e-324；可以表示的最大数值保存在Number.MAX_VALUE中，这个值在多数浏览器中是1.797693134862315 7e+308。



**NaN**

有一个特殊的数值叫NaN，意思是“不是数值”（Not a Number），用于表示本来要返回数值的操作失败了（而不是抛出错误）

```js
    console.log(0/0);     // NaN
    console.log(-0/+0);   // NaN
```



**数值转换**

有3个函数可以将非数值转换为数值：Number()、parseInt()和parseFloat()。Number()是转型函数，可用于任何数据类型。后两个函数主要用于将字符串转换为数值。

Number()函数基于如下规则执行转换。

```js
    let num1 = Number("Hello world! ");   // NaN
    let num2 = Number("");                  // 0
    let num3 = Number("000011");          // 11
    let num4 = Number(true);               // 1
```

考虑到用Number()函数转换字符串时相对复杂且有点反常规，**通常在需要得到整数时可以优先使用parseInt()函数**

parseInt()函数更专注于字符串是否包含数值模式。字符串最前面的空格会被忽略，从第一个非空格字符开始转换。如果第一个字符不是数值字符、加号或减号，parseInt()立即返回NaN。这意味着空字符串也会返回NaN（这一点跟Number()不一样，它返回0）

```js
    let num1 = parseInt("1234blue");   // 1234
    let num2 = parseInt("");             // NaN
    let num3 = parseInt("0xA");         // 10，解释为十六进制整数
    let num4 = parseInt(22.5);          // 22
    let num5 = parseInt("70");          // 70，解释为十进制值
    let num6 = parseInt("0xf");         // 15，解释为十六进制整数

    let num1 = parseInt("10", 2);    // 2，按二进制解析
    let num2 = parseInt("10", 8);    // 8，按八进制解析
    let num3 = parseInt("10", 10);   // 10，按十进制解析
    let num4 = parseInt("10", 16);   // 16，按十六进制解析
```



parseFloat()函数的工作方式跟parseInt()函数类似，都是从位置0开始检测每个字符。同样，它也是解析到字符串末尾或者解析到一个无效的浮点数值字符为止。

parseFloat()函数的另一个不同之处在于，它始终忽略字符串开头的零。

```js
    let num1 = parseFloat("1234blue");   // 1234，按整数解析
    let num2 = parseFloat("0xA");         // 0
    let num3 = parseFloat("22.5");        // 22.5
    let num4 = parseFloat("22.34.5");    // 22.34
    let num5 = parseFloat("0908.5");     // 908.5
    let num6 = parseFloat("3.125e7");    // 31250000
```

#### String类型

String（字符串）数据类型表示零或多个16位Unicode字符序列。字符串可以使用双引号（"）、单引号（'）或反引号（`）标示，因此下面的代码都是合法的：

```js
    let firstName = "John";
    let lastName = 'Jacob';
    let lastName = `Jingleheimerschmidt`
```

不过要注意的是，以某种引号作为字符串开头，必须仍然以该种引号作为字符串结尾



**ECMAScript中的字符串是不可变的（immutable**），意思是一旦创建，它们的值就不能变了。要修改某个变量中的字符串值，必须先销毁原始的字符串，然后将包含新值的另一个字符串保存到该变量

##### 字符字面量

![](https://pic.imgdb.cn/item/65a8b4a4871b83018a8e6740.jpg)

![img](https://res.weread.qq.com/wrepub/epub_34336683_14)



##### 长度

```js
    console.log(text.length); // 28
```

##### 转换为字符串

首先是使用几乎所有值都有的**toString()方法**。这个方法唯一的用途就是返回当前值的字符串等价物

```js
    let age = 11;
    let ageAsString = age.toString();        // 字符串"11"
    let found = true;
    let foundAsString = found.toString();   // 字符串"true"
```



如果你不确定一个值是不是null或undefined，可以使用**String()转型函数**，它始终会返回表示相应类型值的字符串

```js
    let value1 = 10;
    let value2 = true;
    let value3 = null;
    let value4;
    console.log(String(value1)); // "10"
    console.log(String(value2));   // "true"
    console.log(String(value3));   // "null"
    console.log(String(value4));   // "undefined"
```

##### 模板字面量

ECMAScript 6新增了使用模板字面量定义字符串的能力。与使用单引号或双引号不同，模板字面量保留换行字符，可以跨行定义字符串：

```js
    let myMultiLineString = 'first line\nsecond line';
    let myMultiLineTemplateLiteral = `first line
    second line`;
    console.log(myMultiLineString);
    // first line
    // second line"
    console.log(myMultiLineTemplateLiteral);
    // first line
    // second line
    console.log(myMultiLineString === myMultiLinetemplateLiteral); // true
```

由于模板字面量会保持**反引号**内部的空格，因此在使用时要格外注意。格式正确的模板字符串看起来可能会缩进不当

##### **字符串插值**

模板字面量最常用的一个特性是支持字符串插值，也就是可以在一个连续定义中插入一个或多个值

字符串插值通过在${}中使用一个JavaScript表达式实现：

```js
    let value = 5;
    let exponent = 'second';
    // 以前，字符串插值是这样实现的：
    let interpolatedString =
      value + ' to the ' + exponent + ' power is ' + (value ＊ value);
    // 现在，可以用模板字面量这样实现：
    let interpolatedTemplateLiteral =
      `${ value } to the ${ exponent } power is ${ value ＊ value }`;
    console.log(interpolatedString);              // 5 to the second power is 25
    console.log(interpolatedTemplateLiteral);   // 5 to the second power is 25
```

**所有插入的值都会使用toString()强制转型为字符串，而且任何JavaScript表达式都可以用于插值**



```js
    let foo = { toString: () => 'World' };
    console.log(`Hello, ${ foo }! `);        // Hello, World!
```



在插值表达式中可以调用函数和方法：

```js
    function capitalize(word) {
      return `${ word[0].toUpperCase() }${ word.slice(1) }`;
    }
    console.log(`${ capitalize('hello') }, ${ capitalize('world') }! `); // Hello, World!
```

##### 模板字面量标签函数

```js
    let a = 6;
    let b = 9;
    function simpleTag(strings, aValExpression, bValExpression, sumExpression) {
      console.log(strings);
      console.log(aValExpression);
      console.log(bValExpression);
      console.log(sumExpression);
      return 'foobar';
    }
    let untaggedResult = `${ a } + ${ b } = ${ a + b }`;
    lettaggedResult=simpleTag`${a}+${b}=${a+b}`;
    // ["", " + ", " = ", ""]
    // 6
    // 9
    // 15
    console.log(untaggedResult);    // "6 + 9 = 15"
    console.log(taggedResult);      // "foobar"
```

##### 原始字符串

使用模板字面量也可以直接获取原始的模板字面量内容（如换行符或Unicode字符），而不是被转换后的字符表示。为此，可以使用默认的String.raw标签函数：

```js
    // Unicode示例
    // \u00A9 是版权符号
    console.log(`\u00A9`);               // ©
    console.log(String.raw`\u00A9`);   // \u00A9
    // 换行符示例
    console.log(`first line\nsecond line`);
    // first line
    // second line
    console.log(String.raw`first line\nsecond line`); // "first line\nsecond line"
    // 对实际的换行符来说是不行的
    // 它们不会被转换成转义序列的形式
    console.log(`first line
    second line`);
    // first line
    // second line
    console.log(String.raw`first line
    second line`);
    // first line
    // second line
```

另外，也可以通过标签函数的第一个参数，即字符串数组的．raw属性取得每个字符串的原始内容：

```js
    function printRaw(strings) {
      console.log('Actual characters:');
      for (const string of strings) {
        console.log(string);
      }
      console.log('Escaped characters; ');
      for (const rawString of strings.raw) {
        console.log(rawString);
      }
    }
    printRaw`\u00A9${ 'and' }\n`;
    // Actual characters:
    // ©
    //（换行符）
    // Escaped characters:
    // \u00A9
    // \n
```

####  Symbol类型

符号是原始值，且符号实例是唯一、不可变的。符号的用途是确保对象属性使用唯一标识符，不会发生属性冲突的危险。

符号就是用来创建唯一记号，进而用作非字符串形式的对象属性。



**符号的基本用法**

符号需要使用Symbol()函数初始化。因为符号本身是原始类型，所以typeof操作符对符号返回symbol。

```js
    let sym = Symbol();
    console.log(typeof sym); // symbol
```

调用Symbol()函数时，也可以传入一个字符串参数作为对符号的描述（description），将来可以通过这个字符串来调试代码。但是，这个字符串参数与符号定义或标识完全无关：

```js
    let genericSymbol = Symbol();
    let otherGenericSymbol = Symbol();
    let fooSymbol = Symbol('foo');
    let otherFooSymbol = Symbol('foo');
    console.log(genericSymbol == otherGenericSymbol);   // false
    console.log(fooSymbol == otherFooSymbol);             // false
```



未完



#### Object类型

```js
    let o = new Object();
```

Object的实例本身并不是很有用，但理解与它相关的概念非常重要。类似Java中的java.lang. Object, ECMAScript中的Object也是派生其他对象的基类。Object类型的所有属性和方法在派生的对象上同样存在。



### 函数

ECMAScript中的函数使用function关键字声明，后跟一组参数，然后是函数体。

**函数的基本语法**

```js
    function functionName(arg0, arg1, ..., argN) {
      statements
    }
```

```js
    function sayHi(name, message) {
      console.log("Hello " + name + ", " + message);
    }
```

**函数调用**

```js
    sayHi("Nicholas", "how are you today? ");
```



**有返回值的函数**

ECMAScript中的函数不需要指定是否返回值。任何函数在任何时间都可以使用return语句来返回函数的值，用法是后跟要返回的值

```js
    function sum(num1, num2) {
      return num1 + num2;
    }

    const result = sum(5, 10);
```

要注意的是，只要碰到return语句，函数就会立即停止执行并退出。因此，return语句后面的代码不会被执行





## 第10章 函数

**函数实际上是对象**，每个函数都是Function类型的实例

因为函数是对象，所以函数名就是指向函数对象的指针，而且不一定与函数本身紧密绑定

### 定义函数的方式

```js
    function sum (num1, num2) {
      return num1 + num2;
    }
```



**函数表达式**

```js
    let sum = function(num1, num2) {
      return num1 + num2;
    };
```

> 注意这里的函数末尾是有分号的，与任何变量初始化语句一样



**“箭头函数”（arrow function）**

```js
    let sum = (num1, num2) => {
      return num1 + num2;
    };
```



### 箭头函数


