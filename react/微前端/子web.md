1.在子web上定义全局变量（pages/global.d.ts）
```
interface Window {
  // 是否存在无界
  __POWERED_BY_WUJIE__?: boolean;
  // 子应用公共加载路径
  __WUJIE_PUBLIC_PATH__: string;
  // 原生的querySelector
  __WUJIE_RAW_DOCUMENT_QUERY_SELECTOR__: typeof Document.prototype.querySelector;
  // 原生的querySelectorAll
  __WUJIE_RAW_DOCUMENT_QUERY_SELECTOR_ALL__: typeof Document.prototype.querySelectorAll;
  // 原生的window对象
  __WUJIE_RAW_WINDOW__: Window;
  // 子应用沙盒实例
  __WUJIE: WuJie;
  // 子应用mount函数
  __WUJIE_MOUNT: () => void;
  // 子应用unmount函数
  __WUJIE_UNMOUNT: () => void;
  // 注入对象
  $wujie: {
    bus: EventBus;
    shadowRoot?: ShadowRoot;
//接收主应用通过<WujieReact>传来的参数 
    props?: {
      userName: string;
      token: string;
      handleBackPlatform: (isSignout?: boolean) => void;
      handleOpenBackstage: (type: AutoProjectEnum, toBack: boolean) => void;
    };
    location?: object;
  };
}

```
2.对退出登录、用户名、切换后台做判断

判断是否是无界，是的话则使用主web退出登录
```
  window.__POWERED_BY_WUJIE__
                        ? window.$wujie.props?.handleBackPlatform(true)
                        : signOut(() => navigate("/login", { replace: true }));
```
```
     <span className="text-base">
                  {window.__POWERED_BY_WUJIE__
                    ? window.$wujie.props?.userName
                    : userName}
                </span>
```
```
     <div onClick={() => {
                    window.__POWERED_BY_WUJIE__
                      ? window.$wujie.props?.handleOpenBackstage(
                          AutoProjectEnum.Qualitydetect,
                          true
                        )
                      : window.open(
                          "/backStage",
                          "_blank",
                          "noopener,noreferrer"
                        );
                  }}
                > 切換後台   </div>
```
3.判断token的情况(auth-status.tsx)
  ```
  if (window.__POWERED_BY_WUJIE__) {
    window.$wujie.props?.token || window.$wujie.props?.handleBackPlatform(true);
  } else if (!localStorage.getItem(tokenKey)) {
    return <Navigate to="/login" state={{ from: location }} replace={true} />;
  }
```
4.对http-client.tsx
还有接口的token（http-client.tsx），当是无界的时候，也要使用主web传来的token
```
 const authorizeToken = window.__POWERED_BY_WUJIE__
      ? window.$wujie.props?.token
      : localStorage.getItem(import.meta.env.TOKENKEY);
```
当登录有问题的时候，也要做判断
```
  if (window.__POWERED_BY_WUJIE__) {
          window.$wujie.props?.handleBackPlatform(true);
 } else {
        localStorage.removeItem(import.meta.env.TOKENKEY);
        window.location.reload();
}
```

项目切换按钮也要做无界判断
```
 {window.__POWERED_BY_WUJIE__ && (
        <div className="px-[2.5rem]">
          <Button
            className="bg-transparent text-[#6554F1] border-[#6554F1] my-[2rem]"
            block
            onClick={() => window.$wujie.props?.handleBackPlatform()}
          >
            切換AI項目
          </Button>
        </div>
      )}
```

5.监听且同步状态（router/index.tsx）
```
 useEffect(() => {
    const handleTokenRefresh = (token: string, userName: string) => {
      if (window.$wujie?.props) {
        window.$wujie.props.token = token;
        window.$wujie.props.userName = userName;
      }
    };

    const registerListener = () => {
      if (window.$wujie?.bus) {
        window.$wujie.bus.$on("token_refresh", handleTokenRefresh);//监听事件
      } else {
        console.log("Wujie bus 未初始化");
      }
    };

    registerListener();

    return () => {
      if (window.$wujie?.bus) {
        window.$wujie.bus.$off("token_refresh", handleTokenRefresh);//移除事件
      }
    };
  }, []);

```

