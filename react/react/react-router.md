## react-router

### 一 路由基础

#### 1.安装

`npm install react-router-dom@6`或`yarn add react-router-dom@6 `

#### 2.在 index.tsx 文件中配置

导入 import { BrowserRouter } from "react-router-dom";
换成路由标签<BrowserRouter>
BrowserRoute(HTML5 的 history API)，让页面的 UI 与 URL 同步。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/1bf1f304-aeca-4ec1-a679-8a71b1975286)

#### 3.在 App.tsx 文件中注册路由

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/f369c013-013c-45d1-90ee-3201af21e56c)

#### 4.导航：使用路由实现跳转

##### (1)Link

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/4f6c0dce-2d00-4d89-a1b9-1a66a22baa3b)

##### (2)useNavigate

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/5df19982-5c54-4ef5-8e1e-a20bc05ce4e5)

#### 5. 传递参数和读取参数

传递参数

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/790121ee-1543-4b44-a5ee-480157d48ccb)
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/2c1a75b1-3192-4508-8063-c0b375d0b602)

使用 useParams 接受参数

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/1674d5cc-b10f-4ecb-aefb-9b262675993c)

#### 6.二级路由

在注册路由时把二级路由嵌套在一级路由里边

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/cefb6c1a-8b79-4bcf-9c98-e02f2d26d801)
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/819b32ee-fd8e-4840-8d11-680bb8599707)

结果：

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/d08f0269-97c3-41ac-8acd-3cad25076106)

设置页面/路由不存在或异常时显示的内容，path="\*"

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/e7a22f62-025c-4067-b364-7de89b0cbd0a)

### 二．使用 createBrowserRouter 封装路由

#### 1.在 src 下新建一个路由 router 文件夹，新建 index.tsx 文件，用来存放路由

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/caed065f-8a31-42dd-ba19-c0195b95278c)

路由配置

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/3c198cde-5fc9-497b-86f3-6e687bf78a61)

#### 2 在 index.tsx 文件上注册路由

RouterProvider:是一个 router 的开始，所有路由对象都会传到这个组里

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/3cee20ff-1008-4d2f-b31c-08fe99040019)

在页面上使用

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/12e63342-08ee-4adb-a42f-06ea27ce14f0)

结果：

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/ca23b3c0-13f6-4d25-b87f-152fb9cac607)

### 三.自定义封装路由组件

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/46d79689-d40f-4cb3-8650-e52d9f8122ce)

#### 2 index.tsx:封装路由

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/efd9c5d6-cded-45d9-b091-a99180e85cfc)
![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/1dee7e59-b642-4148-9154-288ab36de515)

#### 3 在 props.ts 文件中定义数据类型

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/5416b2a9-d203-4523-bbf3-9754852b8119)

#### 4 在 App.tsx 文件引入 Router 组件

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/4f660678-a10c-4241-bc0a-0c2d319055bd)
