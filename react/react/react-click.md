### 一.添加事件处理函数  

```
<button onClick={handClick} >点击</button>
```

```
const handClick = () => {
    console.log("点击事件");
  };
```

内联的事件处理函数：

```
<button onClick={() => {console.log("点击") }} >点击</button>
```

捕获阶段执行事件:` onClickCapture={handClickCapture}`
捕获事件无论再哪层，都是最先执行的

### 二.传递参数

#### 1.普通传参

```
<button onClick={(e: any) => handClick(e, "aa")}>点击</button>
```

```
const handClick = (e: any, arg: string) => {
    console.log(arg);
    console.log(e);
  };
```

#### 2.使用返回函数的函数来传递参数

```
<button onClick={handClick("aa")}>点击</button>
```

```
const handClick = (arg: string) => (e: any) => {
    console.log(arg);
    console.log(e);
  };
```

#### 3.使用数据属性传递事件和参数

元素上设置 data-\* 属性以在 onClick 事件处理程序中传递参数

```
<button date-str="aa" onClick={handClick}> 点击</button>
```

```
const handClick = (e: any) => {
    const arg = e.currentTarget.getAttribute("date-str");
    console.log(arg);
    console.log(e);
  };
```

### 三.在事件处理函数中读取 props（参数）

直接访问组件的 props

![image.png](https://upload-images.jianshu.io/upload_images/29487578-63878c84cbb3cb66.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

将事件处理函数作为 props 传递

![image.png](https://upload-images.jianshu.io/upload_images/29487578-5b42e24ce1f37acb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 四.事件传播

先执行 button ，在执行 div
注意：_在 React 中所有事件都会传播，除了 onScroll，它仅适用于你附加到的 JSX 标签。_

```
<div  className="Toolbar"  onClick={() => {alert("你点击了 toolbar ！"); }  >
      <button onClick={() => alert("正在播放！")}>播放电影</button>
      <button onClick={() => alert("正在上传！")}>上传图片</button>
 </div>
```

阻止传播:阻止触发绑定在外层标签上的事件处理函数

```
e.stopPropagation();
```

阻止默认事件:阻止少数事件的默认浏览器行为(表单提交)

```
e.preventDefault()
```

### 五.常用事件

onClick：点击事件。

onChange：输入框值改变事件。

onInput：输入框事件(值改变触发)。

onFocus：获得焦点事件（进入输入框出发）。

onBlur：失去焦点事件（离开输入框出发）。

onSubmit：表单提交事件（e.preventDefault()防止提交时重新刷新页面）。

```
<form
     onSubmit={(e) => {
      e.preventDefault();
      console.log("提交了");
     }}
 ></from>
```

onClickCapture：点击事件捕获。

onContextMenu：鼠标右击事件。

onMouseDown：鼠标按下事件。

onMouseUp：鼠标松开事件。
