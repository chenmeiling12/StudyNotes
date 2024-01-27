### tag 版本

#### 1.添加一个版本，与里程碑一样。

![image.png](https://upload-images.jianshu.io/upload_images/29487578-a5c699b77bb9df70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2.把 Dockerfile 的 pr 合进去，点击 Merged 后;立马到 Tags 页面，马上点击 create tag;立马到 teamcity(CI)点击 Run,并查看是不是版本号是否一致;如果不是，则重新开 pr,重复以上步骤。

![](https://upload-images.jianshu.io/upload_images/29487578-f807ac2a63b51b61.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/29487578-d951c3413f887b55.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/29487578-00331a00791857ab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3.到 Octopus Deploy（CD）的创建 relases

![image.png](https://upload-images.jianshu.io/upload_images/29487578-949db300f1aa0bae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/29487578-842ed90c95e446c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/29487578-55f54e5f493a0988.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 4.发 test 环境

![image.png](https://upload-images.jianshu.io/upload_images/29487578-da9587d534fedc42.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 5.到 lssues 创建关掉原有的 milestone,并新建一个新的 milestone.

![image.png](https://upload-images.jianshu.io/upload_images/29487578-6af8d9200755ef43.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
