## typeScript 接口

接口是一系列抽象方法的声明，是一些方法特征的集合，这些方法都应该是抽象的，需要由具体的类去实现，然后第三方就可以通过这组抽象方法调用，让具体的类执行具体的方法。
一.ts 接口定义：
interface interface_name {
}

##### 一.ts 接口

定义接口 person

```
interface Person {
    name: string;
    age: number;
    isGril: boolean;
    gride: number[];
    say: () => string;
    run: () => void;
  }
```

定义 student 变量，它的类型是 Person

```
const student: Person = {
    name: "Tom",
    age: 18,
    isGril: false,
    gride: [90, 100, 99, 80],
    say: (): string => {
      return "Hello";
    },
    run: () => {
      console.log("run");
    },
  };
```

customer 实现了接口 Person 的属性和方法

```
 console.log(student.name); //Tom
 console.log(student.age); //18
 console.log(student.gride);//[90, 100, 99, 80]
 console.log(student.isGril);//false
 console.log(student.say()); //Hello
 console.log(student.run()); //run
```

##### 二. 联合类型和接口

```
interface person {
    name: string;
    grade: string[] | string | number | (() => string);
  }
```

值为 string[]时

```
const sd: person = {
    name: "tom",
    grade: ["18", "99", "60"],
  };
  console.log(sd.name + "----" + sd.grade);//tom----18,99,60
```

值为 string 时

```
const sd1: person = {
    name: "tom",
    grade: "100",
  };
  console.log(sd1.name + "----" + sd1.grade);//tom----100
```

值为 number 时

```
const sd2: person = {
    name: "tom",
    grade: 99,
  };
  console.log(sd2.name + "----" + sd2.grade);//tom----99
```

值为(() => string)函数时

```
const sd3: person = {
    name: "tom",
    grade: () => {
      return "88";
    },
  };
  const grade: any = sd3.grade;
  console.log(sd3.name + "----" + grade());//tom----88
```

##### 三.接口和数组

将数组的索引值和元素设置为不同类型，索引值可以是数字或字符串
定义数组类型，index 为 number 型，数组元素是 string 型

```
interface person {
    [index: number]: string;
}
```

```
const list: person = ["a", "b", "c"];
console.log(list[0]);
```

##### 四.接口继承

接口继承就是说接口可以通过其他接口来扩展自己。
Typescript 允许接口继承多个接口。
继承使用关键字 **extends**。

语法：Child_interface_name extends super_interface1_name, …,super_interfaceN_name

1.单继承接口
父接口：

```
interface person {
    age: number;
 }
```

子继承父接口：

```
interface manProps extends person {
    name: string;
}
```

使用继承类型定义变量

```
const man: manProps = {
    age: 18,
    name: "tom",
  };
  console.log(man.name);//tom
```

2.多继承接口
父接口：

```
interface person {
    age: number;
  }
  interface body{
    head:boolean

  }
```

子继承父接口：

```
interface manProps extends person,body {
    name: string;
  }
```

使用继承类型定义变量

```
const man: manProps = {
    age: 18,
    name: "tom",
    head:true
  };
  console.log(man.name);//tom
```
