### 1.使用 SortableJS 实现同一层列表拖拽

##### （1）写法一：使用配置项

注意：使用 option 配置时，ReactSortable 里没有 plugins 属性 会报 ts 错误，所以要用@ts-ignore 避开了 ts 机制

![image.png](https://upload-images.jianshu.io/upload_images/29487578-92414bc519aa922b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### （2）写法二：使用 new

![image.png](https://upload-images.jianshu.io/upload_images/29487578-2216ca5b0a5941b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### （3）写法三：自定义组件

当在 prop 中使用自定义组件时 tag，它唯一允许的组件是一个 forwardRef 组件

![image.png](https://upload-images.jianshu.io/upload_images/29487578-fc69c25ce0060e4e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 常用的配置项：

```
draggable: ".item",  // 允许拖拽的项目类名；
delay: 0,// 定义鼠标选中列表单元可以开始拖动的延迟时间；
animation: 150,//排序动画的时间；
handle: ".className",//指定可拖拽的元素，.className是类名；
filter: ".className",  // 过滤器，不需要进行拖动的元素；
draggable: ".className"//允许拖拽的项目类名；
chosenClass: ".className",  // 被选中项的 类名;
dragClass: ".className",  // 正在被拖拽中的类名;
touchStartThreshold: 0,//取消延迟拖动事件之前，点应该移动多少px;
invertSwap: false,//是否始终使用反向交换区域
```
