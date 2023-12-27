### 一. React.memo()

#### 1.组件渲染存在的问题：

在 React 的渲染流程中，一般来说，父组件的某个状态发生改变，那么父组件和父组件所使用的所有子组件，都会强制渲染。

![image.png](https://upload-images.jianshu.io/upload_images/29487578-bc68ce7574399d6b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

每点击一次 add,num 状态会改变，则会重新渲染父组件及其一下的子组件。

![image.png](https://upload-images.jianshu.io/upload_images/29487578-d2179303f041065e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2 .解决以上问题：

在子组件上加上 React.memo()

![image.png](https://upload-images.jianshu.io/upload_images/29487578-a1bb5d274c95bc90.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

当父组件状态改变时，只渲染父组件，子组件不会做无关的刷新，从而达到了性能优化的目的

![image.png](https://upload-images.jianshu.io/upload_images/29487578-e0dc5b71f7f1b84c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3.使用 React.memo()存在问题：

memo 对于新旧 props 的比较是浅比较，当一个引用类型的 props 改变时，只要它的地址没有发生改变，就算 props 中某一项数据发生了改变，被 memo 包裹的组件也不会重新渲染

![image.png](https://upload-images.jianshu.io/upload_images/29487578-b053ed2381314fec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

运行结果：
点击 addNum 按钮 n 次之后
页面（子组件）：1 2 3 4
浏览器：打印出 n 个 1 2 3 4

##### 总结：

（1）父组件重新渲染，没有被 memo 包裹的子组件也会重新渲染。

（2）被 memo 包裹的组件只会对新旧 props 做浅比较，对于引用类型的数据如果发生了更改，需要返回一个新的地址，才会重新渲染。

（3）memo 并不是用的越多越好，因为缓存本身也是需要开销的。如果每一个组件都用 memo 去包裹一下，那么对浏览器的开销就会很大

（4）项目中可以针对刷新频率高的组件，根据实际情况，使用 memo 进行优化

### 二．useMemo()

useMemo():它可以缓存一个结果，当这个缓存结果不变时，可以借此来进行性能优化。

#### 1 .使用 useMemo 缓存:多次点击只打印一次

![image.png](https://upload-images.jianshu.io/upload_images/29487578-a231ce118f999581.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/29487578-1345914e74e70486.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2. 如果使用 useMemo(()=>{},[deps])绑定 deps,当 deps 变化时才会重新渲染。

![image.png](https://upload-images.jianshu.io/upload_images/29487578-93979baa9f1bb35f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3.不使用 useMemo 缓存，每次点击都重新渲染

![image.png](https://upload-images.jianshu.io/upload_images/29487578-ddcd3e87c239b71b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/29487578-016c81e929294354.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 总结：

(1)useMome(()=>{},[]):执行了 callback 后，返回一个结果，这个结果就会被缓存起来

(2)useMome(()=>{},[deps]): deps 依赖发生改变的时候，会重新执行 callback 计算并返回最新的结果，否则就使用缓存的结果

(3)useMemo 是对计算的结果进行缓存，当缓存结果不变时，会使用缓存结果（计算属性）

(4)useMemo 并不是用的越多越好，对于耗时长、性能开销大的地方，可以使用 useMemo 来优化，但大多数情况下，计算结果的开销还没有使用 useMemo 的开销大，应视情况而定

### 三．useCallback()

useCallback ():会把传入的 callback 缓存起来。当 deps 依赖发生改变的时候，会重新缓存最新的 callback ，否则就使用缓存的结果

点击了三次，使用 useCallback 对函数进行缓存，因此不会重新渲染

![image.png](https://upload-images.jianshu.io/upload_images/29487578-64370c79744201d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/29487578-618494b01245f75e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 总结：

(1)useCallback 与 useMemo 类似，是对函数进行缓存

(2)useCallback 可以单独使用，但是单独使用的使用对性能优化并没有实质的提升，且父组件此时重新渲染，子组件同样会渲染。

(3)配合 memo 一起使用，这样当父组件重新渲染时，缓存的函数的地址不会发生改变，memo 浅比较会认为 props 没有改变，因此子组件不会重新渲染。
