
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [《JavaScript高级程序设计(第三版)》学习笔记](#javascript高级程序设计第三版学习笔记)
* [基础知识整理](#基础知识整理)
	* [第三章 基本概念](#第三章-基本概念)
		* [一、语法](#一-语法)
		* [二、变量](#二-变量)
		* [三、数据类型](#三-数据类型)
		* [四、函数](#四-函数)
	* [第四章 变量、作用域和内存问题](#第四章-变量-作用域和内存问题)
		* [一、基本类型和引用类型的值](#一-基本类型和引用类型的值)
		* [二、执行环境及作用域](#二-执行环境及作用域)
	* [第五章 引用类型](#第五章-引用类型)
		* [一、Object 类型](#一-object-类型)
		* [二、Array 类型](#二-array-类型)
		* [三、Date 类型](#三-date-类型)
		* [四、RegExp 类型](#四-regexp-类型)
		* [五、Function 类型](#五-function-类型)
		* [六、基本包装类型](#六-基本包装类型)
	* [第六章 面向对象的程序设计](#第六章-面向对象的程序设计)
		* [一、理解对象](#一-理解对象)
		* [二、创建对象](#二-创建对象)
		* [三、继承](#三-继承)
	* [第七章 函数表达式](#第七章-函数表达式)
		* [一、递归](#一-递归)
		* [二、闭包](#二-闭包)
		* [三、模仿块级作用域](#三-模仿块级作用域)
		* [四、私有变量](#四-私有变量)
	* [第八章 BOM](#第八章-bom)

<!-- /code_chunk_output -->

# 《JavaScript高级程序设计(第三版)》学习笔记

**作者简介：**

  Nicholas C. Zakas（尼古拉斯•泽卡斯）世界顶级Web技术专家，现为雅虎公司界面呈现架构师，负责My Yahoo!和雅虎首页等大访问量站点的设计。

  尼古拉斯拥有丰富的Web开发和界面设计经验，曾经参与许多世界级大公司的Web解决方案开发。他还是High Performance JavaScript一书的作者，并与他人合作撰写了Professional Ajax和Even Faster Web Sites。

  尼古拉斯拥有梅里马克学院计算机科学学士学位和埃迪柯特学院的MBA学位。他的个人网站是：<u>[www.nczonline.net](www.nczonline.net)</u>，他的Twitter别名是 @slicknet 。

<br>

**前言：**

阅读本书主要是为了弥补自己在 `JavaScript` 基础知识上的不足，希望系统的加深学习，并记录自己在阅读过程中的收获以及思考。

> 注：笔记只是记录自己不懂或忽略的只是，其他内容不记录在内

<br>
<br>
<br>

# 基础知识整理

## 第三章 基本概念

### 一、语法

`ECMAScript` 的语法大量借鉴了 `C` 及其他类 `C` 语言（如 `Java` ）的语法。

<br>


***1. 区分大小写***

- `ECMAScript` 中的一切（变量、函数名和操作符）都要区分大小写。

<br>

***2. 标识符***

- **标识符**：指变量、函数、属性的名字，或者函数的参数。

按照惯例，`ECMAScript` 标识符采用驼峰大小写格式，也就是第一个字母小写，剩下的每个单词的首字母大写。比如：
```
firstSecond
myCar
doSomethingImportant
```
虽然没有谁强制要求必须采用这种格式，但为了与 `ECMAScript` 内置的函数和对象命名格式保持一致，可以将其当作一种最佳实践。

<br>

***3. 语句***

`ECMAScript` 中的语句以一个分号结尾；如果省略分号，则由解析器确定语句的结尾。虽然语句结尾的分号不是必需的，但我们建议任何时候都不要省略它,因为:
```
  1、可以避免 很多错误（例如不完整的输入）；
  2、开发人员可以放心地通过删除多余的空格来压缩 `ECMAScript` 代码（代码行结尾处没有分号会导致压缩错误）；
  3、加上分号也会在某些情况下增进代码的性能，因为解析器不必再花时间推测应该在哪里插入分号了；
```

<br>

### 二、变量

`ECMAScript` 的变量是松散类型的，可以用来保存任何类型的数据。

- 用 `var` 操作符定义的变量将成为定义该变量的作用域中的局部变量;

- 省略 `var` 操作符可以定义全局变量，但局部作用域中定义的全局变量很难维护;

<br>

### 三、数据类型

`ECMAScript` 可以用 `typeof` 操作符来检测给定变量的数据类型。

**注意：**`typeof` 是一个操作符而不是函数，因此例子中的圆括号尽管可以使用，但不是必需的。比如：
```JavaScript
var message = "some string";
alert(typeof message);   // "string"
alert(typeof(message));  // "string"
alert(typeof 95);        // "number"
```

<br>

***1. Undefined类型***

Undefined类型只有一个值，即特殊的 `undefined`。

- 对未初始化的变量执行 `typeof` 操作符将返回 `undefined` 值；

- 对未声明的变量执行 `typeof` 操作符将返回 `undefined` 值；

**注意**：显式地初始化变量依然是明智的选择，因为当 `typeof` 操作符返回"undefined"值时， 我们就知道被检测的变量还没有被声明，而不是尚未初始化。

<br>

***2. Null类型***

Null类型只有一个值，这个特殊的值是 `null`。**从逻辑角度来看，`null` 值表示一个空对象指针，而这也正是使用 `typeof` 操作符检测 `null` 值时会返回"object"的原因。** 比如：

```JavaScript
var car = null;
alert(typeof car);   // "object"
```

如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为 `null` 而不是其他值。这样一来，只要直接检查 `null` 值就可以知道相应的变量是否已经保存了一个对象的引用，比如：

```JavaScript
var car = null;
if (car != null) {
  // 对 car 对象执行某些操作
}
```

**注意**：`undefined` 值是派生自 `null` 值的，因此 `ECMA-262` 规定对它们的相等性测试要返回 `true`，比如：

```JavaScript
alert(null == undefined);   //true
```

尽管 `null` 和 `undefined` 有这样的关系，但它们的用途完全不同。无论在什么情况下，都没有必要把一个变量的值显式地设置为 `undefined`，可是同样的规则对 `null` 却不适用。

换句话说，只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存 `null` 值。这样做不仅可以体现 `null` 作为空对象指针的惯例，而且也有助于进一步区分 `null` 和 `undefined`。

<br>

***3. Boolean类型***

Boolean类型只有两个字面值：`true` 和 `false`。下表给出了各种数据类型及其对应的转换规则：

| 数据类型 | 转换为true的值 | 转换为false的值 |
| :------: | :------: | :------: |
| Boolean | true | false |
| String | 任何非空字符串 | ""（空字符串） |
| Number | 任何非零数字值（包括无穷大） | 0和NaN |
| Object | 任何对象 | null |
| Undefined | N/A | undefined |

这些转换规则对理解流控制语句（如 `if` 语句）自动执行相应的 `Boolean` 转换非常重要，因为错误地使用一个对象而不是一个 `Boolean` 值，就有可能彻底改变应用程序的流程。

<br>

***4. Number类型***

Number类型使用 `IEEE754` 格式来表示整数和浮点数值（浮点数值在某些语言中也被称为双精度数值）。为支持各种数值类型，`ECMA-262` 定义了不同的数值字面量格式。比如：

```js
var intNum = 55;        // 整数
var octalNum1 = 070;    // 八进制的 56
var octalNum2 = 079;    // 无效的八进制数值——解析为 79
var octalNum3 = 08;     // 无效的八进制数值——解析为 8
var hexNum1 = 0xA;      // 十六进制的 10
var hexNum2 = 0x1f;     // 十六进制的 31
```

**注意**：在进行算术计算时，所有以八进制和十六进制表示的数值最终都将被转换成十进制数值。

<br>

- **浮点数值：**

**<u><font color="red">由于保存浮点数值需要的内存空间是保存整数值的两倍，因此 `ECMAScript` 会不失时机地将浮点数值转换为整数值。</font></u>** 比如：

```js
var floatNum1 = 1.;     // 小数点后面没有数字——解析为 1
var floatNum2 = 10.0;   // 整数——解析为 10
```

- **数值范围：**

由于内存的限制，`ECMAScript` 并不能保存世界上所有的数值。如果某次计算的 结果得到了一个超出 JavaScript 数值范围的值，那么这个数值将被自动转换成特殊的 `Infinity` 值。

- **NaN：**

NaN，即非数值（Not a Number），是一个特殊的数值，这个数值用于表示一个本来要返回数值的操作数未返回数值的情况（这样就不会抛出错误了）。它有两个特点：

```
  a、任何涉及 NaN 的操作（例如 NaN/10）都会返回 NaN；
  b、NaN 与任何值都不相等，包括 NaN 本身；
```

- **数值转换：**

有 3 个函数可以把非数值转换为数值：`Number()`、`parseInt()` 和 `parseFloat()`。

**Number()函数的转换规则如下:**

```
  如果是 Boolean 值，true 和 false 将分别被转换为 1 和 0。
  如果是数字值，只是简单的传入和返回。
  如果是 null 值，返回 0。
  如果是 undefined，返回 NaN。
  如果是字符串，遵循下列规则：
     如果字符串中只包含数字（包括前面带正号或负号的情况），则将其转换为十进制数值，即 "1" 会变成 1，"123"会变成 123，而"011"会变成 11（注意：前导的零被忽略了）；
     如果字符串中包含有效的浮点格式，如"1.1"，则将其转换为对应的浮点数值（同样，也会忽略前导零）；
     如果字符串中包含有效的十六进制格式， 例如 "0xf" ， 则将其转换为相同大小的十进制整数值；
     如果字符串是空的（不包含任何字符），则将其转换为 0；
     如果字符串中包含除上述格式之外的字符，则将其转换为 NaN。
  如果是对象，则调用对象的 valueOf() 方法，然后依照前面的规则转换返回的值。如果转换的结果是NaN，则调用对象的 toString() 方法，然后再次依照前面的规则转换返回的字符串值。
```

 由于 `Number()` 函数在转换字符串时比较复杂而且不够合理，因此在处理整数的时候更常用的是 `parseInt()` 函数。

 <br>

 **parseInt()函数的转换规则如下:**

 ```
   parseInt()函数在转换字符串时，更多的是看其是否符合数值模式。它会忽略字符串前面的空格，直至找到第一个非空格字符；
   如果第一个字符不是数字字符或者负号，parseInt() 就会返回 NaN；
   用 parseInt() 转换空字符串会返回 NaN（ Number()对空字符返回 0）；
   如果第一个字符是数字字符，parseInt()会继续解析第二个字符，直到解析完所有后续字符或者遇  
  到了一个非数字字符；
 ```

举例如下：

```JavaScript
var num1 = parseInt("1234blue");    // 1234
var num2 = parseInt("");            // NaN
var num3 = parseInt("0xA");         // 10（十六进制数）
var num4 = parseInt(22.5);          // 22
var num5 = parseInt("070");         // 56（八进制数）
var num6 = parseInt("70");          // 70（十进制数）
var num7 = parseInt("0xf");         // 15（十六进制数）
```

在 `ECMAScript 5` JavaScript 引擎中，`parseInt()` 已经不具有解析八进制值的能力，因此前导的 0 会被认为无效，为了消除在使用 `parseInt()` 函数时可能导致的上述困惑，可以为这个函数提供第二个参数：

```js
var num = parseInt("0xAF", 16);   //175
var num1 = parseInt("AF", 16);    //175
var num2 = parseInt("AF");        //NaN
```

**注意**：指定基数会影响到转换的输出结果。比如：

```js
var num1 = parseInt("10", 2);     //2 （按二进制解析）
var num2 = parseInt("10", 8);     //8 （按八进制解析）
var num3 = parseInt("10", 10);    //10 （按十进制解析）
var num4 = parseInt("10", 16);    //16 （按十六进制解析）
```

不指定基数意味着让 `parseInt()` 决定如何解析输入的字符串，因此为了避免错误的解析，我们建议无论在什么情况下都明确指定基数。

<br>

**parseFloat()函数的转换规则如下:**

```
  与parseInt()函数类似，parseFloat() 也是从第一个字符（位置 0）开始解析每个字符；
  parseFloat()会一直解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止；
  字符串中的第一个小数点是有效的，而第二个小数点就是无效的；
  parseFloat()始终都会忽略前导的 0 ；
  parseFloat()可以识别前面讨论过的所有浮点数值格式，也包括十进制整数格式。但十六进制格式的字符串则始终会被转换成 0；
  parseFloat()只解析十进制值，因此没有第二个参数指定基数的用法；
  如果字符串包含的是一个可解析为整数的数（没有小数点，或者小数点后 都是零），  
  parseFloat()会返回整数；
```

举例如下：
```js
var num1 = parseFloat("1234blue");    //1234 （整数）
var num2 = parseFloat("0xA");         //0
var num3 = parseFloat("22.5");        //22.5
var num4 = parseFloat("22.34.5");     //22.34
var num5 = parseFloat("0908.5");      //908.5
var num6 = parseFloat("3.125e7");     //31250000
```

<br>

***5. String类型***

`ECMAScript` 中用双引号表示的字符串和用单引号表示的字符串完全相同。

- **字符串的特点：**

`ECMAScript` 中的字符串是不可变的，一旦创建，它们的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个包含新值的字符串填充该变量；

<br>

- **转换为字符串：**

把一个值转换为一个字符串有两种方式：

**toString()方法**

```js
var num = 10;
alert(num.toString());      // "10"（默认情况）
alert(num.toString(2));     // "1010" （二进制）
alert(num.toString(8));     // "12" （八进制）
alert(num.toString(10));    // "10" （十进制）
alert(num.toString(16));    // "a" （十六进制）
```

<br>

**String()方法**
```
  如果值有 toString()方法，则调用该方法（没有参数）并返回相应的结果；
  如果值是 null，则返回"null"；
  如果值是 undefined，则返回"undefined"。
```

`null` 和 `undefined` 没有 `toString()` 方法，所以 `String()` 函数就返回了这两个值的字面量。

举例如下：

```js
var value1 = 10;    alert(String(value1));     // "10"
var value2 = true;  alert(String(value2));     // "true"
var value3 = null;  alert(String(value3));     // "null"
var value4;         alert(String(value4));     // "undefined"
```

<br>

***6. Object类型***

`ECMAScript` 中的对象其实就是一组数据和功能的集合。对象可以通过执行 `new` 操作符后跟要创建的对象类型的名称来创建。

**<u><font color="red">Object 的每个实例都具有下列属性和方法：</font></u>**

```
  constructor：保存着用于创建当前对象的函数，构造函数（constructor）就是 Object()；
  hasOwnProperty(propertyName)：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。其中，作为参数的属性名（propertyName）必须以字符串形式指定（例如：o.hasOwnProperty("name")）；
  isPrototypeOf(object)：用于检查传入的对象是否是传入对象的原型；
  propertyIsEnumerable(propertyName)：用于检查给定的属性是否能够使用 for-in 语句来枚举。与 hasOwnProperty()方法一样，作为参数的属性名必须以字符串形式指定；
  toLocaleString()：返回对象的字符串表示，该字符串与执行环境的地区对应；
  toString()：返回对象的字符串表示；
  valueOf()：返回对象的字符串、数值或布尔值表示。通常与 toString() 方法的返回值相同；
```

<br>

### 四、函数

`ECMAScript` 中的函数使用 `function` 关键字来声明，通过函数可以封装任意多条语句，而且可以在 **<font color="#282828">任何地方</font>** 、 **<font color="#282828">任何时候</font>** 调用执行。

<br>

***1. 参数***

**<u><font color="red">`ECMAScript` 函数不限制参数数量，也不限制参数的数据类型</font></u>**。即便定义的函数只接收两个参数，但在调用这个函数时也未必一定要传递两个参数。

也就是说，我们可以向 `ECMAScript` 函数传递任意数量的参数，并且可以通过 `arguments` 对象来访问这些参数。

**<u><font color="#282828">`ECMAScript` 中的参数在内部是用一个数组来表示的，函数接收到的始终都是这个数组，而不关心数组中包含哪些参数（如果有参数的话）。</font></u>**

<br>

**<u><font color="red">`ECMAScript` 函数的两个重要特点：</font></u>**

```
a、命名的参数只提供便利，但不是必需的；
b、解析器不会验证命名参数；
```

举例如下：

```js
function howManyArgs() {
  alert(arguments.length);
}

howManyArgs("string", 45);    //2
howManyArgs();                //0
howManyArgs(12);              //1
```

<br>

***2. 返回值***

**<u><font color="red">`ECMAScript` 函数无须指定函数的返回值，因为任何函数都可以在任何时候返回任何值。 实际上，未指定返回值的函数返回的是一个特殊的 `undefined` 值</font></u>**。

<br>

***3. ECMAScript没有重载***

**函数重载**：指函数的方法名相同，但参数不同。

如前所述，`ECMAScirpt` 函数没有签名，因为其参数是由包含零或多个值的数组来表示的。所以 **<u><font color="#282828">真正的重载</font></u>** 是不可能做到的。

但是，我们可以通过 **<u><font color="red">检查传入函数中参数的类型和数量并作出不同的反应，来模仿方法的重载。</font></u>**

举例如下：

```js
function doAdd (){
    if(arguments.length === 1){
        alert(arguments[0] + 10);
    }           // 检查参数的长度
    else if (arguments.length === 2){
        alert(arguments[0] + arguments[1]);
    }           // 检查参数的长度
}
doAdd(10);      //20
doAdd(10,20);   //30
```

将上面的代码进行修改完善，如下：

```js
// addMethod - By John Resig (MIT Licensed)
function addMethod(object, name, fn){
    var old = object[ name ];
    object[ name ] = function(){
        if ( fn.length == arguments.length )
            return fn.apply( this, arguments );
        else if ( typeof old == 'function' )
            return old.apply( this, arguments );
    };
}
```

所谓 `addMethod` 函数，简单的理解，就是给某个object，添加一个指定name的函数fn。它利用了闭包，可以通过old变量将先后绑定的函数链接起来。

<br>

**一个巧妙的办法实现重载：**

这个方法来自：JQuery之父John Resig写的《secrets of the JavaScript ninja》这本书。

关于函数重载的总结：<u>[JavaScript 函数重载的实现](https://github.com/Seiya-1314/studyNotes/tree/master/JavaScript/notes/JavaScript函数重载.md) </u>

**<u><font color="red">addMethod 函数的秘诀之一在于 fn.length</font></u>** 。所有函数都有一个length属性，它的值等于定义函数时的参数个数。比如，当你定义的函数只有1个参数时，其length属性为1。

<br>
<br>
<br>
<br>
<br>

## 第四章 变量、作用域和内存问题

JavaScript 的变量与其他语言的变量有很大区别。变量松散类型的本质，决定了它只是在特定时间用于保存特定值的一个名字而已。

由于不存在定义某个变量必须要保存何种数据类型值的规则，变量的值及其数据类型可以在脚本的生命周期内改变。尽管 从某种角度看，这可能是一个既有趣又强大，同时又容易出问题的特性，但 JavaScript 变量实际的复杂 程度还远不止如此。

<br>

### 一、基本类型和引用类型的值

`ECMAScript` 变量包含两种不同数据类型的值：

- **基本类型值** (简单的数据段)：Undefined、Null、Boolean、Number 和 String；
- **引用类型值** (由多个值构成的对象)：Object；

**<u><font color="red">在将一个值赋给变量时，解析器必须确定这个值是基本类型值还是引用类型值</font></u>** 。基本数据类型是按值访问的，因为可以操作保存在变量中的实际的值，因此被保存在 **栈内存** 中。

引用类型的值是保存在内存中的对象，保存在 **堆内存** 中。包含引用类型值的变量实际上包含的并不是对象本身，而是一个指向该对象的指针。与其他语言不同，**<u><font color="red">JavaScript 不允许直接访问内存中的位置，也就是说不能直接操作对象的内存空间</font></u>**。在操作对象时，实际上是在操作对象的引用而不是实际的对象。为此，引用类型的值是按引用访问的。

> 注意：在很多语言中， 字符串以对象的形式来表示， 因此被认为是引用类型的。 ECMAScript 放弃了这一传统。

<br>

***1. 传递参数***

**`ECMAScript` 中所有函数的参数都是按值传递的**。也就是说，把函数外部的值复制给函数内部的参数，就和把值从一个变量复制到另一个变量一样。

基本类型值的传递如同基本类型变量的复制一样，而引用类型值的传递，则如同引用类型变量的复制一样。

<br>

<u>**在向参数传递基本类型的值时，被传递的值会被复制给一个局部变量**</u>（用 `ECMAScript`的概念来说，就是 arguments 对象中的一个元素）。举例如下：

```js
function addTen(num) {
  num += 10; return num;
}

var count = 20;
var result = addTen(count);
alert(count);    //20，没有变化
alert(result);   //30
```

<u>**在向参数传递引用类型的值时，会把这个值在内存中的地址复制给一个局部变量，因此这个局部变量的变化会反映在函数的外部**</u>。举例如下：

```js
function setName(obj) {
  obj.name = "Nicholas";
  obj = new Object();
  obj.name = "Greg";
  return obj;
}

var person1 = new Object();
var person2 = setName(person1);

alert(person1.name); //"Nicholas"
alert(person2.name); //"Greg"
```

> 可以把 ECMAScript 函数的参数想象成局部变量。

<br>

***2. 检测类型***

- 基本类型检测：typeof 操作符；
- 引用类型检测：instanceof 操作符；

```js
alert(person instanceof Object);    // 变量 person 是 Object 吗？
alert(colors instanceof Array);     // 变量 colors 是 Array 吗？
alert(pattern instanceof RegExp);   // 变量 pattern 是 RegExp 吗？
```

instanceof 操作符的返回值：`true` 和 `false` ；在检测一个引用类型值和 Object 构造函数时，instanceof 操作符始终会返回 true。如果使用 instanceof 操作符检测基本类型的值，则该操作符始终会返回 false。

<br>

### 二、执行环境及作用域

<br>

参考学习：[理解 JavaScript 作用域和作用域链](http://www.cnblogs.com/lhb25/archive/2011/09/06/javascript-scope-chain.html)

<br>

**<u><font color="red">每个执行环境都有一个与之关联的“变量对象”（variable object），环境中定义的所有变量和函数都保存在这个对象中</font></u>**。全局执行环境是最外围的一个执行环境。

在 Web 浏览器中，全局执行环境被认为是 `window` 对象，因此所有全局变量和函数都是作为 `window` 对象的属性和方法创建的。某个执行环境中的所有代码执行完毕后，该环境被销毁，保存在其中的所有变量和函数定义也随之销毁。

<br>

***1. 作用域链***

当代码在一个环境中执行时，会创建变量对象的一个 **作用域链**（scope chain）。

- **作用域链的用途**：**<u><font color="#282828">保证对执行环境有权访问的所有变量和函数的有序访问</font></u>**。内部环境可以通过作用域链访问所有的外部环境，但外部环境不能访问内部环境中的任何变量和函数。

函数参数也被当作变量来对待，因此其访问规则与执行环境中的其他变量相同。

<br>

***2. 作用域链的延长***

当执行流进入下列任何一个语句时，作用域链就会得到加长：

- try-catch 语句的 catch 块；
- with 语句；

这两个语句都会在作用域链的前端添加一个变量对象。对 `with` 语句来说，会将指定的对象添加到作用域链中。对 `catch` 语句来说，会创建一个新的变量对象，其中包含的是被抛出的错误对象的声明。

<br>

***3. 没有块级作用域***

在其他类 C 的语言中，由花括号封闭的代码块都有自己的作用域，JavaScript 没有块级作用域，举例如下：

```js
// 例一：if语句中定义的变量color，在if语句执行完后不会被销毁
if (true) {
  var color = "blue";
}
alert(color);   //"blue"
```

```js
// 例二：for语句中定义的变量i，在for语句执行完后不会被销毁
for (var i=0; i < 10; i++){
  doSomething(i);
}
alert(i);       //10
```

对于有块级作用域的语言来说，`for` 语句初始化变量的表达式所定义的变量，只会存在于循环的环境之中。而对于 JavaScript 来说，由 `for` 语句创建的变量 i 即使在 `for` 循环执行结束后，也依旧会存在于循环外部的执行环境中。

<br>

- **声明变量：**

使用 `var` 声明的变量会自动被添加到最接近的环境中。如果初始化变量时没有使用 `var` 声明，该变量会自动被添加到全局环境。

> 在编写 JavaScript 代码的过程中，不声明而直接初始化变量是一个常见的错误做 法，因为这样可能会导致意外。

<br>

***4. 垃圾收集***

JavaScript 具有自动垃圾收集机制，执行环境会负责管理代码执行过程中使用的内存。

**原理**：找出那些不再继续使用的变量，然后释放其占用的内存。垃圾收集器会按照固定的时间间隔（或代码执行中预定的收集时间），周期性地执行这一操作。

<br>

- **标记清除：**

JavaScript 中最常用的垃圾收集方式是 **标记清除**（mark-and-sweep）。当变量进入环境（例如，在函数中声明一个变量）时，就将这个变量标记为“进入环境”，而当变量离开环境时，则将其标记为“离开环境”。

<br>

- **引用计数：**

引用计数的含义是跟踪记录每个值被引用的次数，当代码中存在循环引用现象时，“引用计数”算法就会导致问题。这是一种不太常见的垃圾收集策略，JavaScript 引擎目前都不再使用这种算法。

<br>

- **性能问题：**

垃圾收集器是周期性运行的，如果为变量分配的内存数量很可观，那么回收工作量也是相当大。在这种情况下，确定垃圾收集的时间间隔是一个非常重要的问题。

<br>

- **管理内存：**

通常来说分配给 Web 浏览器的可用内存数量通常要比分配给桌面应用程序的少。这样做的目的主要是出于安全方面的考虑，目的是防止运行 JavaScript 的网页耗尽全部系统内存而导致系统崩溃。

**解除引用**（dereferencing）：为确保占用最少的内存获得更好的性能，最佳方式就是为执行中的代码只保存必要的数据，一旦数据不再有用，最好通过将其值设置为 `null` 来释放其引用。这一做法适用于大多数全局变量和全局对象的属性。

这一做法称为解除引用，举例如下

```js
function createPerson(name){
  var localPerson = new Object();
  localPerson.name = name;
  return localPerson;
}
var globalPerson = createPerson("Nicholas");

// 手工解除 globalPerson 的引用
globalPerson = null;
```

解除一个值的引用并不意味着自动回收该值所占用的内存。**<u><font color="#282828">解除引用的真正作用是让值脱离执行环境，以便垃圾收集器下次运行时将其回收</font></u>**。

<br>
<br>
<br>
<br>
<br>

## 第五章 引用类型

引用类型的值（对象）是引用类型的一个实例。**<u><font color="red">在 ECMAScript 中，引用类型是一种数据结构，用于将数据和功能组织在一起</font></u>**。

<br>

### 一、Object 类型

Object 也是 `ECMAScript` 中使用最多的一个类型。Object 是一个基础类型，其他所有类型都从 Object 继承了基本的行为。

创建 Object 实例的方法有两种：

- 使用 new 操作符后跟 Object 构造函数;
- 使用 **对象字面量** 表示法；

对象字面量是对象定义的一种简写形式，目的在于简化创建包含大量属性的对象的过程。举例如下：

```js
var person = {
  "name" : "Nicholas",
  "age" : 29,
  5 : true
};
```

<br>

### 二、Array 类型

Array 类型是一组值的有序列表，同时还提供了操作和转换这些值的功能。`ECMAScript` 中的数组与其他多数语言中的数组有着相当大的区别。

```
  ECMAScript 数组的每一项可以保存任何类型的数据。 也就是说，可以用数组的第一个位置来保存字符串，用第二位置来保存数值，用第三个位置来保存对象， 以此类推。
  ECMAScript 数组的大小是可以动态调整的，即可以随着数据的添加自动增长以容纳新增数据。
```

创建 Array 数组的基本方式有两种：

- 是使用 Array 构造函数（ var colors = new Array(); )；
- 是使用数组字面量表示法（ var colors = ["red", "blue", "green"]; ）；

<br>

***1. 检测数组***

自从 `ECMAScript 3` 做出规定以后，就出现了确定某个对象是不是数组的经典问题。

- instanceof 操作符（适用于全局执行环境）；
- `Array.isArray()` 方法，目的是最终确定某个值到底是不是数组，而不管它是在哪个全局执行环境中创建的；

<br>

### 三、Date 类型

`ECMAScript` 中的 `Date` 类型是在早期 Java 中的 java.util.Date 类基础上构建的。为此，`Date` 类型使用自 UTC（Coordinated Universal Time，国际协调时间）1970 年 1 月 1 日午夜（零时）开始经过的毫秒数来保存日期。

`Date` 类型提供了有关日期和时间的信息，包括当前日期和时间以及相关的计算功能。

<br>

### 四、RegExp 类型

`ECMAScript` 通过 `RegExp` 类型来支持正则表达式。RegExp 类型是 ECMAScript 支持正则表达式的一个接口，提供了最基本的和一些高级的正则表达式功能。

创建 RegExp 类型的两种方式：

```js
/*
 *  1、以字面量形式来定义的正则表达式
 */
var pattern1 = /[bc]at/i;

/*
 *  2、使用构造函数创建的正则表达式
 */
var pattern2 = new RegExp("[bc]at", "i");
```

<br>

### 五、Function 类型

`ECMAScript` 中函数实际上是对象。每个函数都是 `Function` 类型的实例，而且都与其他引用类型一样具有属性和方法。

由于函数是对象，因此函数名实际上也是一个指向函数对象的指针，不会与某个函数绑定。

<br>

***1. 函数声明与函数表达式***

解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁。

解析器会率先读取函数声明，并使其在执行任何代码之前可用（可以访问）；至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行。请看下面的例子：

```js
/*
 *  1、函数声明语法：正常运行
 */
 alert(sum(10,10));
 function sum(num1, num2){
    return num1 + num2;
  }

/*
 *  2、函数表达式：运行报错
 */
alert(sum(10,10));
var sum = function(num1, num2){
   return num1 + num2;
 };
```

<br>

***2. 作为值的函数***

因为 `ECMAScript` 中的函数名本身就是变量，所以函数也可以作为值来使用。也就是说，不仅可以像传递参数一样把一个函数传递给另一个函数，而且可以将一个函数作为另一个函数的结果返回。

<br>

 ***3. 函数内部属性***

函数内部，有两个特殊的对象：`arguments` 和 `this`。

<br>

 ***4. 函数属性和方法***

`ECMAScript` 中的函数是对象，因此函数也有属性和方法。

<br>

### 六、基本包装类型

三种基本包装类 型分别是：Boolean、Number 和 String。以下是它们共同的特征：

```
  每个包装类型都映射到同名的基本类型；
  在读取模式下访问基本类型值时，就会创建对应的基本包装类型的一个对象，从而方便了数据 操作；
  操作基本类型值的语句一经执行完毕，就会立即销毁新创建的包装对象。
```

<br>
<br>
<br>
<br>
<br>

## 第六章 面向对象的程序设计

面向对象（Object-Oriented，OO）的语言有一个标志，那就是它们都有类的概念，而通过类可以创建任意多个具有相同属性和方法的对象。`ECMAScript` 中没有类的概念，因此它的对象也与基于类的语言中的对象有所不同。

每个对象都是基于一个引用类型创建的，这个引用类型可以是第 5 章讨论的原生类型，也可以是开发人员定义的类型。

<br>


### 一、理解对象

<br>

***1. 属性类型***

ECMA-262 第 5 版在定义只有内部才用的特性（attribute）时，描述了属性（property）的各种特征。 ECMA-262 定义这些特性是为了实现 JavaScript 引擎用的，因此在 JavaScript 中不能直接访问它们。

`ECMAScript` 中有两种属性：**数据属性** 和 **访问器属性** 。

<br>

- **数据属性:**

数据属性包含一个数据值的位置，在这个位置可以读取和写入值。数据属性有 4 个描述其行为的特性：

```
  [[Configurable]]：表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性；
  [[Enumerable]]：表示能否通过 for-in 循环返回属性；
  [[Writable]]：表示能否修改属性的值；
  [[Value]]：包含这个属性的数据值；
```

<br>

- **访问器属性:**

访问器属性不包含数据值。它们包含一对儿 getter 和 setter 函数（不过，这两个函数都不是必需的）。有如下 4 个特性：

```
 [[Configurable]]：表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特性， 或者能否把属性修改为数据属性。对于直接在对象上定义的属性，这个特性的默认值为 true。
 [[Enumerable]]：表示能否通过 for-in 循环返回属性。对于直接在对象上定义的属性，这个特性的默认值为 true。
 [[Get]]：在读取属性时调用的函数。默认值为 undefined。
 [[Set]]：在写入属性时调用的函数。默认值为 undefined。
```

<br>

### 二、创建对象

虽然 Object 构造函数或对象字面量都可以用来创建单个对象，但这些方式有个明显的缺点：**使用同一个接口创建很多对象，会产生大量的重复代码**。为解决这个问题，人们开始使用工厂模式的一种变体。

<br>

***1. 工厂模式***

工厂模式是软件工程领域一种广为人知的设计模式，这种模式抽象了创建具体对象的过程.考虑到在 ECMAScript 中无法创建类，开发人员就发明了一种函数，用函数来封装以特定接口创建对象的细节，如下面的例子所示:

```js
function createPerson(name, age, job){
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function(){
	  alert(this.name);
  };
  return o;
}

var person1 = createPerson("Nicholas", 29, "Software Engineer");
var person2 = createPerson("Greg", 27, "Doctor");
```

工厂模式虽然解决了创建多个相似对象的问题，但却没有解决对象识别的问题（即怎样知道一个对象的类型）。随着 JavaScript 的发展，又一个新模式出现了。

<br>

***2. 构造函数模式***

<br>

- **构造函数:**

可以创建自定义的构造函数，从而定义自定义对象类型的属性和方法。例如，可以使用构造函数模式将前面的例子重写如下:

```js
function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function(){
    alert(this.name);
  };
}

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
```

这个例子中，Person()函数取代了createPerson()函数。他们存在以下不同之处：

	- 没有显式地创建对象；

	- 直接将属性和方法赋给了 this 对象；

	- 没有 return 语句；

	- 函数名 Person 使用的是大写字母 P（主要是为了 区别于 ECMAScript 中的其他函数；因为构造函数本身也是函数，只不过可以用来创建对象而已）；

<br>

要创建 Person 的新实例，必须使用 new 操作符。以这种方式调用构造函数实际上会经历以下 4 个步骤：

	- (1) 创建一个新对象；

	- (2) 将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）；

	- (3) 执行构造函数中的代码（为这个新对象添加属性）；

	- (4) 返回新对象；

**<u><font color="red">创建自定义的构造函数意味着将来可以将它的实例标识为一种特定的类型；而这正是构造函数模式胜过工厂模式的地方</font></u>**。

<br>

- **构造函数也是函数:**

构造函数与其他函数的唯一区别，就在于调用它们的方式不同。

**<u><font color="#282828">任何函数，只要通过 new 操作符来调用，那它就可以作为构造函数；而任何函数，如果不通过 new 操作符来调用，那它跟普通函数也不会有什么两样。</font></u>**

<br>

- **构造函数的问题:**

使用构造函数的主要问题，就是每个方法都要在每个实例上重新创建一遍。

<br>

***3. 原型模式***

我们创建的每个函数都有一个 prototype（原型）属性，这个属性是一个指针，指向一个对象， 而这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。

使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法。换句话说，不必在构造函数中定义对象实例的信息，而是可以将这些信息直接添加到原型对象中，如下面的例子所示：

```js
function Person(){}

Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
  alert(this.name);
};

var person1 = new Person();
person1.sayName();   //"Nicholas"

var person2 = new Person();
person2.sayName();   //"Nicholas"
alert(person1.sayName == person2.sayName);  //true
```

**与构造函数模式不同的是，新对象的这些属性和方法是由所有实例共享的**。

<br>

***4. 组合使用构造函数模式和原型模式***

创建自定义类型的最常见方式，就是组合使用构造函数模式与原型模式。构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。它有两个好处:

	- 每个实例都会有自己的一份实例属性的副本， 但同时又共享着对方法的引用，最大限度地节省了内存;

	- 这种混成模式还支持向构造函数传递参数;

举例如下：

```js
function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.friends = ["Shelby", "Court"];
}

Person.prototype = {
  constructor : Person,
  sayName : function(){
    alert(this.name);
  }
}

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");

person1.friends.push("Van");

alert(person1.friends); //"Shelby,Count,Van"
alert(person2.friends); //"Shelby,Count"
alert(person1.friends === person2.friends); //false
alert(person1.sayName === person2.sayName); //true
```

这种构造函数与原型混成的模式，是目前在 ECMAScript 中使用最广泛、认同度最高的一种创建自定义类型的方法。可以说，这是用来定义引用类型的一种默认模式。

<br>

***5. 动态原型模式***

动态原型模式把所有信息都封装在了构造函数中，通过在构造函数中初始化原型（仅在必要的情况下），又保持了同时使用构造函数和原型的优点

<br>
<br>

### 三、继承

继承是 `OO` 语言中的一个最为人津津乐道的概念。许多 `OO` 语言都支持两种继承方式：<strong>接口继承</strong> 和 <strong>实现继承</strong>。如前所述，由于函数没有签名，所以无法实现接口继承。ECMAScript 只支持实现继承，而且其实现继承主要是依靠原型链来实现的。

<br>

***1. 原型链***

基本思想是利用原型让一个引用类型继承另一个引用类型的属性和方法。本质是重写原型对象，代之以一个新类型的实例。

- **原型链的问题：**

	- 问题一：在通过原型来实现继承时，原型实际上会变成另一个类型的实例。于是，原先的实例属性也就顺理成章地变成了现在的原型属性了。

	- 问题二：应该没有办法在不影响所有对象实例的情况下，给超类型的构造函数传递参数。

<br>

***2. 借用构造函数（伪造对象或经典继承）***

在子类型构造函数的内部调用超类型构造函数。如下所示：

```js
function SuperType(name){
	this.name = name;
}

function SubType(){
//继承了 SuperType，同时还传递了参数
  SuperType.call(this, "Nicholas");

//实例属性
  this.age = 29;
}

var instance = new SubType();
alert(instance.name);    //"Nicholas";
alert(instance.age);     //29
```

相对于原型链而言，借用构造函数有一个很大的优势，即可以在子类型构造函数中向超类型构造函数传递参数。

<br>

- **借用构造函数的问题:**

	- 方法都在构造函数中定义，因此函数复用就无从谈起了。

	- 在超类型的原型中定义的方法，对子类型而言也是不可见的，结 果所有类型都只能使用构造函数模式。

<br>

***3. 组合继承(伪经典继承)***

将原型链和借用构造函数的技术组合到一块，从而发挥二者之长的一种继承模式。背后的思路是使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承。举例如下：

```js
function SuperType(name){
  this.name = name;
  this.colors = ["red", "blue", "green"];
}

SuperType.prototype.sayName = function(){
  alert(this.name);
};

function SubType(name, age){
  //继承属性
  SuperType.call(this, name);

  this.age = age;
}

//继承方法
SubType.prototype = new SuperType(); SubType.prototype.constructor = SubType;
SubType.prototype.sayAge = function(){
  alert(this.age);
};

var instance1 = new SubType("Nicholas", 29); instance1.colors.push("black");
alert(instance1.colors);        //"red,blue,green,black"
instance1.sayName();            //"Nicholas";
instance1.sayAge();             //29

var instance2 = new SubType("Greg", 27);
alert(instance2.colors);       //"red,blue,green"
instance2.sayName();           //"Greg";
instance2.sayAge();            //27
```

**<u><font color="red">组合继承避免了原型链和借用构造函数的缺陷，融合了它们的优点，成为 JavaScript 中最常用的继承模式</font></u>** 。而且，instanceof 和 isPrototypeOf()也能够用于识别基于组合继承创建的对象。

<br>

***4. 原型式继承***

ECMAScript5 通过新增 Object.create()方法规范化了原型式继承。这个方法接收两个参数：一个用作新对象原型的对象和（可选的）一个为新对象定义额外属性的对象。

```js
var person = {
  name: "Nicholas",
  friends: ["Shelby", "Court", "Van"]
};

// 在传入一个参数的情况下，Object.create() 与 object()方法的行为相同。
var anotherPerson = Object.create(person);
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");

var yetAnotherPerson = Object.create(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");

alert(person.friends);     //"Shelby,Court,Van,Rob,Barbie"

// 以这种方式指定的任何属性都会覆盖原型对象上的同名属性。
var finalPerson = Object.create(person, {
  name: { value: "Greg" }
});

alert(finalPerson.name);  //"Greg"
```

在没有必要兴师动众地创建构造函数，而只想让一个对象与另一个对象保持类似的情况下，原型式继承是完全可以胜任的。不过别忘了，包含引用类型值的属性始终都会共享相应的值，就像使用原型模式一样。

<br>

***5. 寄生式继承***

寄生式继承的思路与寄生构造函数和工厂模式类似，即创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后再像真地是它做了所有工作一样返回对象。举例如下：

```js
function createAnother(original){
  var clone = object(original);    // 通过调用函数创建一个新对象
  clone.sayHi = function(){        // 以某种方式来增强这个对象
    alert("hi");
  };
  return clone;                    // 返回这个对象
}

var person = {
  name: "Nicholas",
  friends: ["Shelby", "Court", "Van"]
};

var anotherPerson = createAnother(person);
anotherPerson.sayHi();             //"hi"
```

在主要考虑对象而不是自定义类型和构造函数的情况下，寄生式继承也是一种有用的模式。**使用寄生式继承来为对象添加函数，会由于不能做到函数复用而降低效率；这一点与构造函数模式类似**。

<br>

***6. 寄生组合式继承***

所谓寄生组合式继承，即通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。本质上，就是 **<u><font color="red">使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型的原型</font></u>** 。

```js
function inheritPrototype(subType, superType){
  var prototype = object(superType.prototype);  //创建对象
  prototype.constructor = subType;              //增强对象
  subType.prototype = prototype;                //指定对象
}

function SuperType(name){
  this.name = name;
  this.colors = ["red", "blue", "green"];
}

SuperType.prototype.sayName = function(){
  alert(this.name);
};

function SubType(name, age){
  SuperType.call(this, name);
  this.age = age;
}

inheritPrototype(SubType, SuperType);

SubType.prototype.sayAge = function(){
  alert(this.age);
};
```

<br>
<br>
<br>
<br>
<br>

## 第七章 函数表达式

在 JavaScript 编程中，函数表达式是一种非常有用的技术。使用函数表达式可以无须对函数命名，从而实现动态编程。

<br>

**函数表达式的特点：**

- 函数表达式不同于函数声明。函数声明要求有名字，但函数表达式不需要。没有名字的函数表达式也叫做匿名函数；

- 在无法确定如何引用函数的情况下，递归函数就会变得比较复杂;

- 递归函数应该始终使用 arguments.callee 来递归地调用自身，不要使用函数名——函数名可能会发生变化；

<br>

### 一、递归

递归函数是在一个函数通过名字调用自身的情况下构成的，如下所示：

```js
function factorial(num){
  if (num <= 1){ return 1; }
  else {
    return num * factorial(num-1);
  }
}
```

这是一个经典的递归阶乘函数。虽然这个函数表面看来没什么问题，但下面的代码却可能导致它出错:

```js
var anotherFactorial = factorial;
factorial = null;
alert(anotherFactorial(4));     //出错！
```

调用 anotherFactorial()时，由于必须执行 factorial()，而 factorial 已经不再是函数，所以就会导致错误。在这种情况下，使用 `argu-ments.callee` 可以解决这个问题。**<u><font color="red">arguments.callee 是一个指向正在执行的函数的指针</font></u>**

```js
function factorial(num){
  if (num <= 1){ return 1; }
  else {
    return num * arguments.callee(num-1);
  }
}
```

<br>

### 二、闭包

**<u><font color="#282828">闭包是指有权访问另一个函数作用域中的变量的函数</font></u>** 。创建闭包的常见方式，就是在一个函数内部创建另一个函数，如下：

```js
function createComparisonFunction(propertyName) {
  return function(object1, object2){
    var value1 = object1[propertyName];
    var value2 = object2[propertyName];

    if (value1 < value2){
      return -1;
    } else if (value1 > value2){
      return 1;
    } else {
      return 0;
    }
  };
}
```

<br>

***1. 闭包与变量***

**<u><font color="#282828">闭包只能取得包含函数中任何变量的最后一个值。别忘了闭包所保存的是整个变量对象，而不是某个特殊的变量</font></u>**。

```js
function createFunctions(){
  var result = new Array();
  for (var i=0; i < 10; i++){
    result[i] = function(){ return i; };
  }
  return result;
}
```

表面上看，似乎每个函数都应该返自己的索引值。但实际上，每个函数都返回10。因为每个函数的作用域链中都保存着createFunctions()函数的活动对象，所以它们引用的都是同一个变量i。当createFunctions()函数返回后，变量i的值是10，此时每个函数都引用着保存变量i的同一个变量对象，所以在每个函数内部i的值都是10。我们可以通过创建另一个匿名函数强制让闭包的行为符合预期，如下所示:

```js
function createFunctions(){
  var result = new Array();
  for (var i=0; i < 10; i++){
    result[i] = function(num){
      return function(){
        return num;
      };
    }(i);
  }
  return result;
}
```

<br>

***2. 关于 this 对象***

匿名函数的执行环境具有全局性，因此其 this 对象通常指向 window 。但有时候由于编写闭包的方式不同，这一点可能不会那么明显。如下图所示：

```js
var name = "The Window";
var object = {
  name : "My Object",
  getNameFunc : function(){
    var that = this;
    return function(){ return that.name; };
  }
};
alert(object.getNameFunc()());   //"My Object"
```

在定义匿名函数之前，我们把 this 对象赋值给了一个名叫 that 的变量。而在定义了闭包之后，闭包也可以访问这个变量，因为它是我们在包含函数中特意声名的一个变量。 即使在函数返回之后，that 也仍然引用着 object.

**<u><font color="#282828">this 和 arguments 也存在同样的问题。如果想访问作用域中的 arguments 对象，必须将对该对象的引用保存到另一个闭包能够访问的变量中</font></u>**。

<br>

### 三、模仿块级作用域

JavaScript没有块级作用域的概念。这意味着在块语句中定义的变量，实际上是在包含 函数中而非语句中创建的。

JavaScript从来不会告诉你是否多次声明了同一个变量；遇到这种情况，它只会对后续的声明视而不见（不过，它会执行后续声明中的变量初始化）。匿名函数可以用来模仿块级作用域并避免这个问题。语法如下所示：

```js
(function(){
  //这里是块级作用域
})();
```

将函数声明包含在一对圆括号中，表示它实际上是一个函数表达式。而紧随其后的另一对圆括号会立即调用这个函数。

这种做法可以减少闭包占用的内存问题，因为没有指向匿名函数的引用。只要函数执行完毕，就可以立即销毁其作用域链了。

<br>

### 四、私有变量

严格来讲，JavaScript 中没有私有成员的概念；所有对象属性都是公有的。不过有一个私有变量的概念。任何在函数中定义的变量，都可以认为是私有变量，因为不能在函数的外部访问这些变量。

**如果在一个函数内部创建一个闭包，那么闭包通过自己的作用域链可以在函数外部访问函数内部变量**。利用这一点，我们可以创建用于访问私有变量的公有方法：

<br>

***1. 特权方法***

**<u><font color="red">有权访问私有变量和私有函数的公有方法</font></u>**。

- 在构造函数中定义特权方法：

```js
function MyObject(){
  //私有变量和私有函数
  var privateVariable = 10;
  function privateFunction(){ return false; }

  //特权方法
  this.publicMethod = function (){
    privateVariable++;
    return privateFunction();
  };
}
```

在构造函数中定义特权方法也有一个缺点，那就是你必须使用构造函数模式来达到这个目的。构造函数模式的缺点是针对每个实例都会创建同样一组新方法，而使用静态私有变量来实现特权方法就可以避免这个问题。

<br>

- 在私有作用域中定义私有变量或函数：

```js
(function(){
  // 私有变量和私有函数
  var privateVariable = 10;
  function privateFunction(){ return false; }
  // 构造函数
  MyObject = function(){ };
  // 公有/特权方法
  MyObject.prototype.publicMethod = function(){
    privateVariable++;
    return privateFunction();
  };
})();
```

这个模式在定义构造函数时并没有使用函数声明，而是使用了函数表达式。函数声明只能创建局部函数,出于同样的原因，也没有在声明 MyObject 时使用 var 关键字。记住：初始化未经声明的变量，总是会创建一个全局变量。因此，MyObject就成了一个全局变量，能够在私有作用域之外被访问到。

这个模式与在构造函数中定义特权方法的主要区别:**私有变量和函数是由实例共享的，由于特权方法是在原型上定义的，因此所有实例都使用同一个函数**。而这个特权方法，作为一个闭包，总是保存着对包含作用域的引用。

以这种方式创建静态私有变量会因为使用原型而增进代码复用，但每个实例都没有自己的私有变量。到底是使用实例变量，还是静态私有变量，最终还是要视你的具体需求而定。

<br>

***2. 模块模式***

前面的模式是用于为自定义类型创建私有变量和特权方法的。而模块模式（module pattern）则是为单例创建私有变量和特权方法。**<u><font color="#282828">所谓单例（singleton），指的就是只有一个实例的对象</font></u>**。

JavaScript 是以对象字面量的方式来创建单例对象的，如下：

```js
var singleton = {
  name : value,
  method : function () {
    // 这里是方法的代码
  }
};
```

模块模式通过为单例添加私有变量和特权方法能够使其得到增强，其语法形式如下：

```js
var singleton = function(){
  // 私有变量和私有函数
  var privateVariable = 10;
  function privateFunction(){ return false; }

  // 特权/公有方法和属性
  return {
    publicProperty: true,
    publicMethod : function(){
      privateVariable++;
      return privateFunction();
    }
  };
}();
```

<br>
<br>
<br>
<br>
<br>

## 第八章 BOM

BOM：浏览器对象模型

BOM 提供了很多对象，用于访问浏览器的功能，这些功能与任何网页内容无关。

<br>

1. **window 对象**

	window 是 BOM 的核心对象，它表示浏览器的一个实例。在浏览器中，window 对象有双重角色，它既是通过 JavaScript 访问浏览器窗口的一个接口，又是 ECMAScript 规定的 Global 对象。

	<br>

2. **location 对象**

	navigator 对象提供了与浏览器有关的信息。到底提供哪些信息，很大程度上取决于用户的浏览器；不过，也有一些公共的属性（如 userAgent）存在于所有浏览器中。

	<br>

3. **navigator 对象**

	location 对象是很特别的一个对象，因为它既是 window 对象的属性，也是 document 对象的属性。它提供了与当前窗口中加载的文档有关的信息，还提供了一些导航功能。

	<br>

4. **screen 对象**

	screen 对象基本上只 用来表明客户端的能力，其中包括浏览器窗口外部的显示器的信息，如像素宽度和高度等。

	<br>

5. **history 对象**

	history 对象保存着用户上网的历史记录，从窗口被打开的那一刻算起。因为 history 是 window 对象的属性，因此每个浏览器窗口、每个标签页乃至每个框架，都有自己的 history 对象与特定的 window 对象关联。

<br>
<br>
<br>
<br>
<br>
