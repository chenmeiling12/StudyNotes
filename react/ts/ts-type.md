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





