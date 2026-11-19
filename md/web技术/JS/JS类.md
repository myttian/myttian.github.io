### 1、概述

##### 1、定义类

**类是用于创建对象的模板**：用 class 关键字来创建一个类，类中包含一个特殊的方法 **constructor()**，它是类的构造函数。

```js
class ClassName {
  constructor() { ... }
}
   
class Runoob {
  constructor(name, url) {
    this.name = name;
    this.url = url;
  }
}            /*创建了一个类Runoob。类中初始化了两个属性： "name" 和 "url"。 */

let site = new Runoob("菜鸟教程",  "https://www.runoob.com");
```

##### 2、使用类

定义好类后，用 **new** 关键字来创建对象，创建对象时会自动调用构造函数方法 **constructor()**

类表达式是定义类的另一种方法。类表达式可以命名或不命名。 命名类表达式的名称是该类体的局部名称。

```js
// 未命名/匿名类
let Runoob = class {
  constructor(name, url) {
    this.name = name;
    this.url = url;
  }
};
console.log(Runoob.name);
// output: "Runoob"
 
// 命名类
let Runoob = class Runoob2 {
  constructor(name, url) {
    this.name = name;
    this.url = url;
  }
};
console.log(Runoob.name);
// 输出: "Runoob2"
```

### 2、类继承

[JavaScript 类继承](https://www.runoob.com/js/js-class-inheritance.html)

JavaScript 类继承使用 extends 关键字；已有的类称为**基类（父类）**，新建的类称为**派生类（子类）**。

super()方法用于调用父类的构造函数。这样就可以访问父类的属性和方法

```javascript
// 基类
class Animal {
    // eat() 函数
    // sleep() 函数
};
 
 
//派生类
class Dog extends Animal {
    // bark() 函数
};
```

```JS
class Site {
  constructor(name) {
    this.sitename = name;
  }
  present() {
    return '我喜欢' + this.sitename;
  }
}
 
class Runoob extends Site {
  constructor(name, age) {
    super(name);              //super()方法用于调用父类的构造函数。这样就可以访问父类的属性和方法.
    this.age = age;
  }
  show() {
    return this.present() + ', 它创建了 ' + this.age + ' 年。';
  }
}
 
let noob = new Runoob("菜鸟教程", 5);
document.getElementById("demo").innerHTML = noob.show();
```

### 3、getter 和 setter

类中可以使用 getter 和 setter 来获取和设置属性值，getter 和 setter 需要在严格模式下执行。 使我们对属性的操作变的很灵活。

类中添加 getter 和 setter 使用的是 get 和 set 关键字；getter 是一种获得属性值的方法，setter是一种设置属性值的方法

很多开发者在属性名称前使用下划线字符 **_** 将 getter/setter 与实际属性分开

### 4、静态方法

静态方法是使用 static 关键字修饰的方法，又叫类方法，属于类的，但不属于对象，在实例化对象之前可以通过 **类名.方法名** 调用静态方法。

静态方法不能在对象上调用，只能在类中调用。

```js
class Runoob {
  constructor(name) {
    this.name = name;
  }
  static hello() {
    return "Hello!!";
  }
}
 
let noob = new Runoob("菜鸟教程");
 
// 可以在类中调用 'hello()' 方法
document.getElementById("demo").innerHTML = Runoob.hello();
 
// 不能通过实例化后的对象调用静态方法
// document.getElementById("demo").innerHTML = noob.hello();
// 以上代码会报错
//如果想在对象 noob 中使用静态方法，可以作为一个参数传递给它：
document.getElementById("demo").innerHTML = Runoob.hello(noob);
```

