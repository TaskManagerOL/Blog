---
title: TypeScript
date: 2024-01-30 12:17:40
tags: [笔记,前端]
excerpt: Javascript进阶版👽
categories: 技术栈
---

# TypeScript

前言：很久之前就想着学Typescript了，但是一直在嘴上说没有时间学，说是没有但实际上学习这个也不会花费太久时间，只要肯挤时间并强制去完成就肯定可以完成。

[TypeScript 中文手册 ](https://typescript.bootcss.com/)

TS其实就是JS Plus，笔记中只写我觉得和JS不一样的很多的地方详细需要自己参考文档。

# TypeScript相比JS的优势

+ 更早(写代码的同时)发现错误，减少找Bug、改Bug时间，提升开发效率。
+ 程序中任何位置的代码都有代码提示，随时随地的安全感，增强了开发体验。
+ 强大的类型系统提升了代码的可维护性，使得重构代码更加容易。
+ 支持最新的ECMAScript语法，优先体验最新的语法，让你走在前端技术的最前沿。
+ TS类型推断机制，不需要在代码中的每个地方都显示标注类型，让你在享受优势的同时，尽量降低了成本。除此之外，Vue 3源码使用TS重写、Angular默认支持TS、React与TS完美配合，TypeScript已成为大中型前端项目的首先编程语言。

# 安装TypeScript

有两种主要的方式来获取TypeScript工具：

- 通过npm（Node.js包管理器）
- 安装Visual Studio的TypeScript插件

Visual Studio 2017和Visual Studio 2015 Update 3默认包含了TypeScript。 如果你的Visual Studio还没有安装TypeScript，你可以[下载](https://typescript.bootcss.com/index.html#download-links)它。

针对使用npm的用户：

```
npm install -g typescript
```

# TS中的高级功能

## 类型注解

TypeScript里的类型注解是一种轻量级的为函数或变量添加约束的方式。 在这个例子里，我们希望`greeter`函数接收一个字符串参数。 然后尝试把`greeter`的调用改成传入一个数组：

```typescript
function greeter(person: string) {
    return "Hello, " + person;
}

let user = [0, 1, 2]; 

document.body.innerHTML = greeter(user);
```

重新编译，你会看到产生了一个错误。

```
error TS2345: Argument of type 'number[]' is not assignable to parameter of type 'string'.
```

类似地，尝试删除`greeter`调用的所有参数。 TypeScript会告诉你使用了非期望个数的参数调用了这个函数。 在这两种情况中，TypeScript提供了静态的代码分析，它可以分析代码结构和提供的类型注解。

**要注意的是尽管有错误，`greeter.js`文件还是被创建了。 就算你的代码里有错误，你仍然可以使用TypeScript。但在这种情况下，TypeScript会警告你代码可能不会按预期执行。**

## 接口

让我们开发这个示例应用。这里我们使用接口来描述一个拥有`firstName`和`lastName`字段的对象。 在TypeScript里，只在两个类型内部的结构兼容那么这两个类型就是兼容的。 这就允许我们在实现接口时候只要保证包含了接口要求的结构就可以，而不必明确地使用`implements`语句。

```typescript
interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person: Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = { firstName: "Jane", lastName: "User" };

document.body.innerHTML = greeter(user);
```

因为我对type对象不是很了解（看完这些文章之后感觉到tasklist有些语句需要规范化了orz），这里也补充一下type&interface的知识：

类型别名 type 和 接口 interface 区别与联系

+ 不同点：

  + 类型别名type用来给一个类型起个新名字，接口interface是命名数据结构（例如对象）的另一种方式

  + type可以用来表示基本类型、对象类型、联合类型、元组和交集；interface仅限于描述对象类型

  + interface 定义重名了会合并属性，type 会报错

  + interface 可以 extends， type 是不允许 extends ，但是 type 缺可以通过交叉类型 实现 interface 的 extend 行为，并且两者并不是相互独立的，也就是说 interface 可以 extends type, type 也可以 与 interface 类型 交叉

+ 相同点：

  + 都可以描述 Object和Function

  + interface 和 type 都可以继承。

## 类

最后，让我们使用类来改写这个例子。 TypeScript支持JavaScript的新特性，比如支持基于类的面向对象编程。

让我们创建一个`Student`类，它带有一个构造函数和一些公共字段。 注意类和接口可以一起共作，程序员可以自行决定抽象的级别。

还要注意的是，在构造函数的参数上使用`public`等同于创建了同名的成员变量。

```typescript
class Student {
    fullName: string;
    constructor(public firstName: string, public middleInitial: string, public lastName: string) {
        this.fullName = firstName + " " + middleInitial + " " + lastName;
    }
}

interface Person {
    firstName: string;
    lastName: string;
}

function greeter(person : Person) {
    return "Hello, " + person.firstName + " " + person.lastName;
}

let user = new Student("Jane", "M.", "User");

document.body.innerHTML = greeter(user);
```

# 基础类型

## 枚举

`enum`类型是对JavaScript标准数据类型的一个补充。 像C#等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。

```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

默认情况下，从`0`开始为元素编号。 你也可以手动的指定成员的数值。 例如，我们将上面的例子改成从`1`开始编号：

```typescript
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green;
```

或者，全部都采用手动赋值：

```typescript
enum Color {Red = 1, Green = 2, Blue = 4}
let c: Color = Color.Green;
```

枚举类型提供的一个便利是你可以由枚举的值得到它的名字。 例如，我们知道数值为2，但是不确定它映射到Color里的哪个名字，我们可以查找相应的名字：

```typescript
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

alert(colorName);  // 显示'Green'因为上面代码里它的值是2
```

## 任意值

有时候，我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。 那么我们可以使用`any`类型来标记这些变量

```typescript
let list: any[] = [1, true, "free"];
```

## Never

`never`类型表示的是那些永不存在的值的类型。 例如，`never`类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型； 变量也可能是`never`类型，当它们被永不为真的类型保护所约束时。

`never`类型是任何类型的子类型，也可以赋值给任何类型；然而，*没有*类型是`never`的子类型或可以赋值给`never`类型（除了`never`本身之外）。 即使`any`也不可以赋值给`never`。

下面是一些返回`never`类型的函数：

```typescript
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
    throw new Error(message);
}

// 推断的返回值类型为never
function fail() {
    return error("Something failed");
}

// 返回never的函数必须存在无法达到的终点
function infiniteLoop(): never {
    while (true) {
    }
}
```

## 类型断言

有时候你会遇到这样的情况，你会比TypeScript更了解某个值的详细信息。 通常这会发生在你清楚地知道一个实体具有比它现有类型更确切的类型。

通过*类型断言*这种方式可以告诉编译器，“相信我，我知道自己在干什么”。 类型断言好比其它语言里的类型转换，但是不进行特殊的数据检查和解构。 它没有运行时的影响，只是在编译阶段起作用。 TypeScript会假设你，程序员，已经进行了必须的检查。

类型断言有两种形式。 其一是“尖括号”语法：

```typescript
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

另一个为`as`语法：

```typescript
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```

两种形式是等价的。 至于使用哪个大多数情况下是凭个人喜好；然而，当你在TypeScript里使用JSX时，只有`as`语法断言是被允许的。

# 变量声明

`let`和`const`是JavaScript里相对较新的变量声明方式。 像我们之前提到过的，`let`在很多方面与`var`是相似的，但是可以帮助大家避免在JavaScript里常见一些问题。 `const`是对`let`的一个增强，它能阻止对一个变量再次赋值。

因为TypeScript是JavaScript的超集，所以它本身就支持`let`和`const`。 下面我们会详细说明这些新的声明方式以及为什么推荐使用它们来代替`var`。

## 作用域规则

对于熟悉其它语言的人来说，`var`声明有些奇怪的作用域规则。 看下面的例子：

```typescript
function f(shouldInitialize: boolean) {
    if (shouldInitialize) {
        var x = 10;
    }

    return x;
}

f(true);  // returns '10'
f(false); // returns 'undefined'
```

有些读者可能要多看几遍这个例子。 变量`x`是定义在*`if`语句里面*，但是我们却可以在语句的外面访问它。 这是因为`var`声明可以在包含它的函数，模块，命名空间或全局作用域内部任何位置被访问（我们后面会详细介绍），包含它的代码块对此没有什么影响。 有些人称此为*`var`作用域*或*函数作用域*。 函数参数也使用函数作用域。

## 变量获取怪异之处

快速的猜一下下面的代码会返回什么：

```typescript
for (var i = 0; i < 10; i++) {
    setTimeout(function() { console.log(i); }, 100 * i);
}
```

介绍一下，`setTimeout`会在若干毫秒的延时后执行一个函数（等待其它代码执行完毕）。

好吧，看一下结果：

```typescript
10
10
10
10
10
10
10
10
10
10
```

很多JavaScript程序员对这种行为已经很熟悉了，但如果你很不解，你并不是一个人。 大多数人期望输出结果是这样：

```typescript
0
1
2
3
4
5
6
7
8
9
```

还记得我们上面讲的变量获取吗？

> 每当`g`被调用时，它都可以访问到`f`里的`a`变量。

让我们花点时间考虑在这个上下文里的情况。 `setTimeout`在若干毫秒后执行一个函数，并且是在`for`循环结束后。 `for`循环结束后，`i`的值为`10`。 所以当函数被调用的时候，它会打印出`10`！

一个通常的解决方法是使用立即执行的函数表达式（IIFE）来捕获每次迭代时`i`的值：

```typescript
for (var i = 0; i < 10; i++) {
    // capture the current state of 'i'
    // by invoking a function with its current value
    (function(i) {
        setTimeout(function() { console.log(i); }, 100 * i);
    })(i);
}
```

这种奇怪的形式我们已经司空见惯了。 参数`i`会覆盖`for`循环里的`i`，但是因为我们起了同样的名字，所以我们不用怎么改`for`循环体里的代码。

## let声明

### 块作用域

当用`let`声明一个变量，它使用的是*词法作用域*或*块作用域*。 不同于使用`var`声明的变量那样可以在包含它们的函数外访问，块作用域变量在包含它们的块或`for`循环之外是不能访问的。

### 重定义及屏蔽

我们提过使用`var`声明时，它不在乎你声明多少次；你只会得到1个。

```typescript
function f(x) {
    var x;
    var x;

    if (true) {
        var x;
    }
}
```

在上面的例子里，所有`x`的声明实际上都引用一个*相同*的`x`，并且这是完全有效的代码。 这经常会成为bug的来源。 好的是，`let`声明就不会这么宽松了。

```typescript
let x = 10;
let x = 20; // 错误，不能在1个作用域里多次声明`x`
```

并不是要求两个均是块级作用域的声明TypeScript才会给出一个错误的警告。

```typescript
function f(x) {
    let x = 100; // error: interferes with parameter declaration
}

function g() {
    let x = 100;
    var x = 100; // error: can't have both declarations of 'x'
}
```

并不是说块级作用域变量不能用函数作用域变量来声明。 而是块级作用域变量需要在明显不同的块里声明。

```typescript
function f(condition, x) {
    if (condition) {
        let x = 100;
        return x;
    }

    return x;
}

f(false, 0); // returns 0
f(true, 0);  // returns 100
```

在一个嵌套作用域里引入一个新名字的行为称做*屏蔽*。 它是一把双刃剑，它可能会不小心地引入新问题，同时也可能会解决一些错误。 例如，假设我们现在用`let`重写之前的`sumMatrix`函数。

```typescript
function sumMatrix(matrix: number[][]) {
    let sum = 0;
    for (let i = 0; i < matrix.length; i++) {
        var currentRow = matrix[i];
        for (let i = 0; i < currentRow.length; i++) {
            sum += currentRow[i];
        }
    }

    return sum;
}
```

这个版本的循环能得到正确的结果，因为内层循环的`i`可以屏蔽掉外层循环的`i`。

*通常*来讲应该避免使用屏蔽，因为我们需要写出清晰的代码。 同时也有些场景适合利用它，你需要好好打算一下。

## `let`和`const`用哪个

现在我们有两种作用域相似的声明方式，我们自然会问到底应该使用哪个。 与大多数泛泛的问题一样，答案是：依情况而定。

使用[最小特权原则](https://en.wikipedia.org/wiki/Principle_of_least_privilege)，所有变量除了你计划去修改的都应该使用`const`。 基本原则就是如果一个变量不需要对它写入，那么其它使用这些代码的人也不能够写入它们，并且要思考为什么会需要对这些变量重新赋值。 使用`const`也可以让我们更容易的推测数据的流动。

另一方面，用户很喜欢`let`的简洁性。 这个手册大部分地方都使用了`let`。



## 解构数组

最简单的解构莫过于数组的解构赋值了：

```typescript
let input = [1, 2];
let [first, second] = input;
console.log(first); // outputs 1
console.log(second); // outputs 2
```

这创建了2个命名变量 `first` 和 `second`。 相当于使用了索引，但更为方便：

```typescript
first = input[0];
second = input[1];
```

解构作用于已声明的变量会更好：

```typescript
// swap variables
[first, second] = [second, first];
```

作用于函数参数：

```typescript
function f([first, second]: [number, number]) {
    console.log(first);
    console.log(second);
}
f(input);
```

你可以在数组里使用`...`语法创建剩余变量：

```typescript
let [first, ...rest] = [1, 2, 3, 4];
console.log(first); // outputs 1
console.log(rest); // outputs [ 2, 3, 4 ]
```

当然，由于是JavaScript, 你可以忽略你不关心的尾随元素：

```typescript
let [first] = [1, 2, 3, 4];
console.log(first); // outputs 1
```

或其它元素：

```typescript
let [, second, , fourth] = [1, 2, 3, 4];
```

## 对象解构

你也可以解构对象：

```typescript
let o = {
    a: "foo",
    b: 12,
    c: "bar"
};
let { a, b } = o;
```

这通过 `o.a` and `o.b` 创建了 `a` 和 `b` 。 注意，如果你不需要 `c` 你可以忽略它。

就像数组解构，你可以用没有声明的赋值：

```typescript
({ a, b } = { a: "baz", b: 101 });
```

注意，我们需要用括号将它括起来，因为Javascript通常会将以 `{` 起始的语句解析为一个块。

你可以在对象里使用`...`语法创建剩余变量：

```typescript
let { a, ...passthrough } = o;
let total = passthrough.b + passthrough.c.length;
```

## 属性重命名

你也可以给属性以不同的名字：

```typescript
let { a: newName1, b: newName2 } = o;
```

这里的语法开始变得混乱。 你可以将 `a: newName1` 读做 “`a` 作为 `newName1`“。 方向是从左到右，好像你写成了以下样子：

```typescript
let newName1 = o.a;
let newName2 = o.b;
```

令人困惑的是，这里的冒号*不是*指示类型的。 如果你想指定它的类型， 仍然需要在其后写上完整的模式。

```typescript
let {a, b}: {a: string, b: number} = o;
```

## 默认值

默认值可以让你在属性为 undefined 时使用缺省值：

```typescript
function keepWholeObject(wholeObject: { a: string, b?: number }) {
    let { a, b = 1001 } = wholeObject;
}
```

现在，即使 `b` 为 undefined ， `keepWholeObject` 函数的变量 `wholeObject` 的属性 `a` 和 `b` 都会有值。

## 函数声明

解构也能用于函数声明。 看以下简单的情况：

```typescript
type C = { a: string, b?: number }
function f({ a, b }: C): void {
    // ...
}
```

但是，通常情况下更多的是指定默认值，解构默认值有些棘手。 首先，你需要在默认值之前设置其格式。

```typescript
function f({ a, b } = { a: "", b: 0 }): void {
    // ...
}
f(); // ok, default to { a: "", b: 0 }
```

其次，你需要知道在解构属性上给予一个默认或可选的属性用来替换主初始化列表。 要知道 `C` 的定义有一个 `b` 可选属性：

```typescript
function f({ a, b = 0 } = { a: "" }): void {
    // ...
}
f({ a: "yes" }); // ok, default b = 0
f(); // ok, default to {a: ""}, which then defaults b = 0
f({}); // error, 'a' is required if you supply an argument
```

**要小心使用解构。 从前面的例子可以看出，就算是最简单的解构表达式也是难以理解的。 尤其当存在深层嵌套解构的时候，就算这时没有堆叠在一起的重命名，默认值和类型注解，也是令人难以理解的。 解构表达式要尽量保持小而简单。 你自己也可以直接使用解构将会生成的赋值表达式。**

## 展开

展开操作符正与解构相反。 它允许你将一个数组展开为另一个数组，或将一个对象展开为另一个对象。 例如：

```typescript
let first = [1, 2];
let second = [3, 4];
let bothPlus = [0, ...first, ...second, 5];
```

这会令`bothPlus`的值为`[0, 1, 2, 3, 4, 5]`。 展开操作创建了`first`和`second`的一份浅拷贝。 它们不会被展开操作所改变。

你还可以展开对象：

```typescript
let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
let search = { ...defaults, food: "rich" };
```

`search`的值为`{ food: "rich", price: "$$", ambiance: "noisy" }`。 对象的展开比数组的展开要复杂的多。 像数组展开一样，它是从左至右进行处理，但结果仍为对象。 这就意味着出现在展开对象后面的属性会覆盖前面的属性。 因此，如果我们修改上面的例子，在结尾处进行展开的话：

```typescript
let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
let search = { food: "rich", ...defaults };
```

那么，`defaults`里的`food`属性会重写`food: "rich"`，在这里这并不是我们想要的结果。

对象展开还有其它一些意想不到的限制。 首先，它仅包含对象 [自身的可枚举属性](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)。 大体上是说当你展开一个对象实例时，你会丢失其方法：

```typescript
class C {
  p = 12;
  m() {
  }
}
let c = new C();
let clone = { ...c };
clone.p; // ok
clone.m(); // error!
```

