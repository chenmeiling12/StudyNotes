#### 1.定义树类型

```
export interface ITreepProps {
  key: string;
  title: string;
  children?: ITreepProps[];
}
```

#### 2.树组件
onExpand: 处理当树节点展开时的逻辑。
expandedKeys: 含当前*展开*的节点键值的数组。
autoExpandParent: 布尔值，当展开子节点时，是否自动展开父节点。
checkable: 树节点可被选中，（显示复选框）。
checkedKeys: 含当前*选中*节点键值的数组。
onCheck：当某节点被选中时，处理其逻辑。

```
<Tree
     onExpand={onExpand}
      expandedKeys={expandedKeys}
      autoExpandParent={autoExpandParent}
      treeData={convert(orgTree)}
      checkable
      onCheck={(_, { checkedNodes }) =>onCheck({ checkedNodes,   }) }
     checkedKeys={checkedKeys?.map((item) => item.key)}
   />
```

#### 3.处理树的数据结构：

使用递归的方式处理树结构

```
const convert = (data: ITreeNode[]) => {
//递归终止条件
    return data?.map((item, index) => {
      const result: ITreeProps = {
        key: item.id ?? index,
        title: item.name,
      };

      if (item.children && item.children.length > 0) {
//自身调用
        result.children = convert(item.children);
      }

      return result;
    });
  };
```

#### 4.树查询

```
const onChange = (e: React.ChangeEvent<HTMLInputElement>) => {
const { value } = e.target;

//如果搜索框的值为空，则当前节点全部不展开，父节点全部不自动展开（递归终止）
    if (!value) {
      setExpandedKeys([]);
      setAutoExpandParent(false);
      return;
    }

//创建一个空数组，用于存储过滤后的节点的键
    const filteredKeys: React.Key[] = [];

    const filterTree = (data:ITreeProps[]) => {
//遍历每个节点
      for (let i = 0; i < data.length; i++) {
        const node = data[i];

        const nodeTitle = String(node.title);

//不区分大小写，如果输入的值包含在节点的title字段，就将该节点的键值添加到 filteredKeys 数组中。
        if (nodeTitle.toLowerCase().includes(value.toLowerCase())) {
          filteredKeys.push(node.key);
        }

//有子节点，则使用递归处理
        if (node.children) {
          filterTree(node.children);
        }
      }
    };

    filterTree(convert(orgTree));

//将过滤后的数组存进展开节点，且其父节点自动打开
    setExpandedKeys(filteredKeys);
    setAutoExpandParent(true);
  };
```
