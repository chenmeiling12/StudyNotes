### 一.es6 let 与 const

- let 声明的变量只在 let 命令所在的代码块内有效。
- const 声明一个只读的常量，一旦声明，常量的值就不能改变。

##### 1.代码块内有效

let 和 const 是在代码块内有效，var 是在全局范围内有效

```
if (true) {
    var a = 0;
    let b = 1;
    const c = 2;
    console.log(a); //0
    console.log(b); //1
    console.log(c); //2
  }
  console.log("a:" + a); //b:1
  // console.log(b); //ReferenceError: b is not defined
  console.log(c); //ReferenceError: c is not defined
```

##### 2.不能重复声明

var 可以声明多次,let 和 const 只能声明一次
let 适用于计数器

```
var a = 0;
  var a = 4;
  let b = 1;
  let b = 5;
  const c = 2;
  const c = 5;
  console.log(a); //4
  console.log(b); //Identifier 'b' has already been declared.
  console.log(c); //Identifier 'c' has already been declared.
```

##### 3.不存在变量提升

var 会变量提升,let 和 const 不存在变量提升

```
console.log("a:" + a); //a:undefined
console.log("b:" + b); // ReferenceError: Cannot access 'b' before initialization
console.log("c:" + c); // ReferenceError: Cannot access 'c' before initialization
var a = 0;
let b = 1;
const c = 2;
```

##### 4 .const

const 声明一个只读变量，声明之后不允许改变。意味着，一旦声明必须初始化，否则会报错。

注意：_const 不允许改变不是指变量的值不变，而是动变量指向的内存地址所保存的数据不允许改动。_
_简单类型：值就保存在变量指向的那个内存地址，等同于常量。_
_复杂类型：变量指向的内存地址其实是保存了一个指向实际数据的指针， c 只能保证指针是固定的，无法控制数据结构变化。_

```
const c ;// Missing initializer in const declaration.
```

### 二.解构赋值

解构赋值是对赋值运算符的扩展。是一种针对数组或者对象进行模式匹配，然后对其中的变量进行赋值。

解构模型：
![image.png](https://upload-images.jianshu.io/upload_images/29487578-23371a8468cfdbd9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 1.数组解构模型

######（1）基本

```
constlet [a, b, c] = [1, 2, 3];
console.log(a);//1
console.log(b);//2
console.log(c);//3
```

######（2）可嵌套

```
  const [a, [[b], c]] = [1, [[2], 3]];
  console.log(a); //1
  console.log(b); //2
  console.log(c); //3
```

######（3）可忽略

```
const [a, , b] = [1, 2, 3];
console.log(a); //1
console.log(b); //3
```

######（4）不完全解构

```
const [a = 1, b] = [];
console.log(a); //1
console.log(b); //undefined
```

######（5）剩余运算符

```
const [a, ...b] = [1, 2, 3];
console.log(a); //1
console.log(b); //[2，3]
```

######（6）字符串等

```
  const [a, b, c, d, e] = "hello";
  console.log(a); //h
  console.log(b); //e
  console.log(c); //l
  console.log(d); //l
  console.log(e); //o
```

######（7）解构默认值
当解构模式没有匹配结果时，直接使用默认值作为返回结果；当有匹配结果，且匹配结果是 undefined 时，会触发默认值作为返回结果。

```
  const [a = 2] = [undefined];
  console.log(a); //2
```

```
  const [a = 3, b = a] = [1];
  console.log(a); //1
  console.log(b); //1
```

```
   const [a = 3, b = a] = [1, 2];
  console.log(a); //1
  console.log(b); //2
```

##### 2.对象模型解构

###### （1）基本

```
  const { foo, bar } = { foo: "aaa", bar: "bbb" };
  console.log(foo); //aaa
  console.log(bar); //bbb
```

```
  const { baz: foo } = { baz: "ddd" };
  console.log(foo); //ddd
```

###### (2)可嵌套可忽略

```
 const obj = {
    p: ["hello", { y: "world" }]
  };
  const {
    p: [x, { y }],
  } = obj;
  console.log(x); //hello
  console.log(y); //world
```

```
 const obj = {
    p: ["hello", { y: "world" }],
  };
  const {
    p: [x, {}],
  } = obj;
  console.log(x); //hello
```

###### (3)不完全解构

```
  const obj = {
    p: [{ y: "world" }]
  };
  const {
    p: [{ y }, x],
  } = obj;
  console.log(x); //undefined
  console.log(y); //world
```

###### (4)剩余运算符

```
  const { a, b, ...rest } = { a: 10, b: 20, c: 30, d: 40 };
  console.log(a); //10
  console.log(b); //20
  console.log(rest); //{c: 30, d: 40 }
```

###### (5)解构默认值

```
  const { a = 10, b = 5 } = { a: 3 };
  console.log(a); //3
  console.log(b); //5
```

```
  const { a: aa = 10, b: bb = 5 } = { a: 3 };
  console.log(aa); //3
  console.log(bb); //5
```

### 三.Symbol

Symbol 是原始数据类型。表示独一无二的值，最大的用法是用来定义对象的唯一属性名。

##### 1.基本用法

不能用 new 命令,可接受一个字符串作为参数，为新创建的 Symbol 提供描述，用来显示在控制台或者作为字符串的时候使用，便于区分。

```
  const sy = Symbol("KK");
  console.log(sy); // Symbol(KK)
  console.log(typeof sy); // symbol

  // 相同参数 Symbol() 返回的值不相等
  let sy1 = Symbol("kk");
  console.log(sy === sy1);//false
```

##### 2.使用场景

###### （1）作为属性名

每一个 Symbol 的值都是不相等的，所以 Symbol 作为对象的属性名，可以保证属性不重名。
写法一：
\*Symbol 作为对象属性名时不能用.运算符，要用方括号。因为.运算符后面是字符串，所以取到的是字符串 sy 属性，而不是 Symbol 值 sy 属性。

```
  const sy = Symbol("key1");
  const syObject = {};
  syObject[sy] = "kk";
  console.log(syObject); // {Symbol(key1): "kk"}
```

写法二：

```
  const sy = Symbol("key1");
  const syObject = {
    [sy]: "kk",
  };
  console.log(syObject); // {Symbol(key1): "kk"}
```

写法三：

```
  const sy = Symbol("key1");
  const syObject = {};
  Object.defineProperty(syObject, sy, { value: "kk" });
  console.log(syObject); // {Symbol(key1): "kk"}
```

注意：

- Symbol 值作为属性名时，该属性是公有属性，可以在类的外部访问。
- for...in 、 for...of 、Object.keys() 、 Object.getOwnPropertyNames() 中无输出值。
- 通过 Object.getOwnPropertySymbols() 和 Reflect.ownKeys() 可读取到一个对象的 Symbol 属性。

###### （2）定义常量

使用 Symbol 定义常量，这可以保证这一组常量的值都不相等。

```
const COLOR_RED = Symbol("red");
const COLOR_YELLOW = Symbol("yellow");
const COLOR_BLUE = Symbol("blue");
```

###### （3）Symbol.for()

Symbol.for() 类似单例模式，首先会在全局搜索被登记的 Symbol 中是否有该字符串参数作为名称的 Symbol 值，如果有即返回该 Symbol 值，若没有则新建并返回一个以该字符串参数为名称的 Symbol 值，并登记在全局环境中供搜索。

```
  const yellow = Symbol("Yellow");
  const yellow1 = Symbol.for("Yellow");
  console.log(yellow === yellow1); // false
  const yellow2 = Symbol.for("Yellow");
  console.log(yellow1 === yellow2); // true
```

###### （4）Symbol.keyFor()

Symbol.keyFor() 返回一个已登记的 Symbol 类型值的 key ，用来检测该字符串参数作为名称的 Symbol 值是否已被登记。

```
 const yellow1 = Symbol.for("Yellow");
 console.log(Symbol.keyFor(yellow1)); // Yellow
```

### 四.Map 与 Set

#### (一)Map 对象

Map 对象保存键值对。键和值都可以是任意值(对象或者原始值) 。

###### Maps 和 Objects 的区别：

- Object 的键只能是字符串/ Symbols，Map 的键可以是任意值。
- Map 中的键值是有序的（FIFO 原则），而添加到对象中的键则不是。
- Map 的键值对个数可以从 size 属性获取，而 Object 的键值对个数只能手动计算。
- Object 都有自己的原型，原型链上的键名可能和自己在对象上的设置的键名产生冲突。

##### 1.key

总结：

- 初始化 map 对象： const map = new Map();
- 向 map 对象添加键值对：map.set(key, value);
- 获取值：map.get(key)

###### (1)key 是字符串

```
  const myMap = new Map();
  const keyString = "a string"; //键
  myMap.set(keyString, "和键'a string'关联的值"); //设置键和值
  console.log(myMap.get(keyString)); // 值
  console.log(myMap.get("a string")); //值
  console.log(myMap);// {key: "a string". value: "和键'a string'关联的值}
```

###### (2)key 是对象

```
 var myMap = new Map();
  var keyObj = {};
  myMap.set(keyObj, "和键 keyObj 关联的值");//设置key
  console.log(myMap.get(keyObj)); // 和键 keyObj 关联的值
  console.log(myMap.get({})); // undefined, 因为 keyObj !== {}
  console.log(myMap);//{key: {}  value : "和键 keyObj 关联的值"}
```

###### (3)key 是函数

```
  const myMap = new Map();
  const keyString = "a string"; //键
  myMap.set(keyString, "和键'a string'关联的值"); //设置键和值

  console.log(myMap.get(keyString)); // 值
  console.log(myMap.get("a string")); //值
  console.log(myMap);// {'a string' => "和键'a string'关联的值"}
```

###### (4)key 是 NaN

NaN 作为 Map 的键来说是没有区别的

```
  var myMap = new Map();
  myMap.set(0, "zero");
  myMap.set(1, "one");
  const myMap = new Map();
  myMap.set(NaN, "not a number");
  console.log(myMap.get(NaN)); // not a number
```

##### 2.Map 的迭代

###### （1）for...of

遍历 key-value

```
  for (var [key, value] of myMap) {
    console.log(key + " = " + value); //0 = zero   1 = one
  }
或
  for (var [key, value] of myMap.entries()) {
    console.log(key + " = " + value);//0 = zero   1 = one
  }
```

遍历 key

```
  for (var key of myMap.keys()) {
    console.log(key);//0  1
  }
```

遍历 value

```
for (var value of myMap.values()) {
    console.log(value);
  }
```

###### （2）forEach()

```
 myMap.forEach((value, key) => {
    console.log(key + " = " + value);//0 = zero  1 = one
  }, myMap);
```

##### 3.Map 对象的操作

###### （1）map 与 array 的转换

Map 构造函数可以将一个 二维 键值对数组转换成一个 Map 对象

```
 var kvArray = [
    ["key1", "value1"],
    ["key2", "value2"],
  ];
//Array -> Map
  const myMap = new Map(kvArray);
  console.log(myMap); //{key:"key1"  value:"value1"}
//map -> array
  const outArray = Array.from(myMap);
  console.log(outArray);//[["key1", "value1"],["key2", "value2"] ];
```

###### (2)Map 的克隆

Map 对象构造函数生成实例，迭代出新的对象。

```
  var myMap1 = new Map([
    ["key1", "value1"],
    ["key2", "value2"],
  ]);
  var myMap2 = new Map(myMap1);
  console.log(myMap1 === myMap2);//false
```

###### (3)Map 的合并

合并两个 Map 对象时，如果有重复的键值，则后面的会覆盖前面的

```
  const myMap1 = new Map([
    [1, "one"],
    [2, "two"],
    [3, "three"],
  ]);
  const myMap2 = new Map([
    [1, "uno"],
    [2, "dos"],
  ]);
  const merged = new Map([...myMap1, ...myMap2]);
  console.log(merged);//[{key:1,value:"uno"},{key:2,value:"dos"},,{key:1,value:three"},]
```

#### (二)Set 对象

- Set 对象可存储任何类型的唯一值（原始值/对象引用）。
- Set 对象存储的值总是唯一的，所以需要判断两个值是否恒等。有几个特殊值需要特殊对待。
- Set 对象 存储对象时之间引用不同不恒等，即使值相同，Set 也能存储。

###### Set 中的特殊值：

- +0 与 -0 在存储判断唯一性的时候是恒等的，所以不重复；
- undefined 与 undefined 是恒等的，所以不重复；
- NaN 与 NaN 是不恒等的，但是在 Set 中只能存一个，不重复。

##### 1.Set 对象的存储

```
  const mySet = new Set();
  mySet.add(1); // Set(1) {1}
  mySet.add(5); // Set(2) {1, 5}
  mySet.add(5); // Set(2) {1, 5}  值的唯一性
  mySet.add("some text")// {1, 5, "some text"} 类型的多样性

  //对象之间引用不同不恒等，即使值相同，Set 也能存储
  var o = { a: 1, b: 2 };
  mySet.add(o);
  mySet.add({ a: 1, b: 2 });
  console.log(mySet); // {1, 5, "some text", { a: 1, b: 2 }, { a: 1, b: 2 }}
```

##### 2.类型转换

###### (1)Array<——>Set

```
  // Array -> Set
  const mySet = new Set(["value1", "value2", "value3"]);
  console.log(mySet); //Set(3) {'value1', 'value2', 'value3'}

  //将 Set -> Array
  const myArray = [...mySet];
  console.log(myArray); //['value1', 'value2', 'value3']
```

###### (2)String->Set

```
  const mySet = new Set("hello");
  console.log(mySet); //Set(4) {'h', 'e', 'l', 'o'}
```

##### 3.Set 对象作用

###### (1)数组去重

```
  const mySet = new Set([4, 4, 3, 1, 2, 3, 3]);
  console.log([...mySet]); // [4, 3, 1, 2]
```

###### (2)并集

两个 Set 对象合并时，如果匹配到已存在的数据，会自动忽略。

```
   const a = new Set([1, 2, 3]);
  const b = new Set([4, 3, 2]);
  const union = new Set([...a, ...b]);
  console.log(union);//{1, 2, 3, 4}
```

###### (1)并集

取两个 Set 的相同值

```
  const a = new Set([1, 2, 3]);
  const b = new Set([4, 3, 2])
  const intersect = new Set([...a].filter((x) => b.has(x)));
  console.log(intersect); //Set(2) {2, 3}
```

###### (1)差集

在 a 中，不存在 b 中的值的集合

```
  const a = new Set([1, 2, 3]);
  const b = new Set([4, 3, 2]);
  const difference = new Set([...a].filter((x) => !b.has(x)));
  console.log(difference);//Set(1) {1}
```
