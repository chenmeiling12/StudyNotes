### 1.理解 useCallback

useCallback(fn, dep)有两个参数，fn 是缓存需要在组件中多次调用的回调函数，dep 是依赖项。
当依赖项发生变化时，useCallback 会返回一个新的回调函数，否则返回之前缓存的回调函数，这样可以避免在每次渲染时都重新生成回调函数，从而提高组件的性能。

### 2.使用

#### 1）当不使用 useCallback 时

每次组件重新渲染时，handleClick 函数都会被重新创建

```
import {  useState } from "react";

export const Test = () => {
  const [num, setNum] = useState(0);

  const handleClick = () => {
    setNum(num + 1);
    console.log(num);
  };

  return (
    <div>
      <button onClick={handleClick}>Click me</button>
    </div>
  );
};
```

![image.png](https://upload-images.jianshu.io/upload_images/29487578-5eaa08466a6f2fd2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 2）依赖项为空 [] 时

由于依赖数组为空，handleClick 在组件挂载时只会被创建一次，不会在后续的渲染中重新创建。这种写法是不推荐，但可以参考 3）的优化写法

```
import { useCallback, useState } from "react";

export const Test = () => {
  const [num, setNum] = useState(0);

  const handleClick = useCallback(() => {
    setNum(num + 1);
    console.log(num);
  }, []);

  return (
    <div>
      <button onClick={handleClick}>Click me</button>
    </div>
  );
};
```

![image.png](https://upload-images.jianshu.io/upload_images/29487578-2f51d8573e79bb62.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3）使用依赖项时

handleClick 函数会在 num 改变时重新创建，确保它是最新的

```
import { useCallback, useState } from "react";

export const Test = () => {
  const [num, setNum] = useState(0);

//返回的是更新前的值
  const handleClick = useCallback(() => {
    setNum(num + 1);
    console.log(num);
  }, [num]);

//优化写法：返回更新后的值
 const handleClick = useCallback(() => {
    setNum((prev) => {
      console.log(prev + 1);
      return prev + 1;
    });
  }, []);

  return (
    <div>
      <button onClick={handleClick}>Click me</button>
    </div>
  );
};
```

优化前：
![image.png](https://upload-images.jianshu.io/upload_images/29487578-9fdc7721b6f235f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

优化后：

![image.png](https://upload-images.jianshu.io/upload_images/29487578-16f7c54736a654e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

优化的写法解释，setNum 是由 useState 提供的函数，在组件生命周期内保持不变。回调函数 handleClick 仅依赖于 setNum，没有依赖其他任何状态。
handleClick 函数调用时，会更新 setNum 状态，而 handleClick 函数本身不会因为组件重新渲染而重新创建，这符合性能优化的预期。

```
 const handleClick = useCallback(() => {
    setNum((prev) => {
      console.log(prev + 1);
      return prev + 1;
    });
  }, []);
```

4)防止子组件不必要的重新渲染:
当回调函数作为 prop 传递给子组件时，使用 useCallback 可以防止子组件因父组件的重新渲染而重新渲染,要结合 memo()使用

```
import { memo, useCallback, useState } from "react";

const Child = memo((props: { onClick: () => void }) => {
  console.log("ChildComponent rendered");
  return <button onClick={props.onClick}>点击子组件</button>;
});

export const Test = () => {
  const [num, setNum] = useState(0);

  const handleClick = useCallback(() => {
    setNum((prevCount) => prevCount + 1);
  }, []);

  return (
    <div>
      <div>父组件{num}</div>
      <Child onClick={handleClick} />
    </div>
  );
};
```

![image.png](https://upload-images.jianshu.io/upload_images/29487578-db3c87404a5f5992.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
