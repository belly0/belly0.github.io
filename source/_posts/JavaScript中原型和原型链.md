---
title: JavaScript中原型和原型链
date: 2020-11-04 00:02:17
tags:
---

# 1.数据类型

JavaScript的数据类型分为**基本数据类型**和**引用数据类型**。

> 1.基本数据类型
>
> String
>
> Number
>
> Boolean
>
> null
>
> undefined
>
> Symbol(ES6）
>
> 2.引用数据类型
>
> Object

# 2.构造函数

 面向对象编程，总是得生成对象。对象是单个实物的抽象，它表示了某一类实物的共同特征。而构造函数就是专门用来生成实例对象的函数，其作为对象的模板。一个构造函数，可以生成多个实例对象，这些实例对象具有相同的结构。


- 区别于其他普通函数，构造函数名的首字母大写；

- 构造函数内部使用的this关键字，指所要生成的对象实例；

- new命令生成对象。
  *new会创建一个新对象，作为要返回的对象实例；将这个空对象的原型，指向构造函数的prototype属性；将这个空对象赋值给函数内部的this关键字；开始执行构造函数内部的代码。*

  ```javascript
  var Fn=function(){
      name='xxx';
      old=18;
  }
  var f=new Fn();
  console.log(f.name);//undefined
  console.log(f.old);//undefined
  f.name='yyy';
  console.log(f.name);//yyy
  ```

  

# 3.原型是什么？原型链是什么？

对象由函数创建，而函数亦是一种对象。

> Function.prototype.__proto__===Object.prototype  //true
>
> 且Object.prototype.__proto__===null为true

所以每个函数都有一个属性prototype;该prototype属性值是一个对象，默认只有一个constructor的属性，指向这个函数本身。

**原型**是一个prototype对象，用于表示类型之间的关系；

**原型链**指的是在JavaScript中对象之间的继承是通过prototype对象指向父类对象，直到指向Object对象为止，这样就形成了一个原型指向的链条，专业术语称之为原型链。

例如：Student——>Person——>Object *学生*继承*人*类，*人*类继承*对象*类

```javascript
var Person=function(){
   this.age="匿名"
};  
var Student=function(){};  
//创建继承关系,prototype执行Person的一个实例对象  
Student.prototype=new  Person();
```

**五条原型规则：**

1. 所有的引用类型（数组、对象、函数），都具有对象特性，即可自由扩展属性（除了“null”以外）；
2. 所有的引用类型都有一个_proto_属性，叫隐式原型，属性值是一个普通的对象；
3. 所有的函数，都有一个prototype属性，叫显式属性，属性值是一个普通对象；
4. 所有的引用类型的_proto_属性，指向它的构造函数的prototype属性值；

> var 对象名 = new 函数名();
>
> 对象名.__proto__ === 函数名.prototype；

5. 当试图得到一个对象的某个属性时，如果没有，会向它的_proto_中寻找，即向它的构造函数的prototype中寻找。

例如：

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>JavaScript中的原型和原型链</title>
	<script type="text/javascript">
		console.log("五条原型规则实例");
		// 1.所有的引用类型都具有对象属性
		var obj = {};
		obj.a = 100;
		var arr = [];
		arr.a = 100;
		function fn() {};
		fn.a = 100;

		// 2.所有的引用类型都有一个隐式原型
		console.log(obj._proto_);  //undefined
		console.log(arr._proto_);  //undefined
		console.log(fn._proto_);   //undefined

		// 3.所有的函数都有一个prototype属性
		console.log(fn.prototype);  //Object

		// 4.所有的引用类型，_proto_属性值指向它的构造函数的"prototype"属性值
		console.log(obj.__proto__ === Object.prototype);   //true

		// 5.当试图得到一个对象的某个属性时，如果没有，会向它的_proto_中寻找，即向它的构造函数的prototype中寻找。
		// 构造函数
		function Person(name,age) {
			this.name = name;
		}
		Person.prototype.alertName  = function() {
			console.log("构造函数" + this.name);
		}
		// 创建实例
		var p = new Person('lily');
		p.printName = function() {
			console.log(this.name);
		}
		// 测试
		p.printName(); //lily
		p.alertName(); //构造函数lily
	</script>
</head>
<body>

</body>
</html>
```

例子：Dog类继承了Animal类，即拥有了Animal的eat方法

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>JavaScript中的原型和原型链</title>
</head>
<body>
	<script type="text/javascript">
		function Animal() {
			this.eat = function() {
				console.log("animal eat");
			}
		}
		function Dog() {
			this.bark = function() {
				console.log("dog bark");
			}
		}
		Dog.prototype = new Animal();
		var xiaohuang = new Dog();
		xiaohuang.eat();    //animal eat
		xiaohuang.bark();   //dog bark
	</script>
</body>
</html>
```

