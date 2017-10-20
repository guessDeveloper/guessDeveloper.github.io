---
title: '什么是Symbol'
date: 2017-10-20 14:48:42
tags: es6
categories: js
---
上回提到了基本数据类型里es6添加了一种类型Symbol(独一无二)。
es5中对象的属性名都是字符串，这很容易引起冲突。比如在他人的对象上添加一个自己的新属性，新增的属性名很容易跟之前的属性名冲突。为了保证这个属性名是独一无二的，所以es6引入Symbol类型。

##### 概念

es6引入了一种新的原始数据类型Symbol,表示独一无二的值。Symbol通过Symbol函数生成。所以对象的属性名现在可以有两种类型，一种是字符串，另一种是新增的Symbol类型。所有属性名属于Symbol类型，都是独一无二的，不会与其他属性名产生冲突。

```
let s = Symbol();
console.log(typeof(s)) // symbol
```
>Symbol函数前不能使用new命令，否则会报错。因为Symbol是原始数据类型，他并不是对象，也就是说Symbol也不能添加属性，他是一种类似字符串的其他类型。

Symbol函数可以接受一个字符串作为参数，作为对其实例的描述，容易区分。

```
let s1 = Symbol('foo');
let s2 = Symbol('bar');
console.log(s1) //Symbol(foo)
console.log(s2) //Symbol(bar)
s1.toString() // 'Symbol(foo)'
s2.toString() // 'Symbol(bar)'
```
如果Symbol函数的参数是一个对象，就会调用改对象的toString()方法，将其转化为字符串。

```
const obj = {
   toString(){
     return 'abc';
   }
}
const sym = Symbol(obj);
console.log(sym) // Symbol(abc)
```
>Symbol函数只是对其的描述，相同参数的Symbol函数的返回值是不相等的。同时其不能与其他类型的值进行运算，会报错。可以转换为字符串，布尔值。但是不能转为数值。

```
//没有参数
let s1 = Symbol();
les s2 = Symbol();

s1 === s2 //false
//有参数
let s1 = Symbol('hh');
les s2 = Symbol('hh');

s1 === s2 //false

let sym = Symbol('young');

"your are" + sym
// TypeError: can't convert symbol to string

//可转换为布尔值
let sym = Symbol();
Bloolean(sym); //true
!sym //false
// 不能转换为数值
Number(sym) //TypeError

```
##### Symbol用作属性名

Symbol用作属性名有三种写法

```
let sym = Symbol();

//第一种写法
let a = {};
a[sym] = 'Hello';
//第二种写法
let a = {
   [sym]:'Hello'
}
//第三种写法
let a = {};
Object.defineProperty(a,sym,{value:'Hello'});

a[sym] // 'Hello'

```
>Symbol 不能用点运算符

Symbol的用法还有很多在这里就不再一一介绍了，有兴趣的小伙可以去[阮一峰的ECMAScript6入门](http://es6.ruanyifeng.com/#docs/symbol)（膜拜阮大神）做详细了解。
