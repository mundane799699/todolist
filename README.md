### 缘起

帮助自己复习一下前端知识，加深对vue的理解

### 版本

vue2

### 初始化项目

```
vue create todolist
```

禁止eslint

```
lintOnSave: false
```

启动之后直接打开浏览器

```
vue-cli-service serve --open
```



### 划分结构

新建两个vue文件，todoInput、todoList

并在App中引入组件，启动，看一下效果

### todoInput

#### 引入element-ui

https://element.eleme.cn/#/zh-CN/component/installation

```
npm i element-ui
```

在main.js中

```
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
...
Vue.use(ElementUI);
```

#### Input输入框

https://element.eleme.cn/#/zh-CN/component/input

复制粘贴

#### 添加自定义事件

```
this.$emit("addTask", this.taskName);
```

```
addTaskToList(taskName) {
   this.todoList.unshift({
      id: "",
      task: taskName,
      isCompleted: false,
   });
},
```

#### 非空校验

https://element.eleme.cn/#/zh-CN/component/message

#### 引入nanoid

```
npm i nanoid@4
```

nanoid是分别暴露的，所以这样引入

```
import { nanoid } from 'nanoid'
```

### todoList

#### 将todoList数据传给todoList组件

```
<todoList :todoList="undoList"></todoList>
```

### 遍历显示

ul > li

v-for

#### checkbox和span

https://element.eleme.cn/#/zh-CN/component/checkbox

#### 调整样式

写css

#### checkbox添加@change

https://element.eleme.cn/#/zh-CN/component/message

### 已完成/未完成（completeHeader）

去阿里巴巴矢量图标库找个图标

v-if

v-else

发送自定义事件修改状态值

设置文字不可被选中和鼠标指针样式

### 未完成的todoList

在计算属性中添加一个completedList

添加v-show控制未完成todoList的显示与隐藏

增加样式，给已完成的添加删除线



修改el-checkbox的颜色

https://blog.csdn.net/lanmengyingfei/article/details/117443538

https://blog.csdn.net/weixin_46156770/article/details/125867582

### 删除功能

添加一个el-button，默认为display: none

hover时显示

添加删除按钮的点击事件和自定义事件

### 修改功能

#### 在input-container中新增一个el-input

#### 将span变成块级元素

#### 给span增加点击事件，切换成编辑模式，并且自动获取焦点

- Vue.set

- v-for和ref

https://blog.csdn.net/wswq2505655377/article/details/122183254

- $nextTick，当节点渲染完毕了，会执行一次

#### 给el-input增加失去焦点或者按下enter键的事件，切换成查看模式

### 本地存储数据

监控todolist，数据有变化就存入本地

取的时候先从本地取

存储的时候去掉editable属性

### 涉及的vue相关的知识点

- 自定义事件

- Vue.set($set)
- $nextTick
- v-for和ref配合使用

