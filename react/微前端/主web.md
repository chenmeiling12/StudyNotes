## 一.在主应用上

1.定义无界全局变量(/src/global.d.ts)

可用于主页面

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
    props?: { [key: string]: string };
    location?: object;
  };
}
```

定义公共 动态跳转到不同的 Web 方法
```
const handleJump = (type: AutoProjectEnum, toBack: boolean = false) => {
    setToBack(toBack); //是否跳转到后台

    switch (type) {
      case AutoProjectEnum.Identifyfile:
        setWujieApp({
          url: toBack
            ? `${import.meta.env.IDENTIFYFILE}backStage`
            : import.meta.env.IDENTIFYFILE,
          name: AutoProject[type],
        });
        break;

      case AutoProjectEnum.Qualitydetect:
        setWujieApp({
          url: toBack
            ? `${import.meta.env.QUALITYDETECT}backStage`
            : import.meta.env.QUALITYDETECT,
          name: AutoProject[type],
        });
        break;
    }
  };
```
3.控制web应用打开的方式
```
  // 当url和name发生变化时，在新的标签页打开后台，
  useUpdateEffect(() => {
    localStorage.setItem(wujieAppKey, JSON.stringify(wujieApp));

    toBack
      ? window.open(`/autoPage`, "_blank", "noopener,noreferrer") //在新标签页打开
      : window.open(`/autoPage`, "_self"); //在当前页面打开
  }, [wujieApp]);
```

定义一个同步路由页面
当一个页面存在多个子应用时无界支持所有子应用路由同步
```
 const navigate = useNavigate();

  const { userName, tokenKey, userNameKey, wujieAppKey, handleJump } =
    useAuth();

  const [wujieApp, setWujieApp] = useState<{ url: string; name: string }>({
    url: "url",
    name: "local",
  });

  // 退出
  const handleBackPlatform = (isSignout: boolean = false) => {
    if (isSignout) {
      localStorage.setItem(userNameKey, "");
      localStorage.setItem(tokenKey, "");
      localStorage.setItem(wujieAppKey, "");
    }

    navigate("/");
  };

  const handleOpenBackstage = (type: AutoProjectEnum, toBack: boolean) => {
    handleJump(type, toBack);
  };

  // 路由变化时同步更新
  useEffect(() => {
    const params = JSON.parse(localStorage.getItem(wujieAppKey) ?? "");

    setWujieApp({
      url: params.url,
      name: params.name,
    });
  }, [location]);
```
```
<WujieReact
        width="100%"
        height="100%"
        name={wujieApp.name} //微前端应用的名称
        url={wujieApp.url} //微前端应用的地址
        sync={true} //同步机制
        alive={true} //子应用的状态存活
        fiber={true} //优化 React 渲染性能
//传递给子web的参数，在子web上的定义微前端全局变量去接收它。
        props={{
          userName: userName,
          token: localStorage.getItem(tokenKey),
          handleBackPlatform: handleBackPlatform, //切换回主平台
          handleOpenBackstage: handleOpenBackstage, //跳转到不同的web。
        }}
      />
```
实现 跳转到不同的 Web的方法
```
 <div  onClick={() => handleJump(AutoProjectEnum.Qualitydetect)} >AI檢測貨品質量 </div>
```

