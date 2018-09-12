# 对__proto__和prototype的理解。
在js中万事万物皆对象，Functiong (方法)、方法的原型（Function.prototype）也是对象。在对象中，
都有一个__proto__属性。方法（Function）作为一个特殊对象，除了拥有__proto__属性外，还有一个prototype属性。

# 原型对象
该对象包含所有实例共享的属性和方法。原型对象有一个constructor属性，这个属性包含一个指针，指回原构造函数。

# 定义
__proto__: 隐式原型，所有对象都具有该属性，一个对象的隐式原型指向构造该对象的构造函数的原型。
prototype: 显示原型，每个函数在创建后都拥有一个prototype属性，该属性指向函数的原型对象。

#作用
__proto__：是用来构造原型链，用于实现基于原型的继承。保证了实例可以访问到构造函数原型中定义的属性和方法。
prototype: 用来实现基于原型的继承与属性的共享。

#二者关系
隐式原型指向构造该对象的构造函数（constructor）的prototype。

#图解
![原型图解](https://github.com/footars/lanygrp/blob/master/images/prototype.jpg)

1. 构造函数Foo()
构造函数的原型属性Foo.prototype指向了原型对象，在原型对象中的所有属性和方法，都可以通过构造函数Foo声明的实例（f1,f2）共享。

2. 原型对象Foo.prototype
Foo.prototype保存着所有实例共享的属性和方法，原型对象中有一个constructor属性，指向构造函数。

3. 实例
f1、f2 是通过Foo声明的实例，这两个对象中都保存这__proto__属性，指向该实例构造函数的原型对象（Foo.prototype），因此f1、f2就可以访问构造函数原型对象中的所有属性和方法。

# 注意
构造函数Foo()除了是方法外也是对象，也有__proto__属性，指向它的构造函数的原型对象，即Function.prototype。
Function()，Object()也是同理。
最终的Object.prototype的__proto__指向null。

#实例

let one = {a:0};
let two = new Object();

one.__proto__ === one.prototype // true
two.__proto__ === two.prototype // true
one.toString === one.__proto__.toString // true

# 所有的内置对象都是由Object()创建而来。
如： Array.prototype.__proto__ === Object.prototype // true

构造函数：
function Foo(){}
let test = new Foo();
Foo.prototype.__proto__ === Object.prototype // true
test.__proto__ === Foo.prototype // true

原型继承：
1. 继承实例
functiong Boo(){}
Foo.prototype = new Boo();
Foo.porototype.__proto__ === Boo.prototype // true
Foo.prototype.constructor === Boo // true

2. 继承对象
Foo.prototype = {
	a: 1,
	b: 2
}
Foo.prototype.__proto__ === Object.prototype // true
以上两种情况都是重写了Foo.prototype实现的继承，所以Foo.prototype.constructor也被重写。
