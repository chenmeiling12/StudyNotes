## lodash库

isEqual（）函数可以深度比较两个对象、数组是否相等；

#### 1.操作数组函数
chunk（）拆分数组；
uniq（）数组去重；
shuffle（）打乱数组顺序；
flattenDeep（）数组扁平化；
sum（）求和；

#### 2.操作对象函数
get(obj,key,defaultValue)获取对像属性值(当key为undefined的时候设置默认值defaultValue)；
set(obj,key,value)设置对象值；
merge(obj1, obj2)深度合并对像；
pick(obj, [key])选取对像；
omit(obj, [“b”])忽略对像；
sumBy（obj，key）求和；

#### 3.优化函数
debounce（fn,time）防抖；
throttle(fn,time)节流；

#### 4.操作字符串
capitalize（str）首字母大写;
kebabCase（str）所有字母小写，单词间用 - 连接;
snakeCase（str）所有字母小写，单词间用 _ 连接;
camelCase(str)首个单词小写，其余单词首字母大写，去除空格、下划线、连字符等；

#### 5.操作其他函数

重复执行函数times（count，fn）；
random(num1,num2)生成随机数；
range（num1,num2）生成范围数组；
groupBy（set，key）按属性分组，set是一个集合；
clamp(value, min, max)：value在范围内，返回自身，低于 min，返回 min，超过 max，返回 max（用于音量调节、进度条、滑块组件、分页功能）；


