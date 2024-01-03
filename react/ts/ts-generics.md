## 一.泛型

泛型 ：是一种编程语言特性，允许在定义函数、类、接口等时使用占位符来表示类型（可以表示任意类型）。是可重用、灵活且类型安全的代码时非常有用的功能。

使用目的：为了处理不特定类型的数据，使得代码可以适用于多种数据类型而不失去类型检查。

优势：
代码重用： 可以编写与特定类型无关的通用代码，提高代码的复用性。
类型安全： 在编译时进行类型检查，避免在运行时出现类型错误。
抽象性： 允许编写更抽象和通用的代码，适应不同的数据类型和数据结构。

#### 1.泛型标识符

使用约定俗成的标识符，比如常见的 T（表示 Type）、U、V 等，但实际上你可以使用任何标识符。关键是使得代码易读和易于理解，在泛型类型参数上使用描述性的名称，以便于理解其用途。

T: 代表 "Type"，泛型类型参数名

```
const identity: <T>(arg: T) => T = (arg) => {return arg};
console.log(identity(123));//123
console.log(identity(true));//true
console.log(identity("test"));//test
console.log(identity([1, 2, 3, 4])); // [1, 2, 3, 4]
```

K, V: 用于表示键（Key）和值（Value）的泛型类型参数。

```
interface IKeyValueProps<K, V> {
    key: K;
    value: V;
  }
```

E: 用于表示数组元素的泛型类型参数。

```
const printArray: <E>(arr: E[]) => void = (arr) => {
    arr.forEach((item) => console.log(item));
};
  console.log(["a", "b", "c"]);//['a', 'b', 'c']
  console.log([1, 2, 3, 4]);//[1, 2, 3, 4]
```

U, V,···: 通常用于表示第二、第三个、第 n 个泛型类型参数。

```
 const comb: <U, V>(first: U, second: V) => string = (first, second) => {
    return `${first} ${second}`;
  };
  console.log(comb(1, 2));//1  2
```

#### 2.泛型函数

泛型函数可以处理不同类型的函数

定义泛型函数：

```
const identity: <T>(arg: T) => T = (arg) => {return arg};
```

使用泛型函数：

```
const result = identity<string>("Hello");
  console.log(result); //  Hello
  const numberResult = identity<number>(42);
  console.log(numberResult); // 42
```

#### 3. 泛型接口

使用泛型来定义接口，使接口的成员能够使用任意类型。

定义泛型接口：

```
interface IKeyValueProps<K, V> {
    key: K;
    value: V;
  }
```

使用泛型接口：

```
  const kv: IKeyValueProps<number, string> = { key: 1, value: "abc" };
  console.log(kv);//{key:1,value:"abc"}
```

#### 4. 泛型类

泛型也可以应用于类的实例变量和方法

定义泛型类：

```
class box<T> {
    private value: T;
    constructor(value: T) {
      this.value = value;
    }
    getValue(): T {
      return this.value;
    }
  }
```

使用泛型类：

```
 const boxT = new box<string>("abc");
  console.log(boxT.getValue());
```

#### 5. 泛型约束

限制泛型的类型范围.

定义约束接口：

```
interface IlengthProps {
    length: number;
  }
```

使用约束接口：

```
const logLength = <T extends IlengthProps>(arg: T): void => {
    console.log(arg.length);
  };
  logLength("hellow");
```

#### 6. 泛型与默认值

可以给泛型设置默认值，使得在不指定类型参数时能够使用默认类型。

```
const defValue: <T = string>(arg: T) => T = (arg) => {
    return arg;
  };
  console.log(typeof defValue("hello"), typeof defValue(42));//string number
```
