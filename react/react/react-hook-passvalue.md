### 一.useContext()

context：上下文，用于组件之间的传值

使用流程： 1.先创建 createContex：`const CountContext = createContext(0);`

2.Provider 指定使用的范围：
多个参数可以使用对象{}的形式传递/接收（createContext({})初始化也是对象形式

```
<CountContext.Provider value={count}>
<Counter />
</CountContext.Provider>
```

3.使用 useContext：`const count = useContext(CountContext);`

![image.png](https://upload-images.jianshu.io/upload_images/29487578-54bc9a462e93c11f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 二.useRef()

useRef :返回一个可变的 ref 对象，其  .current  属性被初始化为传入的参数（initialValue）。返回的 ref 对象在组件的整个生命周期内保持不变。
获取 dom 节点:ref.current

##### 1.实现组件传值

![image.png](https://upload-images.jianshu.io/upload_images/29487578-115899ffe1ceaa88.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 2.作为数据载体

![image.png](https://upload-images.jianshu.io/upload_images/29487578-e0b61fbfb310c099.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 3.当点击按钮时，会聚焦并选中输入框的文字

![image.png](https://upload-images.jianshu.io/upload_images/29487578-18ff6606fc425d38.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
