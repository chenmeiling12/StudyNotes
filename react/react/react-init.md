## 搭建 react 项目

#### 1.安装 node 环境

下载 node.js 安装包，按默认安装。安装完毕后通过 node -v 查看。

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/fa5bdd44-2552-4b6f-8a9c-8d000e8ca30f)

#### 2.安装脚手架

```
npm install -g create-react-app
```

注意：mac 系统全局安装可能会报以下错误

解决方法：先执行 `sudo chown -R $USER /usr/local/`

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/9364332a-8e30-4539-876d-b63a08b94d90)

#### 3.创建 react+ts 项目

```
create-react-app my-app --template typescript
```

#### 4.运行

```
cd my-app
npm start
```

#### 5.安装 sass

```
npm i sass
```

#### 6.初始化项目

###### (1)把 css 文件改成 module.scss

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/bf9b42da-bd4d-454a-8ace-76118ece4d14)

###### (2)把 es5 改成 es6

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/520725f5-7b87-4259-8b23-1dac8c4551f1)

###### (3)把 APP.tsx 文件写成函数组件

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/d79e5372-e7c5-46ef-927e-8b913a6c0378)

注意：函数组件被引入地方可能要多加个{}

![image](https://github.com/chenmeiling12/StudyNotes/assets/108569295/b9648436-3e88-4ea5-8feb-586c3d9a3143)
