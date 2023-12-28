## 组件传值

### 一．父组件--->子组件

#### 1.属性传值

传递多个参数

![image.png](https://upload-images.jianshu.io/upload_images/29487578-502001ea677dff42.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接收参数可以使用 es6 解构赋值

![image.png](https://upload-images.jianshu.io/upload_images/29487578-4e7d0fb623403dec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

传一个参数

![image.png](https://upload-images.jianshu.io/upload_images/29487578-1e137c928416f81f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/29487578-0f7806ce526b83b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2.函数传值

##### （1）事件传值

![image.png](https://upload-images.jianshu.io/upload_images/29487578-4339e5a515069e0c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

写法二：

![image.png](https://upload-images.jianshu.io/upload_images/29487578-6e1ebdccd8563b0a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

写法三：

![image.png](https://upload-images.jianshu.io/upload_images/29487578-6771d9c3a4ae72b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### （2）属性传值

![image.png](https://upload-images.jianshu.io/upload_images/29487578-88bedf3f49c4346f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-f3a16fde0424158a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-80c096f364b8d7d1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 二．子传父

#### 1.单个参数传值

![image.png](https://upload-images.jianshu.io/upload_images/29487578-798626a616324eb6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2.多个参数传值：

![image.png](https://upload-images.jianshu.io/upload_images/29487578-c38eeb00aa21a1e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

写法二：

![image.png](https://upload-images.jianshu.io/upload_images/29487578-f2fe77535b3cff84.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 三．兄弟传值

原理：子(传)->父->子(收)

#### 1.单个参数传递

![image.png](https://upload-images.jianshu.io/upload_images/29487578-caa04ec4035501c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2.多个参数

![image.png](https://upload-images.jianshu.io/upload_images/29487578-d73f361b3f20b2c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
