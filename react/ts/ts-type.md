## ts 学习笔记

### 一．类型定义

#### 1.基本数据类型

const 变量名：类型=初始值；

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/21d1f042-6cda-4641-9288-33e38935db5a)

#### 2.数组

简单数组：const 变量名：类型[]=初始值；

范型数组：const 变量名：类型<任何类型>=初始值；

任何类型：基本类型，对象类型，接口类型等任何类型

简单数组类型和泛型数组类型的主要区别在于它们能够容纳的元素类型的范围。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/5c9025d7-0bad-4c9c-90af-fdd8a1b43e25)

#### 3.元组

元组类型用来表示已知元素数量和类型的数组，各元素的类型不必相同，对应位置的类型需要相同。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/bcc01bd6-47b5-4014-bd46-2191d5d36337)

#### 4.枚举类型

用于定义数值集合。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/bc06450f-f959-47a8-aa0d-d534dd7947c1)

#### 5.返回值类型：

用于标识方法返回值的类型，表示该方法没有返回值。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/82740795-c024-480f-9643-474fb8bdc34d)

#### 6.其他

null:只有一个值的特殊类型,对象缺失值,表示一个空对象引用。typeof(null)==>Object

undefined:初始化变量为一个未定义的值

never:其它类型（包括 null 和 undefined）的子类型，代表从不会出现的值。

### 二．Number 对象与 String 对象

#### 1.number 对像的属性和方法

语法：var num = new Number(value);

属性

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/06472d82-a1e6-48e5-86ce-38bf6c700b46)

方法

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/1467bb7f-3136-4507-9a25-6c301e19df16)

#### 2.String 对象

属性

constructor：对创建该对象的函数的引用。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/5f0de213-74c0-4c35-916c-e57d0d31fb95)

打印结果：

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/c1cfe3d8-1d29-4885-b288-4efaf8a876fd)

方法

![image.png](https://upload-images.jianshu.io/upload_images/29487578-ef9dc51f415fb3e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 三．数组

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/6c8aac51-d0c8-4934-bee6-77d6d18e03e7)

#### 1.Array

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/8a289def-c8e3-43b9-8cf9-162d2fa71cc9)
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/5df2cf39-0c62-44b7-b34c-1b6c8de47e90)
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/0d15fbb5-7a99-4be0-917f-afd6b218db5a)
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/c9dee851-05a6-44db-88c5-b1f291e94f3f)

#### 2.多维数组

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/476e1944-c6fa-414f-931e-608317ddf55f)
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/37552509-c0e9-40c5-880b-725b83f2c721)

#### 4.数组方法

![image.png](https://upload-images.jianshu.io/upload_images/29487578-420dccd2d89cf4cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### （1）数组—>字符串

![image.png](https://upload-images.jianshu.io/upload_images/29487578-5d781387c11a8688.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### （2）every 与 some

相同点：

every 和 some 都有三个参数，即 item-当前项，index-当前项的索引值，array-数组本身；都可循环遍历数组。

不同点：

every：相当于逻辑关系中的且，只有所有参数都满足条件时，才返回 true，一旦有一个不满足，则逻辑中断，返回 false。

some：相当于逻辑关系中的或，只要有一个参数满足条件，就中断遍历，返回 true，若遍历完所有参数，没有符合的项，返回 false。

![image.png](https://upload-images.jianshu.io/upload_images/29487578-cd8e9f4e19cbf3d5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### （3）map 和 forEach

相同点:

(1)都是循环遍历数组中的每一项。

(2)都有三个参数，分别为 item(当前每一项)，index(索引值)，arr(原数组)。

(3)匿名函数中的 this 都是指向 window。

不同点：

(1) map()会分配内存空间存储新数组并返回，forEach()不会返回数据。

(2)forEach 方法没有返回值，是 undefined，不能使用 return，仅用于遍历数组执行操作。

(3)map 方法返回一个新的数组，其中包含对每个元素执行操作后的结果。

(4)map 速度比 foreach 快。

![image.png](https://upload-images.jianshu.io/upload_images/29487578-b47a132d6825673d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### (4)reduce 与 reduceRight

![image.png](https://upload-images.jianshu.io/upload_images/29487578-c877b28403a62c9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### (5)filter

![image.png](https://upload-images.jianshu.io/upload_images/29487578-f10ba1c0d0fe08d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### (6)增删改

![image.png](https://upload-images.jianshu.io/upload_images/29487578-bea4bcf2ca0c67e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
