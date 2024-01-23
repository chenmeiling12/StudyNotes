#### 1.在 public 新建 appsetting.json 文件，定义全局配置

```
{
  "serverUrl": "https://testapi.yamimeal.com",
  "jsVersion": "3.8.0",
  "sourceSystem": "web_customer",
  "languagecode": "zh-TW"
}
```

#### 2.在根目录下新建.evn 文件，添加端口号

```
PORT = 8080
```

#### 3.在 src 新建新建 appsettings.ts 文件,定义类型

```
export interface AppSettings {
  serverUrl: string;
  jsVersion: string;
  sourceSystem: string;
  languagecode: string;
}

const settings = (window as any).appSettings;

export async function InitialAppSetting() {
  if ((window as any).appSettings) return (window as any).appSettings;

  await fetch("../appsetting.json", {
    headers: { "Content-Type": "application/json", Accept: "application/json" },
  })
    .then((res) => res.json())
    .then((res: AppSettings) => {
      return ((window as any).appSettings = res);
    });
}

export default settings as AppSettings;
```

#### 4.在 src 新建 AppHook.ts，初始化 appsetting

```
import { useState, useEffect } from "react";
import { InitialAppSetting } from "./appsettings";

const useAction = () => {
  const [isLoaded, setIsLoaded] = useState<boolean>(false);

  useEffect(() => {
    InitialAppSetting().then(() => setIsLoaded(true));
  }, []);
  return { isLoaded };
};

export default useAction;
```

在 app.tsx 使用

![image.png](https://upload-images.jianshu.io/upload_images/29487578-8a3431532fbb6a7a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 5.在 src 新建 services 目录

![image.png](https://upload-images.jianshu.io/upload_images/29487578-b1bfc0c116bbbf61.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### (1)在 services 新建 api 目录 http-client.tsx，封装 get/post 请求

```
import { AppSettings } from "../../appsettings";

export async function Get<T>(url: string) {
  return base<T>(url, "get");
}

export async function Post<T>(url: string, data?: object) {
  return base<T>(url, "post", data);
}

export async function base<T>(
  url: string,
  method: "get" | "post",
  data?: object
) {
  const settings: AppSettings = (window as any).appSettings;

  return await fetch(`${settings.serverUrl}${url}`, {
    method: method,
    body: data ? JSON.stringify(data) : undefined,
    headers: {
      js_version: settings.jsVersion,
      source_system: settings.sourceSystem,
      "Content-Type": "application/json",
    },
  })
    .then((res) => res.json())
    .then((res: T) => {
      return res;
    })
    .catch((err) => {
      console.log("request error:", err);
      throw new Error(err);
    });
}

```

##### （2）在 api 目录下新建定义接口目录和文件，存放接口

```
import { Get, Post } from "../http-client";
import {
  ISwiperApiDataProps,
  ISwiperListProps,
  IGroceryListParamsProps,
  IGroceryListProps,
} from "../../dtos/grocery";

//post
export const GetSwiperList = async (
  data: ISwiperApiDataProps
): Promise<ISwiperListProps[]> => {
  return await Post("/api/Advertisement/advertisements", data);
};

//get
export const GetGroceryList = async (
  params: IGroceryListParamsProps
): Promise<IGroceryListProps> => {
  return await Get(
    `/api/merch/list?limit=${params.limit}&page=${params.page}&deliveryType=${params.deliveryType}&lat=${params.lat}&lng=${params.lng}`
  );
};

```

##### (3)在 services 目录下新建 dtos,在 dtos 目录下新建定义接口目录和文件,存放接口数据的数据类型

```
export enum GroceryTypeEnum {
  Pickup = 0,
  Delivery = 1,
  Both = 2,
}

export interface IGroceryListParamsProps {
  limit: number;
  page: number;
  deliveryType: number;
  lat: number;
  lng: number;
}
```

#### 6.在组件中调用接口

```
//get
 GetGroceryList({
      limit: 30,
      page: page,
      deliveryType: GroceryTypeEnum.Pickup,
      lat: latlng.lat,
      lng: latlng.lng,
    }).then((data) => {
        setPickupList(data);
      }
    })
    .catch((err) => {
      throw new Error(err);
    });;

//post
    PostSwiperList({
      pageLocation: PageLocationEnum.HomePageUp,
      languageCode: settings.languagecode,
      latLng: latLng,
    }).then((data) => {
      setSwiperList(data);
    }).
    catch((err) => {
      throw new Error(err);
    });;
```
