## 一.recoil的基本使用
### 1.安装
```
yarn add recoil
```
### 2.在根组件index.tsx中引入，确保整个应用可以访问 Recoil 状态
```
import ReactDOM from "react-dom";
import App from "./app";
import { RecoilRoot } from "recoil";

ReactDOM.render(
    <RecoilRoot>
      <App />
    </RecoilRoot>,
  document.getElementById("root")
);
```
### 3.基本使用，新建src/state/index.tsx

#### 1）Atom的定义   
 Atom 是状态的单位   
 它们可更新也可订阅：当 atom 被更新，每个被订阅的组件都将使用新值进行重渲染
```
import { atom } from "recoil";

export const textState = atom<string>({
  key: "textState", // 唯一的 key
  default: "", // 初始值
});
```

#### 2）Atom在组件使用

```
import { textState } from "@/state/todoAtoms";
import { useRecoilState } from "recoil";

export const Home = () => {
//接收atom
  const [text, setText] = useRecoilState(textState);

  return (
      <div onClick={() =>  setText( text + 2)} >
        {text}
      </div>
  );
};
```

### 4.selector的使用
selector相当于计算属性
#### 1)定义

```
export const addTextState = selector({
  key: "addTextState",
  get: ({ get }) => {
    const addTextState = get(textState);
    return addTextState + 2;
  }
```
#### 2）在组件上使用
```
import { addTextState } from "@/state/todoAtoms";
import { useRecoilValue } from "recoil";

export const Test = () => {
  const addTextStates = useRecoilValue(addTextState);

  return (
      <div>selector:{addTextStates}</div>
  );
};
```
### 5.增删改
#### 1)定义atom
```
import { atom } from "recoil";

export const list = atom<{ id: string; text: string }[]>({
  key: "list",
  default: [],
});
```
#### 2)  拿list的数据
```
  const [lists, setLists] = useRecoilState(list);
//或
  const lists = useRecoilValue(list);

  const setLists = useSetRecoilState(list);
```
#### 3）实现增删改
```
const [inputValue, setInputValue] = useState("");
//增
  const addItem = () => {
    setLists((oldlist) => [...oldlist, { id: "123", text: inputValue }]);
  };
//删
  const deleteItem = (indexToRemove: number) => {
    setLists(lists.filter((_, index) => index !== indexToRemove));
  };
//改（更新）
  const updateItem = (indexToUpdate: number, updateData: any) => {
    setLists(
      lists.map((item, index) => (index === indexToUpdate ? updateData : item))
    );
  };

<div>
      <div>
        <input
          type="text"
          value={inputValue}
          onChange={(e) => {setInputValue(e.target.value); }}
        />
        <button onClick={addItem}>新增</button>
      </div>

      {lists.map((item, index) => (
        <div className="flex" key={index}>
          <div key={index}>{item.text}</div>

          <div onClick={() => {deleteItem(index);}}> 删除</div>
          <div onClick={() => updateItem(index, { id: "123", text: "update" })}>更新</div>
        </div>
      ))}
    </div>

```
## 二.recoil 的hook
```
//  读取和更新状态
const [value, setValue] = useRecoilState(myAtom);

// 仅读取状态
const value = useRecoilValue(myAtom);

//  仅更新状态
const setValue = useSetRecoilState(myAtom);

//  重置状态
const resetValue = useResetRecoilState(myAtom);
```
