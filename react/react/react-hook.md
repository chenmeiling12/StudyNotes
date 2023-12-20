## react hooks

#### 1 useState()：状态钩子

该函数返回一个数组，由两个值组成。

state：是变量，指向状态的当前值；

setState：是函数，用来更新状态，约定是 set 前缀加上状态的变量名；

initDate：是 state 初始化的值。它可以是任何类型的值，但对于函数有特殊的行为。在初始渲染后，此参数将被忽略。

##### 总结：

引入 import { useState } from "react";

初始化：const [state, setState] = useState(initDate);

使用：{state}

修改：setState("click you")

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/c9c09c10-8fc7-461f-8a49-732fd09f5e98)

#### 2 useEffect(callback):生命周期钩子

useEffect 用于处理组件中的 effect，通常用于请求数据，事件处理，订阅等相关操作。

##### (1)用法：没有设置依赖：useEffect(callback)

##### 作用：

函数式组件第一次渲染完毕后，执行 useEffect 中的 callback 回调函数，等价于 vue 组件中的 mounted；

在组件每一次更新完毕后，也会执行 useEffect 中的 callback 回调函数，等价于 vue 组件中的 updated。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/559f4a9f-b3ff-4e9c-916c-e70360a1d182)
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/40789eb8-9e1a-4816-8a28-6c8eb6cb9a48)

##### (2)设置但没有依赖项：useEffect（(callback, [ ])）

##### 作用：

函数式组件只有第一次渲染完后执行 callback，后面视图更新，callback 都不再执行，类似于 vue 组件的 Mounted(只渲染一次)。
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/8f5f7935-49d1-4142-a255-5cb3a7419e33)
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/368da2fb-41b6-4851-b1cf-af96edcc27f5)

##### (3)设置并有依赖：useEffect（callback, [依赖的状态(可以有多个状态)]）

##### 作用：

函数式组件第一次渲染后会执行 callback；

当依赖的状态值(或者多个依赖状态中的一个)发生改变，也会触发 callback 执行；

依赖的状态如果没有变化，在组件更新的时候，callback 不会执行。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/a1b1523e-e7c3-46f4-b5df-08edce9d5656)

###### 注意：当 num 变量的值发生变化时，会值行 callback；当 count 变量的值发生变化时，只有初次渲染时会执行 callback，后面变化就不会再执行了

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/cf0cf1c7-cbe2-4528-9a1a-32581bdd7086)

###### 注意：当 num 变量或 count 变量的其中任何一个值发生变化时，都会执行 callback；

###### 注意：只有依赖值发生变化时，才会执行 callback，即使组件更新，依赖值没变的话依旧不会执行 callback。

#####（4）返回函数：useEffect(() => {return () => {}},[依赖项])}

##### 作用：初次渲染不会执行 return 函数

如果依赖值为空，不会执行；

如果存在依赖，依赖的状态发生改变后，组件更新，会把上一次返回的函数执行。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/6caf1aac-d86f-4190-9a67-c0514ed08a06)

##### 注意事项

useEffect 必须在函数的最外层上下文中调用，不能把其嵌入到条件判断、循环等操作语句中

useEffect 只能是一个同步函数，不能使用 async

### 其他

#### 页面与逻辑分开

在当前页面的文件夹下新建一个 hook.ts 文件

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/a339800a-ea01-460d-b1e2-3543e56b60cc)

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/e65553f2-0145-4c65-b97f-697ca83a5c82)
