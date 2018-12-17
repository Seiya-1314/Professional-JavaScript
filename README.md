# 《JavaScript高级程序设计(第三版)》学习笔记

**作者简介：**

  Nicholas C. Zakas（尼古拉斯•泽卡斯）世界顶级Web技术专家，现为雅虎公司界面呈现架构师，负责My Yahoo!和雅虎首页等大访问量站点的设计。尼古拉斯拥有丰富的Web开发和界面设计经验，曾经参与许多世界级大公司的Web解决方案开发。他还是High Performance JavaScript一书的作者，并与他人合作撰写了Professional Ajax和Even Faster Web Sites。尼古拉斯拥有梅里马克学院计算机科学学士学位和埃迪柯特学院的MBA学位。他的个人网站是www.nczonline.net，他的Twitter别名是@slicknet。
<br>

**前言：**

记录自己在阅读本书过程中的收获以及思考。
<br>

## 第三章 基本概念

#### 一、语法

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

#### 二、变量

`ECMAScript` 的变量是松散类型的，可以用来保存任何类型的数据。

- 用 `var` 操作符定义的变量将成为定义该变量的作用域中的局部变量;

- 省略 `var` 操作符可以定义全局变量，但局部作用域中定义的全局变量很难维护;
<br>

#### 三、数据类型

`ECMAScript` 可以用 `typeof` 操作符来检测给定变量的数据类型。

**注意：**`typeof` 是一个操作符而不是函数，因此例子中的圆括号尽管可以使用，但不是必需的。比如：
```JavaScript
var message = "some string";
alert(typeof message);   // "string"
alert(typeof(message));  // "string"
alert(typeof 95);        // "number"
```

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

尽管 `null` 和 `undefined` 有这样的关系，但它们的用途完全不同。无论在什么情况下，都没有必要把一个变量的值显式地设置为 `undefined`，可是同样的规则对 `null` 却不适用。换句话说，只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存 `null` 值。这样做不仅可以体现 `null` 作为空对象指针的惯例，而且也有助于进一步区分 `null` 和 `undefined`。
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
