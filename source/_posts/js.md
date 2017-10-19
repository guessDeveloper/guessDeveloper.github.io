---
title: 'js 基本数据类型与引用数据类型'
date: 2017-10-19 13:57:55
tags: js es6
categories: js
---
#### 基本数据类型与引用数据类型及传输原理
js的数据类型划分为引用数据类型和基本数据类型

> 基本数据类型
基本数据类型包括 number string 布尔值 null undefind symbol(es6新增)
存储在栈(stack)中的简单数据段，它们的值直接存储在变量访问的位置，栈区包含了变量的标识符和变量值。

> 引用数据类型
引用数据类型包括 数组 对象 函数
存储在堆(heap)中,所以变量存储的只是一个指向对象在内存处的指针。放在栈空间的值是指向对象的栈中地址。

![堆栈](http://www.w3school.com.cn/i/ct_js_value.gif?_=6671909)

##### 按值传递与按引用传递

按值传递(call by value)常用的求职策略 (函数的形参是被调用时所传实参的副本，修改形参的值不会影响实参值)
按引用传递(call by reference)  (函数形参接受实参的隐式引用，而非副本。当形参值发生变化的时候实参也会影响，两者指向的是相同的值。)

```
var name = 'joke';
var rename = name;
name = 'jake'
console.log(name.rename) // jake joke
```
name 的值修改并没有改变rename，所以这里是按值传递。赋值创建了新的内存空间。

##### 基本数据类型

不可变性(immutable)

基本类型是不可变的(immutable),只有引用类型才是可变的,我们在尝试改变字符串的内容时,js都会看做创建新的字符串。
```
var str = 'abc';
str[0] // 'a'
str[0] = c 
console.log(str) // 'abc'

var name = 'wang';
var upName=name.toUpperCase(); 
name.attr = 'hhh';
console.log(upName,name); // 输出 'WANG' 'wang'
console.log(name.attr); // undefind

```
我们无法改变，也无法添加任何属性方法。

##### 引用数据类型

```
var obj = {x:1};
var o = obj;
o.x = 100 ;
console.log(obj.x) \\ 100;
o = {x:200} \\ 重新赋值 新的内存空间
console.log(JSON.stringify(obj),JSON.stringify(o))//{"x":100} {"x":200})

```
引用类型的值是同时保存栈内存和堆内存的对象

>js 不允许直接访问内存中的位置，也就是说不能操作对象的内存空间。但是我们可以操作对象的引用。
准确的说，引用类型的存储需要内存的栈区和堆区（栈内存、堆内存）共同完成。栈内存保存变量的标识和指向对象堆内存的指针。

```
var obj1 = {};
var obj2 = {};
console.log(obj1 == obj2 ) //false
```
引用类型按引用访问，比较时对比两个对象的堆内存地址是否相同。

##### 两种数据类型在形参与实参中的区别

###### 先说说什么是实参跟形参
实参：可以是变量、常量、表达式、函数等。在函数调用时必须是确定值，以便把值传给形参。
形参：全称 “形式参数” 在定义函数名和函数体时使用的参数，目的是接受调用函数时的参数。

```
function add(p){
   p+=100;
   return p
}
var num = 99;
var result = add(num);
console.log(result,num) \\199,99
```
num是实参,p是形参,add函数在调用时p接受num的传值，在函数内操作。num没有发生变化。但是当num是引用类型的时候。

```
function add(p){
   p[0]=100;
   return p
}
var num = [98];
var result = add(num);
console.log(result,num) \\[100],[100]

```
在方法内 形参的改变将影响实参。这个现象在其他语言中不存在。例如php

```
<?php
function fun($p){
   $p[0] = 99;
}
$num = [10];
fun($num)
var _dump($num);
/*
 array(size = 1)
   0 => int 10
/*
?>
```


