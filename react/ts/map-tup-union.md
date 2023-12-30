## 一. Map对象
Map 对象保存键值对，并且能够记住键的原始插入顺序。任何值(对象或者原始值) 都可以作为一个键或一个值。

### 1. 创建对象
```
const obj = new Map()
```

### 2.Map对象属性与函数
######  设置键值对，返回该 Map 对象。
```
obj.set("a", 1)
obj.set(1, 1)
console.log(obj)// {'a' => 1, 1 => 1}
```

######  查找。返回键对应的值，如果不存在，则返回 undefined
```
 console.log(obj.get("a"))//1
```

######  判断是否存在。返回布尔值，用于判断 Map 中是否包含键对应的值。
```
console.log(obj.has("a"))//true
```

######  返回 Map 对象键/值对的数量
```
  console.log(obj.size)//2
```

######  包含了 Map 对象中每个元素的键 。
```
 console.log(obj.keys())//{'a', 1}
```

######  包含了Map对象中每个元素的值
```
console.log(obj.values())//{1, 1}
```

######  移除 Map 对象的所有键/值对 。
```
console.log(obj.clear())//undefine
```

### 3. 迭代
######  迭代key
```
for (let key of obj.keys()) {
    console.log(key)//a 1
  }
```

######  迭代 value
```
for (let val of obj.values()) {
    console.log(val)//1 1
  }
```
######  迭代 key => value
```
  for (let entry of obj.entries()) {
    console.log(entry[0], entry[1]);  //a  1 
  }                                   //1  1
```

######  使用对象解析
```
  for (let [key, value] of obj) {
    console.log(key, value);       //a  1 
  }                                //1  1
```

## 二.元组(any[])
组中允许存储不同类型的元素，元组可以作为参数传递给函数。

### 1.元组声明
```
const tuple=[10,"aa",true,[1,2,3],{a:1,b:'9'}]
或
const tuple=[]
tuple[0]=10
tuple[1]="aa"
```

### 2.元组的属性和方法
###### 获取元组的中某一项的元素
```
 console.log(tuple[1])
```

######  获取元组的长度
```
console.log(tuple.length)  //5
```

######  添加元素在元组最后面,且返回元组的长度
```
console.log(tuple.push(0))//6
```

######  删除元组最后的一个元素,且返回被删除的元素
```
console.log(tuple.pop())//{a:1,b:'9'}
```

######  更新元组
```
tuple[0]=123
console.log(tuple)
```

######  解构元素
```
const [a,b]=tuple
console.log(a)//10
console.log(b)//aa

const [c,...d]=tuple
console.log(c)//10
console.log(d)//["aa",true,[1,2,3],{a:1,b:'9'}]
```

## 三 .联合类型
联合类型可以通过管道(|)将变量设置多种类型，赋值时要根据设置的类型来赋值.
语法格式：Type1|Type2|Type3 

######  1.声明联合类型变量
注意：不能使用const
```
let type:number|string
type=1
type="a"
```

######  2.声明联合类型数组
```
let arr:number[]|string[]; 
arr=[1,2,3]
arr=["a","b","c"]
```

######  3.联合类型当数组使用
```
const typeFun=(name:string|string[])=>{
  if(typeof name=="string"){
    console.log(name)
  }else{
    name.map((item:string,index:number)=>{
      console.log(name[index])
    })
  }
}
typeFun("tom")
或
typeFun(["tom","linda"])
```