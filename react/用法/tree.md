### 一.树的展示

##### 树的渲染

```
   <Tree checkable treeData={treeData} />
```

##### 树数据的获取

```
const [treeData, setTreeData] = useState<ITreeData[]>([]);

  const GetGetPersonTreeList = () => {
    GetPersonTree({
      StaffIdSource: 1,
      HierarchyDepth: 2,
      HierarchyStaffRange: 0,
    })
      .then((res) => {
        setTreeData(res ? convertToTreeData(res) : []);
      })
      .catch(() => {
        setTreeData([]);
      });
  };

useEffect(() => {
    GetGetPersonTreeList();
  }, []);
```

##### 处理接口返回的树数据方法，convertToTreeData.ts

```
export const convertToTreeData = (foundationData: IFoundationResponse) => {
  return foundationData.staffDepartmentHierarchy.map(convertDetailToTreeData);
};

const convertDetailToTreeData = (detail: IFoundationDetail) => {
  const { department, staffs, childrens } = detail;

  const treeData: ITreeData = {
    title: department.name,
    value: department.id,
    key: department.id,
  };

  if (staffs && staffs.length > 0) {
    treeData.children = staffs.map((staff) => ({
      title: staff.userName,
      value: staff.id,
      key: staff.id,
    }));
  }

  if (childrens && childrens.length > 0) {
    treeData.children = (treeData.children || []).concat(
      childrens.map(convertDetailToTreeData)
    );
  }

  return treeData;
};
```

##### 树类型定义

```
export interface IFoundationDetail {
  department: {
    id: string;
    name: string;
    parentId: string;
  };
  staffs: {
    id: string;
    userName: string;
  }[];
  childrens?: IFoundationDetail[];
}

export interface IFoundationResponse {
  staffDepartmentHierarchy: IFoundationDetail[];
}

export interface ITreeData {
  title: string;
  value: string;
  key: string;
  children?: ITreeData[];
}
```

### 二.树的多选和展开

<Tree/>添加属性值

```
       checkable

        onExpand={(newExpandedKeys) => {
          setExpandedKeys(newExpandedKeys);
          setAutoExpandParent(false); //可以收起
        }} //执行展开/关闭节点的函数

        onCheck={(checkedKeys) => {
          setShowCheck(checkedKeys as React.Key[]);
        }} //选中和取消时执行的函数onTreeCheck

        expandedKeys={expandedKeys} //存储展开指定的树节点的值

        autoExpandParent={autoExpandParent} //是否自动展开父节点

        checkedKeys={showCheck} //选中树节点的value 数组
```

定义变量用于存储选中、展开树节点的值、判断是否展开父节点

```
  const [showCheck, setShowCheck] = useState<React.Key[]>([]);

  const [expandedKeys, setExpandedKeys] = useState<React.Key[]>([]);

  const [autoExpandParent, setAutoExpandParent] = useState<boolean>(true);
```

### 三.树的搜索

##### 1.打开被搜索到值的父节点

搜索组件

```
    <div className="flex items-center">
        <Input
          placeholder="add man"
          className="w-[40rem] mr-3"
          onChange={(e) => setTreeSearch(e.target.value)}
          value={treeSearch}
        />
        <Button
          type="primary"
          className="w-[6rem] mr-[1rem] bg-[#763DFA]"
          style={{
            background: "linear-gradient( 180deg, #956AF8 0%, #763DFA 67%)",
          }}
          onClick={onTreeSearch}
        >
          查詢
        </Button>
        <Button type="text" className="w-[6rem]" onClick={onResetSearch}>
          重置
        </Button>
      </div>
```

搜索功能

当搜索值为空时，展开节点的 set 为空，并使用 return 继续执行一下代码；
当搜索值不为空:
1）定义一个临时存储符合搜索条件的的 key 的变量 filteredKeys

2）定义一个递归过滤函数，使用 for...of 遍历 treeData 获取当前树节点 node，然后拿当前节点的 title 值去查看，使用 includes 判断 node.title 是否含有搜索的字符，有的话把当前节点的 key 值 push 进 filteredKeys；
判断当前 node 是否有 children，有的话调用递归过滤方法

3）把过滤的出来的树节点的值 set 进展开节点的值,并设置自动展开节点的变量为 true

```
const [treeSearch, setTreeSearch] = useState<string>("");

const onTreeSearch = () => {
//当搜索值为空
    if (!treeSearch) {
      setExpandedKeys([]);

      return;
    }

    const filteredKeys: React.Key[] = []; //用于存储符合搜索条件的的key

//定义递归过滤函数
    const filterTree = (data: ITreeData[]) => {
      for (const node of data) {
        const nodeTitle = node.title;

        if (nodeTitle.toLowerCase().includes(treeSearch.toLowerCase())) {
          filteredKeys.push(node.key);
        }

        if (node.children) {
          filterTree(node.children);
        }
      }
    };

    filterTree(treeData);

    setExpandedKeys(filteredKeys); //把过滤的出来的树节点的值set进展开节点的值

    setAutoExpandParent(true);
  };

//重置，设置搜索值为空，关闭自动展开节点，树的张开节点全设置为空，
  const onResetSearch = () => {
    setTreeSearch("");

    setExpandedKeys([]);

  };
```

####2.搜索高亮
使用 react-highlight-words 实现
<Tree/>添加属性

```
treeData={isFilter ? filterTreeData : treeData}

//高亮
titleRender={(nodeData) => {
          return (
            <Highlighter
              highlightStyle={{
                backgroundColor: "#ffc069",
              }}
              searchWords={[treeSearch]}
              autoEscape
              textToHighlight={nodeData.title ? nodeData.title.toString() : ""}
            />
          );
        }}
```

高亮搜索

高亮的搜索新增节点的过滤
1）新增存储符合搜索条件的节点及其子节点的变量 filteredTree

2）封装一个遍历和过滤每个节点及其子节点的方法 filterNodes(),先使用 forEach 循环遍历树结构，然后定义一个判断是否含有某个节点的键变量 inFilteredTree，再封装一个方法用于递归检查 filteredTree 中是否已经包含某个节点的键，如果不存在，则把该节点的值 push 进 filteredTree，最后把 filteredTree set 进 filterTreeData 即可

```
const [treeData, setTreeData] = useState<ITreeData[]>([]);

const [isFilter, setIsFilter] = useState<boolean>(false);

const onTreeSearch = () => {

    const filteredKeys: React.Key[] = [];

    const filteredTree: ITreeData[] = [];  //用于存储符合搜索条件的节点及其子节点

    const filterTree = (data: ITreeData[]) => {

      //用于遍历和过滤每个节点及其子节点
      const filterNodes = (nodes: ITreeData[]) => {
        nodes.forEach((node: ITreeData) => {
          const nodeTitle = node.title;

          if (nodeTitle.toLowerCase().includes(treeSearch.toLowerCase())) {
            //node.key不含于filteredKeys，把值push进filteredKeys
            filteredKeys.indexOf(node.key) === -1 &&
              filteredKeys.push(node.key);

            let inFilteredTree: boolean = false;

            // 用于递归检查 filteredTree 中是否已经包含某个节点的键
            const checkedSameKey = (data: ITreeData[], key: string) => {
              data.forEach((item) => {
                if (item.key === key) {
                  return (inFilteredTree = true);
                }

                item.children && checkedSameKey(item.children, key);
              });
            };

            checkedSameKey(filteredTree, node.key);

            // 如果不存在，择将节点加入filteredTree
            !inFilteredTree && filteredTree.push(node);
          }

          if (node.children) {
            filterNodes(node.children);
          }
        });
      };

      filterNodes(data);

      return { filteredKeys, filteredTree };
    };

    setIsFilter(true);

    setFilterTreeData(filteredTree);
  };

//重置时设置过滤的数据为空
const onResetSearch = () => {

    setIsFilter(false);

    setFilterTreeData([]);
  };
```
