### 生命周期

#### 1.生命周期函数概念

在组件创建、组件属性更新、组件被销毁的过程中，总是伴随着各种各样的函数执行，这些在组件特定时期，被触发执行的函数。

#### 2.生命周期三个阶段

（1）加载阶段（Mount）：在组件初始化时执行，有一个显著的特点：创建阶段生命周期函数在组件的一辈子中**只执行一次**；

执行顺序：constructor->componentWillMount->render->componentDidMount

（2）更新阶段（Update）：根据组件的属性（state）和状态(props)改变时执行，有选择性的触发 0 次或多次；

执行顺序:componentWillReceiveProps->shouldComponentUpdate->
componentWillUpdate->render->componentDidUpdate

（3）卸载阶段（Unmount）：在组件对象销毁时执行，一辈子**只执行一次**；

#### 3.生命周期函数

![image.png](https://upload-images.jianshu.io/upload_images/29487578-687f7a434941d45e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 总结：

useEffect(()=>{}):mount+update

useEffect(()=>{},[]):mount

useEffect(()=>{},[deps]):mount+update(根据 deps 变化而 update 的)
