### 一.对 CICD 的理解

CICD ：持续集成，持续交付，持续部署的过程。

持续集成 : 将代码更改合并到一个 main 分支的流程。

持续交付 ： 在持续集成阶段建立的测试和构建自动化为基础。

持续部署 ： CI/CD 流程的最后阶段，在这个阶段满足所有要求后，新版本的软件将交付给最终用户。

### 二.CI 配置流程（web）

#### 1.创建项目

![image.png](https://upload-images.jianshu.io/upload_images/29487578-08253b2581423951.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-b06819b832f7b5e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-f030ed00e960c52c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-c005fd2996f36251.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2.项目参数

![image.png](https://upload-images.jianshu.io/upload_images/29487578-31f324b12466a819.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3.新建 build

![image.png](https://upload-images.jianshu.io/upload_images/29487578-93d236c365a59988.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 4.设置构建配置（自动化构建过程）

⚠️：Install Dependencies、Build、Docker Build Images 是在 web 目录下完成的

![image.png](https://upload-images.jianshu.io/upload_images/29487578-2a2fc40f56271a0f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-6a41e4f9a7d0952a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 5.build 配置参数

![image.png](https://upload-images.jianshu.io/upload_images/29487578-63ec20dd5558c48a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-75164653a06ab099.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 6.运行

![image.png](https://upload-images.jianshu.io/upload_images/29487578-b9989cd6bb1cfa4d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-4773adafc37493ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 三.CD 的配置流程（web）

Process 搭建：DEPLOY KUBERNETES CONTAINERS（Deploy web）
和 DEPLOY KUBERNETES INGRESS RESOURCE (Deploy ingress)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-b1b45f9128f60e16.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 1.搭建项目 CD:

![image.png](https://upload-images.jianshu.io/upload_images/29487578-26743aa97981b893.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-82a7fefff4042969.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 2.配置 process

配置 DEPLOY KUBERNETES CONTAINERS （deplaoy web ）
![image.png](https://upload-images.jianshu.io/upload_images/29487578-098e569b89b10881.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-1c3c0431880d2c19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-abc49cc293ba80e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-29e8b520e08af4bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-a32aed1cf96af3b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-9bcf1d377622391e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-1dbb0754041fbecd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

appsettings.json 对应下面的配置（下面图片是在 Variable / Projectmu 目录下）

![image.png](https://upload-images.jianshu.io/upload_images/29487578-a80ac8325b6be1b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### add volume

![image.png](https://upload-images.jianshu.io/upload_images/29487578-b587b714001c89e7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### add container

![image.png](https://upload-images.jianshu.io/upload_images/29487578-12c8462e6230d7e7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-0c411af1ead47a40.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

配置 DEPLOY KUBERNETES INGRESS RESOURCE（Deploy ingress）
![image.png](https://upload-images.jianshu.io/upload_images/29487578-343a0a26b9516e8e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-a1e34a26eb7037c0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-d4c05520e84e9399.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-a47731baf633d720.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-2bdb6c1f9e9ec46e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### ingress host rules

![image.png](https://upload-images.jianshu.io/upload_images/29487578-ed9bec23f2eefcfa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### ingress tls

![image.png](https://upload-images.jianshu.io/upload_images/29487578-eaf9d5c0ebba5e69.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 四.配置 variables/project

dev 开发环境 ： 一般指开发人员本地开发调试阶段。

test 提测环境 ：一般指开发人员提交可测试版本，数据层面会有一定的模拟数据保证功能测试。

prd : 线上环境。

![image.png](https://upload-images.jianshu.io/upload_images/29487578-fcc2cc927fcb1c3a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-47bde3b9626da721.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 五.添加 releases

![image.png](https://upload-images.jianshu.io/upload_images/29487578-c8c4afdee8d1bacd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-dbcb08c3415f2e70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-550d9f19acc42c51.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-ca77dcb29c960907.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
