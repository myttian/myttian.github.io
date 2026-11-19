---
typora-copy-images-to: images
typora-root-url: ./
---

### 1、入门

视频： [视频教程](https://www.bilibili.com/video/BV1VS4y1U7Pj/?p=2&vd_source=7346303e5e18677d7261c2c0c109ecfd) 

[TS ](https://www.cnblogs.com/frontvelsun/p/16388240.html)   

### 2、TypeScript

TS组成部分：`模块、函数、变量、语句和表达式、注释`     [VsCode下部署TypeScript环境](https://www.cnblogs.com/aniugg/articles/16699930.html)		[前端乐哥TS视频教程](https://www.bilibili.com/video/BV1VS4y1U7Pj/?p=34&vd_source=7346303e5e18677d7261c2c0c109ecfd)

typescript是js的超集，主要学习ts里面的原始类型、字面量类型、数组类型、函数类型、类类型、接口类型、类型别名、联合与交叉类型、枚举类型、泛型等类型元素，以及类型推断、类型断言、类型缩小、类型放大等特性。

`区分大小写、每行指令结尾分号可选 console.log("Runoob")`TS面向对象编程 

- **类**：类是一个模板，描述一类对象的行为和状态
- **对象**：对象是类的一个实例，有状态和行为
- **方法**：方法是类的操作的实现步骤

`tsc -init 创建项目，出现tsconfig.json;  outDir    终端-运行任务-显示所有任务-监视 或 tsc -p tsconfig.json --watch`

#### 1、<span style=color:red>数据类型</span>

##### 1、原始类型

- **string，number，boolean，symbol，null，undefined**

```
const num=1;	//类型是1，常量不能改变指向（不能被修改），它的值就是类型
let str="3"		//值就是类型，初始值决定类型
let sy:symbol=Symbol("123")	//如果有2个变量，一个值是Symbol("123")，另一个也是，它们值不相等，Symbol创建出来的，地址(内存空间)永远是新建的
function a(){}	//ts函数没有返回值，函数类型就是void， a()：void{}
```



##### 2、非原始类型

-  小o, 大O,{}
   - let obj:object = [1];   包括对象、数组
   - let obj:Object = {b:1}:  包括基础数据类型
   - let obj:{} = {b:1};       等效于Object

##### 3、数组

```ts
export{} //导出为空

// 声明变量为数组; 在元素类型后面加上[]； 数组元素类型一致，便于处理
//数组声明时未设置类型，则会被认为any类型，在初始化时根据第一个元素的类型来推断数组的类型
let arr: number[] = [1, 2];		//说明数组里都是number类型; arr: number[]声明，[1, 2]初始化 

// 或者使用数组泛型(类型参数化) ；number类似一个参数传进去
let arr: Array<number> = [1, 2];

//数组解构:把数组元素赋值给变量
var arr:number[] = [12,13] 
var[x,y] = arr // 将数组的两个元素赋值给变量 x 和 y

//数组在函数中的使用:作为参数传递给函数;  作为函数的返回值
```

##### 4、联合类型

```ts
//通过管道(|)将变量设置多种类型，赋值时可以根据设置的类型来赋值  
var val:string|number 
```

##### 5、交叉类型

```ts
//& 属性必须都有； 
let obj:{name:string,age:number} & {height:number} ;
obj = {name:"张三",age:1, height:2}
```

  6、联合、交叉类型

```ts
//& 优先 | ;            两套类型选一套出来用
let obj:{name:string} & {age:number} | {name:number} & {age:string};

obj = {
	name: "zhangsan",
	age: 17
}

obj = {
	name: 2,
	age: "17"
}
```

##### 7、any和unknow区别

- 不推荐any，绕过类型校验，相当于不是在写TS
- unknow有做类型校验
##### 8、接口类型

[ interface与type区别](https://blog.csdn.net/zxl1990_ok/article/details/125153958)    [联合类型与交叉类型](https://www.bilibili.com/read/cv16612483/)  [联合、交叉类型](https://www.kancloud.cn/jiangjing/typescript/2759985)  [看云文档管理](https://www.kancloud.cn/@jiangjing)  [广场 · 看云](https://www.kancloud.cn/explore) 

```ts
//接口用来定义类型；    一系列抽象方法的声明，要由具体的类去实现; 
// 定义接口类型--给数组用
interface ArrayNumber {
  [idx: number]: number; //下标类型(idx:number)：值类型(number)
}

let arr1: ArrayNumber = [1, 2, 3];

// 定义接口类型--给函数用
//很少使用接口类型来定义函数的类型，更多使用内联类型或类型别名配合箭头函数语法来定义函数类型
interface FnItf {
  (p:string,a:number): void;  //形参及类型：返回值类型
}

let fn:FnItf = (p:string,a:number): void => {}
fn("",1)



```

```ts
//TypeScript 不仅能帮助前端改变思维方式，还能强化面向接口编程的思维和能力，而这正是得益于 Interface 接口类型
//使用接口定义变量和函数参数的类型
interface PersonInfo {
  name: string;
  age: number;
}
// 定义变量的类型
let zhangsan: PersonInfo = {
  name: "张三",
  age: 20,
};

// 定义数组的类型
interface ArrayNumber {
  [idx: number]: number;
}

let arr1: ArrayNumber = [1, 2, 3];

// 定义函数的类型
interface PersonFn {
  (p: PersonInfo): void;
}

let Person1: PersonFn = (obj: PersonInfo): void => {
  console.log(obj.name, obj.age);
};
```

接口继承、同名、缺省、只读

- **继承**

```ts
//多个不同名字的接口可以实现继承，组合成一个新的接口
interface NameInfo {
  name: string;
}
interface AgeInfo {
  age: number;
}
interface PersonInfo extends NameInfo, AgeInfo {
  height: number;
}

let p: PersonInfo = {
  name: "张三",
  age: 20,
  height: 177,
};
```

- **同名接口**

  ```ts
  interface AItf {
      a: number
  }
  interface AItf {
      b: string,
  }
  //同名特点：合并了所有属性类型; 可扩展性更好
  let obj:AItf = {
    a:1,
    b:"b"
  };
  ```

  

- **缺省、只读**

  ```ts
  interface PersonInfo {
    name?: string; // 缺省； 加个问号，可选，可以不要
    readonly height: number; // 只读
  }
  ```

##### 9、类型别名type

`给类型起别名`

`接口类型的一个作用是将内联类型抽离出来，从而实现类型可复用。也可以使用类型别名接收抽离出来的内联类型实现复用。格式：`type` 别名名称 = 类型定义`

```ts
type StrOrNum = string | number			//联合类型定义
let str:StrOrNum = "1"
str=10

type ObjType = {a:number&2,b:string}	//交叉类型定义
let obj:ObjType = {
	a:2	
	b:"bb"
}

//interface和type区别：都可以用来自定义类型； 类型别名支持联合和交叉类型定义； 类型别名不支持重名(复)定义，接口可以
interface AItf{
    a:string
}
type Atype = AItf['a'];  //Atype拿到的就是string类型 ；用类型别名保存接口上的某个属性类型； 接口和类型别名混着用，类型别名从接口取类型用
let str2:Atype = "10"

type color = 'red' | 'blue' | string & {}
let c:color = 'red'
```

`多数的情况下使用接口类型和类型别名的效果等价，但是在某些特定的场景下这两者还是存在很大区别。
重复定义的接口类型，它的属性会叠加，这个特性使得我们可以极其方便地对全局变量、第三方库的类型做扩展
如果我们重复定义类型别名，那么就会报错`

##### 10、变量声明

[类型断言](https://www.jianshu.com/p/0aea34031246)

> 1. 变量使用前必须先声明
>    1. 声明变量的类型及初始值  `var [变量名] : [类型] = 值;`
>    2. 声明变量并初始值，但不设置类型，该变量可以是任意类型 `var [变量名] = 值;`
>    3. 声明类型，但没有初始值，值会设置为 undefined `var [变量名] : [类型];`
>    4. 没有类型和初始值，类型可以是任意类型，默认初始值为 undefined  `var [变量名];`

- **类型断言**：手动指定一个值的类型  ` <类型>值  或  值 as 类型`
- **类型推断**：类型没有时，TS编译器利用类型推断来推断类型； 根据初始赋值推导出变量类型，以后类型不能改

#### 2、<span style=color:red>函数</span>

带参数函数：  `function func_name( param1 [:datatype], param2 [:返回值类型]) { }`

```ts
//接口定义函数类型
interface FnItf{
	(p:string):number
}
let fn:FnItf = (p:string):number => {	//形参及类型：返回值类型
	returen 1
}
fn("")

//类型别名定义函数类型
type addFnType = (a: number, b:number) => void;	//返回值void
let fn2: addFnType = (num1, num2) => {}
fn2("")
```

- ==可选参数-问号?==： 如果定义了参数，必须传入参数，除非设置为可选，可选参数使用问号, 可选参数必须跟在必需参数后面   `function fn(a: string, b?: string) { }`

- ==默认参数==-等号： 如果不传入该参数的值，则使用默认参数   `function fn(a:number,b:number = 3) {return a+b }` ;    fn(5)

- ==剩余参数==：不知道要向函数传入多少个参数， 将一个不确定数量的参数作为一个数组传入；` function fn2(a:number, b:number, ...) { }   `            fn2(1,2,3,4,5,6)    [nums ](https://blog.csdn.net/Caesar6666/article/details/120394616)  [深拷贝和浅拷贝](https://www.cnblogs.com/SpringAndMoon/p/14549609.html)   

  ```ts
  function sum(...nums: number[]) {       		//...arr:number[]  数组里全是数字   nums列表类型
      return nums.reduce((a, b) => a + b, 0);
  }
  sum(1, 2); // => 3
  sum(1, 2, 3); // => 6
  ```

  ```ts
  //浅拷贝只是复制地址； 深拷贝完全复制，开辟对应的空间，空间大小占用一样但是位置不同
  //假设B复制了A，当修改A时，看B是否会发生变化，如果B也跟着变了，说明这是浅拷贝，如果B没变，那就是深拷贝
  let obj1 = {a:1,b:2,c:[1,2,3]}
  let obj2 = {...obj1}		//此时b： {a:1,b:2,c:[1,2,3]}
  obj1.a = 100
  obj1.c[0] = 1000
  console.log(obj1)	// => {a:100,b:2,c:[1000,2,3]}
  console.log(obj2)	// => {a:1,b:2,c:[1000,2,3]}  浅拷贝：拷贝了第一层（1，2）； 数组里面的没有拷贝；（和obj1原值相比）
  ```

  

- 构造函数：使用构造函数Function()来定义函数    `var res = new Function ([arg1[, arg2[, ...argN]],] functionBody)`

- 递归函数：函数内调用函数本身 

- Lambda函数：即箭头函数  `( [param1, param2,…param n] )=>statement;`

- ==函数重载==：方法名相同，参数不同，返回类型可以相同也可以不同

##### 1、promise

```ts
interface DataItf {     	//定义data类型，定义接口被其它接口调用
    a: number;
    b: number;
}

interface ResItf {      	//通过接口定义res的类型，有三个属性，规定了resolve的参数类型
    code: number;
    data: DataItf[];        //{a:number,b:number}[]，每个元素都有a和b属性; 这里还可以写成接口形式
    message: string
}

//Promise对象：   p对象名：Promise<res的类型>
let p: Promise<ResItf> = new Promise((resolve, reject) => {     // < >泛型
    resolve({		//对象，传数据
        code: 0,
        data: [{ a: 1, b: 2 }, { a: 11, b: 22 }],
        message: ""
    })
})
p.then(res => {		//接收处理数据
    if (res.code == 0) {
        res.data.map(item => item.a)
    }
})
```

##### 2、this

ts中，要指明this指向；  必须要明确的指定this的类型（严格模式下）

```ts
interface Window{	//用接口扩展myname属性
    myname:string
}

//ts提供了Window类型，window是Window类型的对象
function Person(this:Window,name: string) {   //ts中，要指明this指向，即this类型（在函数第一个形参处注明）
        
    //Window类型中没有myname属性，需要通过接口扩展这个属性    
    this.myname = name
}
window.Person("")
```

```ts
interface Window {
    person: (n: string) => void;
    myname: string;
  }
type objType = {person: (n: string) => void, myname: string};

function person(this: Window | objType , name: string):void {
    this.myname = name;
    console.log(this.myname);
}

window.person = person;
window.person('window name');

let obj:objType = {
    person,
    myname: ''
};
obj.person('obj name');
```

加export{ }后， 要创建一个类型声明文件**global.d.ts**，为window对象上扩展两个属性person、myname

```ts
//global.d.ts， 在全局上，给Window接口扩展这个属性
interface Window{
    Person:(n:string)=>void;	//Person是函数类型
    myname:string
}
```

```ts
export{ }
//加export{} ,这里就不是全局，这里扩展到Window接口就失效了，需要写到global.d.ts

function Person(this:Window,name: string) {  
    this.myname = name
}

//加export{} ,这里就不是全局，Person不是window下的属性，Person函数挂到window.Person下
window.Person = Person
window.Person("")
```

让this指向自定义对象 ：`function person(this: Window | objType , name: string):void`

```ts
//让this指向自定义对象
export { }
type ObjType = { myname: string, Person: (m: string) => void }

let obj: ObjType = {    //定义一个 obj对象
    myname: "zhang",
    Person: () => { }
}
//定义函数时，this的类型，必须和调用时的类型一致
function Person(this:ObjType,name: string) {
    this.myname = name
}

obj.Person = Person
obj.Person("xxxx")
```

this指向的联合类型写法：

#### 3、<span style=color:red>数组</span>

#### 4、<span style=color:red>对象</span>

#### 5、<span style=color:red>元组</span>

```ts
//元组用来表示：数组中元素的数据类型不必相同， 对应位置的类型需要相同
let x: [string, number];
x = ['Runoob', 1];    // 运行正常
x = [1, 'Runoob'];    // 报错
console.log(x[0]);    // 输出 Runoob

//元组可以作为参数传递给函数

//解构元组： 把元组元素赋值给变量
var a =[10,"Runoob"] 
var [b,c] = a 
console.log( b )   //10
console.log( c )   //Runoob
```



### 3、高级

#### 1、枚举

```ts
//枚举类型用于定义数值集合
enum Color {Red, Green, Blue};
let c: Color = Color.Blue;
console.log(c);    // 输出 2

//枚举不是用来定义类型(接口），用来列举数据
enum StatusCode {
    success = 200,
    paramsError = 400,
    serverError = 500
}
let code: string | number = 400;
if (code == StatusCode.success) {
    console.log('成功');
} else if (code == StatusCode.paramsError) {
    console.log('失败，请求参数问题')
} else if (code == StatusCode.serverError) {
    console.log('失败，服务器问题')
}
```

#### 2、泛型

```ts
// 数组泛型(类型参数化) ；number类似一个参数传进去
let arr: Array<number> = [1, 2];
```

```ts
//T只是标识符，<T>里的类似一个形参，调用时传进来一个类型
function fn1<T>(n: T): T { // function fn1<T,G>(n: T,m:G): T 多个形参
    return n;
}
fn1<number>(100)   //调用时传number类型，类似实参
```

泛型在类型别名和接口上的应用

泛型约束：extends

```ts
type ObjType<N, G = number> = { name: N, getName: () => G }		//给泛型一个默认类型 G=number

//约束：extends 限制泛型只能传某种数据类型； 
interface PersonItf<N extends string|number,G>{
    name:N;
    getName:()=>G
}
```

#### 3、定义类

```ts
export{}
//定义类的同时，会创建一个相同名字的接口
class Preson {
    myName: string = '';       	// 定义属性前，要先声明属性的类型
    constructor(n: string) {	//构造函数,从外部传进来参数n，张三
        this.myName = n;
    }
    getName() {
        return this.myName
    }
}
let p = new Preson('张三');
console.log(p.myName);
console.log(p.getName());

let obj:Preson={    //既然有相同名字接口，就可以做类型
    myName: '',
    getName(){
        return ""
    }
}
```
##### ==类继承==

```ts
export { }
class Person {
    myName: string;
    constructor(n: string) {
        this.myName = n;
    }
    getName() {
        return this.myName
    }
}

class Male extends Person {
    age: number;
    constructor(name: string, age: number) {
        super(name);    //调用父类constructor,并把参数传进去
        this.age = age;
    }
    getName() {     //重写
        return "我叫：" + this.myName
    }
}

let m = new Male('张三', 17);
console.log(m.myName);
console.log(m.age);
console.log(m.getName());
```

```js
//定义类
class class_name { 
    // 类作用域
}

//类继承：TS一次只能继承一个类，不支持继承多个类，但支持多重继承（A 继承 B，B 继承 C）
class child_class_name extends parent_class_name {
    
}
//继承类的方法重写： 类继承后，子类可以对父类的方法重新定义；  方法名相同

//static定义类的数据成员（属性和方法）为静态的，静态成员可以直接通过类名调用

//访问控制修饰符
//类和接口： 类可以实现接口，使用关键字 implements，并将 interest 字段作为类的属性使用
```

##### ==修饰符==

- 访问控制修饰符： 保护对类、变量、方法和构造方法的访问 （访问权限）
  - **public（默认）** : 公有，可以在任何地方被访问。
  - **protected** : 受保护，可以被其自身以及其子类访问。(类和子类里面能访问)
  - **private** : 私有，只能被其定义所在的类访问

##### ==静态属性/成员==

```ts
class Person {
    myName: string;
    static title:string = "title的值";   //静态属性/成员，只能类去用的
    constructor(n: string) {
        this.myName = n;
    }
    getName() {
        return this.myName
    }
}
console.log(Person.title);
Person.title = "修改后的title值";
console.log(Person.title);
```

##### ==抽象类和接口==

```ts
export { }
//抽象类是普通类的描述，指定一个类的规范，给普通类去继承，抽象类不能实例化
// 继承之后，普通类里面必须定义抽象类里面的抽象属性和抽象方法,抽象类里面的普通方法直接继承
abstract class Person {
    abstract name: string;
    abstract getName(): string;
    getAge() {
        return 11
    }
}

class Male extends Person {	//抽象类实现
    name: string = "";
    getName() {
        return this.name
    }
}
```

```ts
//书写接口，给类使用
interface PerItf {
    name: string;
    age?: number;
    getName: () => void;
}
class M implements PerItf {
    name: string = "";
    getName() { };
}
```

##### ==工具类型==

```ts
export { }			//Partial工具类:将< >里的接口类型的属性设置为可缺省属性？
interface PItf {
    name: string;
    age: number
}
//type Partial<T> = { [P in keyof T]?: T[P] | undefined; }
//P类似forin里的临时变量，T的key，即name、age；  能实现可选name? age?
let obj:Partial<PItf> ={
    name: "",
}
```

`let obj:Required<PItf> ={ } 把`<>里的接口类型的属性设置为不可缺省属性

keyof和in  typeof  [TS ](https://www.cnblogs.com/frontvelsun/p/16388240.html)

#### 4、命名空间

```ts
namespace aa { 
   export interface Inf {      }  
   export class Cln {      }  
}
//外部调用命名空间中的类和接口，则需要添加export导出
//在另一个命名空间调用
aa.cln

//如果一个命名空间在一个单独的 TS文件中，使用三斜杠 /// 引用它
/// <reference path = "IShape.ts" /> 
```

#### 5、声明文件

TS引用第三方的 JS库。虽然直接引用可以调用库的类和方法，但是却无法使用TS 类型检查等特性功能。 为了解决这个问题，用声明文件

```ts
//声明文件不包含实现，它只是类型声明;  声明文件以 .d.ts 为后缀; 声明文件或模块的语法:
declare module Module_Name { }
//把声明文件加入到TypeScript中,   TS引入声明文件语法格式
/// <reference path = " runoob.d.ts" />
```



#### 6、模块

```ts
//模块在自身的作用域里执行，并不是在全局作用域
//JavaScript模块加载器是服务于 Node.js 的 CommonJS 和服务于 Web 应用的 Require.js

export interface IShape {}				//模块导出
import shape = require("./IShape")		//模块引入
```







