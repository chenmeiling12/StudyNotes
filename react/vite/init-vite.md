## vite-create-ts-taiwindcss 项目的搭建和初始化

环境：nodejs 16.20.0

#### 1.创建项目

创建最新版本 vite-create 项目

```
npm create vite@latest react-ts -- --template react-ts
```

⚠️：_创建最新版本是 v5,无法使用 yarn_

创建低(2.8.0 )版本 vite

```
npm init vite@2.8.0
```

![image.png](https://upload-images.jianshu.io/upload_images/29487578-bfb16181cd902578.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2.初始化项目

##### (1)删除多余文件

![image.png](https://upload-images.jianshu.io/upload_images/29487578-d794ae7ae3585433.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### (2) 把 app.txs 写成函数组件,且删除多余代码

```
export const App = () => {
  return <div></div>;
};
```

##### (3) 修改其他文件

![image.png](https://upload-images.jianshu.io/upload_images/29487578-72772dfaa66b995f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-02bdaebe933a169b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### (4)新建 router 和 home 页面

安装路由：`yarn add react-router-dom `

![image.png](https://upload-images.jianshu.io/upload_images/29487578-c17d4bce82fed1cc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/29487578-e6573783074e47df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### (5)么配置路径别名

安装@types/node：`yarn add @types/node -D`

在 ts.config.json 配置

```
"compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"]
    }
  }
```

在 vite.config.ts 配置

```
import path from "path";
export default defineConfig({
  alias: {
    "@": path.resolve(__dirname, "./src"),
  },
});
```

##### (6)安装 taiwindcss

```
yarn add -D tailwindcss postcss autoprefixer
```

生成 tailwind.config.js 和 jspostcss.config.js

```
npx tailwindcss init -p
```

在 tailwind.config.js 配置模版路径

```
content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
```

在根目录的 index.css 文件添加

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

在页面中使用

```
<div className="text-3xl font-bold underline">home</div>
```

##### (7)安装 ahooks、ramda、axios

```
yarn add ahooks
yarn add ramda
yarn add axios
```
