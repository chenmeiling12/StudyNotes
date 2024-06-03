#### 1.安装

```
yarn add react-i18next i18next
```

#### 2.创建资源文件是 JSON 文件

在 src 文件下新建 locales/en/translation.json 和 locales/zh/translation.json

```
//locales/en/translation.json
{
  "welcome": "Welcome to React",
  "hello": "Hello"
}
```

```
//locales/zh/translation.json
{
  "welcome": "欢迎使用React",
  "hello": "你好",
  "word": "世界"
}
```

#### 3.配置 i18next,在 src 下创建一个新的文件 i18next.ts

```
import i18n from "i18next";
import { initReactI18next } from "react-i18next";

import enTranslation from "./locales/en/translation.json";
import zhTranslation from "./locales/zh/translation.json";

//初始化 i18next
i18n.use(initReactI18next).init({
//应用程序支持的所有语言的翻译资源，每种语言都对应一个翻译对象
  resources: {
    en: {
      translation: enTranslation,
    },
    zh: {
      translation: zhTranslation,
    },
  },
  lng: "en", // 默认语言
  fallbackLng: "en", // 当当前语言的翻译缺失时回退到该语言
  interpolation: {
    escapeValue: false, // react已经安全了
  },
});

export default i18n;
```

#### 4.在页面上使用

如果 i18next 上的是 en，则显示的是英文，如果是 zh,则显示中文
t 里边的 translation.json 里边的 key 值，输出的就是对应的 value 值

```
import "../../i18next.js";
export const Lang = () => {
 const { t } = useTranslation();
  return (
<>
 <h1>{t("welcome")}</h1>
 <p>{t("hello")}</p>
 <p>{t("word")}</p>
)}
</>
```
