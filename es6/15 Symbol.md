# Symbol数据类型

## 1.Symbol数据类型介绍
- 在JavaScript中，有6中数据类型，分别是：String，Number，Object，Boolean，Null，Undefined
- Es6中添加了一种全新的数据类型，Symbol。
- 作用：解决对象的属性名冲突
## 2.Symbol使用方法
```JavaScript
let name = Symbol();
let person = {
  [name]:"张三"
};
console.log(person[name]) 
//console.log(person.name)
```

- 当Symbol值作为对象属性名的时候，不能用点运算符获取对应的值，需要用[]，例如以下代码：
```JS
let name = Symbol();
let person = {};

person.name;   //undefined
person['name'];//张三
person.name;  //张三
```
## 3.属性遍历
- 当Symbol类型的值作为属性名的时候，该属性不会出现在for...in和for...of中，也不会被Object.keys()获取到
- 如果要获取，有两种方法：
  - 1.使用Object.getOwnPropertySymbols(),它会找到Symbol类型的属性并返回一个数组，数组的成员就是Symbol类型的属性值
  ```JS
  let name = Symbol("name");
  let age = Symbol("age");

  let person = {
    [name]:"张三",
    [age]:"12"
  };
  Object.getOwnPropertySymbols(person);
  //结果:[Symbol(name),Symbol(age)]
  ```
  - 2.使用Reflect.ownKeys()，可以一次性获取所有7中类型
  ```JS
  let person = {
    [Symbol('name')]:"张三",
    "age":21
  };
  Reflect.ownKeys(person);
  //结果:["age",Symbol(name)]
  ```
  - 3.使用Symbol.for()，能够根据参数名，去__全局环境__中搜索是否有以该参数名来创建一个新的Symbol值，有就返回，没有就以参数名来创建一个新的Symbol值
  ```JS
  let n1 = Symbol.for('name')
  let n2 = Symbol.for('name')
  console.log(n1===n2);
  //结果：true
  ```
  注意这里使用Symbol.for创建的Symbol值，如果使用Symbol()去创建，它不会被登记在全局环境中，所以使用在使用Symbol.fot()是得不到的
  ```JS
  let n1 = Symbol('name');
  let n2 = Symbol.for('name');
  console.log(n1===n2);
  //结果:false
  ```
  - 4.使用Symbol.keyFor()，返回一个被登记在__全局环境__中Symbol值的key，没有就返回undefined。注意由于被登记在全局环境中，所以这里的Symbol值要用Symbol.for()创建
  ```JS
  let n1 = Symbol.for('name');
  Symbol.keyFor(n1)
  //"name"
  ```
