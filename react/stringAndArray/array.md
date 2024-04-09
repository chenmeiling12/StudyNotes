### 数组的方法

#### 1.定义一个数组：

```
const arr = [1, 2, 3, 4, 5, 6];
```

#### 2.数组常用的方法

##### 改变原数组

在数组末尾添加数据：` arr.push(item)`

```
 arr.push(arrItem); //[1,2,3,4,5,6,7]
```

在数组头部添加数据：` arr.unshift(item)`

```
 arr.unshift(arrItem);//[7,1,2,3,4,5,6]
```

刪除数组最后一项：` arr.pop()`

```
arr.pop();//[1,2,3,4,5]
```

删除数组的第一项：` arr.shift()`

```
arr.shift();// [2, 3, 4, 5, 6]
```

翻转数组：`arr.reverse() `

```
arr.reverse();//[6,5,4,3,2,1]
```

正序排序：

```
 arr.sort(function (a, b) {
    return a - b;
  })
```

反序排序：

```
 arr.sort(function (a, b) {
    return b - a;
  });
```

位排序（会将数组元素转化成字符串，然后按照 unicode 字符顺序排序）[1, 2, 12, 8, 3, 4, 5, 6]=>[1, 12, 2, 3, 4, 5, 6, 8]

```
 arr.sort()
```

截取，原数组的话是[1,2,5,6];返回新数组，第一个参数是开始截取的索引，第二个参数是截取的个数,[3,4]:`arr.splice(start, num) `

```
  arr.splice(2, 2)
```

插入/更新，原数组[1,2,8,5,6]第一个参数是开始截取的索引，第二个参数是截取的个数,第三个参数是插入的值；新数组：[8,5]:`arr.splice(start, num,value)`

```
 arr.splice(2, 2, 8);
```

#### 不改变原数组

合并数组：`arr.concat(arrNew)`

```
 const arr0 = [7, 8, 9];
  console.log(arr.concat(arr0));//[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

string=>array,通过指定字符把数组转化成字符串:`arr.join(char)`

```
 console.log(arr.join("+"));//1+2+3+4+5+6
```

[3,4,5]截取一段数组，第一个参数是开始截取索引，第二个是结束截取索引（不包含）:`arr.slice(start,end)`

```
 console.log(arr.slice(2, 5));//[3,4,5]
```

判断数组是否含有该值，含有则返回第一次出现该值的索引，否则返回-1:`arr.indexOf(char)`

```
 console.log(arr.indexOf(0));//-1
```

判断数组是否含有该值，含有则返回最后一次出现该值的索引，否则返回-1:`arr.lastIndexOf(char)`

```
 console.log(arr.lastIndexOf(5));//4
```

#### es6

相当于 for,循环遍历数组，没有 return,item:每一项，index:索引，arr:原数组:`arr.forEach()`

```
arr.forEach((item, index, arr) => {
    console.log(item, index, arr);
  });
```

映射数组,映射出一个加工过的数组，item：每一项，index:索引，arr:原数组:`arr.map()`

```
const a = arr.map((item, index, arr) => {
    return item + 5;
  });
  console.log(a); //[6, 7, 8, 9, 10, 11]
```

过滤出符合条件的数组，item：每一项，index:索引，arr:原数组:`arr.filter()`

```
const filter = arr.filter((item, index, arr) => {
    return item > 3;
  });
  console.log(filter);// [4, 5, 6]
```

判断数组是否满足所有条件,全部满足的话返回 true，否则返回 false:`arr.every()`

```
 const every = arr.every((item, index, arr) => {
    return item > 2;
  });
  console.log(every);//false
```

判断是否有满足条件的，有的话返回 true，否则返回 false:`arr.some()`

```
 const some = arr.some((item, index, arr) => {
    return item > 2;
  });
  console.log(some);//true
```

返回第一个满足条件的值:`arr.find()`

```
 const find = arr.find((item, index, arr) => {
    return item > 2;
  });
  console.log(find); //3
```

叠加数组每一项，pre：初始值，item：每一项，index:索引，arr:原数组:`arr.reduce()`

```
 const reduce = arr.reduce((pre, item,index,arr) => {
    return (pre += item);
  });
  console.log(reduce);//21
```
