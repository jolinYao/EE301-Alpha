# Front end code specification
[toc]

## I. Programming Protocol

### 1.1. Naming standard

#### 1.1.1 Project Naming

All lowercase, separated by midlines.

Positive example: `mall-management-system` Negative example: `mall_management-system/ mallManagementSystem`

#### 1.1.2 Directory Naming

All in lowercase, separated by a underscore. When there is a plural structure, plural nomenclature should be used. Abbreviations do not use plural.

**Positive example:** `scripts/styles/components/images/utils/layouts/demo-styles/demo-scripts/img/doc`

**Counterexample:** `script/style/demo_scripts/demoStyles/imgs/docs`

[Special] The component directory in the VUE project `components` is named using `kebab-case`.

**Positive example:** `head-search/page-loading/authorized/notice-icon` **Counterexample:** `HeadSearch/PageLoading`

Naming is also used `kebab-case` for all directories in the [special] VUE project except `components` for the component directories.

**Positive example:** `page-one/shopping-car/user-management` **Counterexample:** `ShoppingCar/UserManagement`

#### 1.1.3 JS, CSS, SCSS, HTML, PNG file naming

All in lowercase, separated by a underscore.

**Positive example:** `render-dom.js/signup.css/index.html/company-logo.png` **Counterexample:** `renderDom.js/UserManagement.html`

#### 1.1.4 Rigor of Naming

It is strictly forbidden to use Pinyin mixed with English in the naming of the code, and it is not allowed to use Chinese directly. Note: Correct English spelling and grammar can make it easier for the reader to understand and avoid ambiguity. Note that even pure Pinyin naming should be avoided

**Positive example:** `henan/luoyang/rmb 等国际通用的名称，可视同英文` **Counterexample:** `DaZhePromotion [打折]/ getPingfenByName() [评分]/ int 某变量 = 3`

Put an end to completely non-standard abbreviations and avoid ignorance of the meaning of the text:

**Counterexample:** `AbstractClass` "Abbreviations" are named `AbsClass`; `condition` "Abbreviations" are `condi` named. Such arbitrary abbreviations seriously reduce the readability of the code.

### 1.2. HTML specification

#### 1.2.1 HTML Type

Recommended document type declaration for HTML5:

(HTML in text/HTML format is recommended. Avoid using XHTML. XHTML and its attributes, such as application/XHTML + XML, have limited application support and optimization space in the browser.

- Specifies the character encoding
- IE compatibility mode
-  Specifies the character encoding
-  The DOCTYPE is capitalized

**Positive example:**

```html
<!DOCTYPE html>
<html>
  <head> 
      <meta http-equiv="X-UA-Compatible" content="IE=Edge" /> 
	  <meta charset="UTF-8" /> 
	  <title>Page title</title> 
  </head>
  <body> 
	 <img src="images/company-logo.png" alt="Company">
 </body> 
  </html>
```

#### 1.2.2 Indent

Indent uses 2 spaces (one tab); nested nodes should be indented.

#### 1.2.3 Block Notes

After each block, list, and table element, add a pair of HTML comments.

#### 1.2.4 Semantic tags

There are a lot of new semantic tags in HTML5, so use semantic tags first to avoid a page full of DIV or p tags.

**Positive example**

```html
<header></header> 
<footer></footer>
```

**Counterexample**

```html
<div> 
  <p></p>
 </div>
```

#### 1.2.5 Quotation marks

Use double quotes ( "") instead of single quotes ( "").

**Positive example:** `<div class=”box”></div>` **Counterexample:** `<div class=’box’></div>`

### 1.3. CSS specification

#### 1.3.1 Naming

- Use lowercase letters for class names, separated by a central dash

- The ID is humped
-  Variables, functions, mixins, and placeholders in scss are camel-named

> ID and class names always use names that reflect the purpose and use of the element, or other generic names, instead of superficial and obscure names.

**Not recommended:**

```css
.fw-800 {
    font-weight: 800;
  }
  .red {
    color: red; 
   }
```

**Recommend**

```css
.heavy {
   font-weight: 800;
  }
.important { 
  color: red; 
  }
```

#### 1.3.2 Selector

**Avoid using tag names in CSS selectors**

> From the principle of separation of structure, presentation, and behavior, HTML tags in CSS should be avoided as much as possible, and there are potential problems with tag names in CSS selectors.

**Use the direct child selector**

> Many front-end developers write selector chains without using direct child selectors (Note: Direct child selectors and descendant selectors
> Difference Sometimes this can lead to painful design problems and sometimes it can be very performance intensive. In any case, however,
> This is a very bad practice. If you don't write very generic selectors that need to match to the end of the DOM, you should always consider direct child selectors.

**Not recommended:**

```css
.content .title {
   font-size: 2rem;
  }
```

**Recommend**

```css
.content > .title {
   font-size: 2rem;
 }
```

#### 1.3.3 Use Abbreviations as Much as Possible

**Not recommended:**

```css
border-top-style: none; 
font-family: palatino, georgia, serif; 
font-size: 100%; line-height: 1.6; 
padding-bottom: 2em; 
padding-left: 1em;
 padding-right: 1em; 
 padding-top: 0;
```

**Recommend**

```css
border-top: 0; 
font: 100%/1.6 palatino, georgia, serif; 
padding: 0 1em 2em;
```

#### 1.3.4 Exclusive row for each selector and attribute

**Not recommended:**

```css
button { 
	width: 100px; 
	height: 50px;
	color: #fff;
	background: #00a0e9;
  }
```

**Recommend**

```css
button {
  width: 100px; height: 50px;
  color: #fff;
  background: #00a0e9; 
}
```

#### 1.3.5 Omit units after 0

**Not recommended:**

```css
 div {
	 padding-bottom: 0px; 
	 margin: 0em;
 }
```

**Recommend:**

```css
div {
    padding-bottom: 0; 
    margin: 0; 
}
```

#### 1.3.6 Avoid using ID selectors and global tag selectors to prevent contamination of global styles

**Not recommended:**

```css
#header {
 padding-bottom: 0px; 
 margin: 0em;
}
```

**Recommend:**

```css
.header { 
	padding-bottom: 0px; 
	margin: 0em; 
}
```

### 1.4. LESS specification

#### 1.4.1 Code organization

**Place the common less file in the style/less/common folder**

Example://color. Less, common. Less.

**Organize in the following order**

1. @ import; 2. Variable declaration; 3. Style declaration;

```css
@import "mixins/size.less"; 
@default-text-color: #333; 
.page {
 width: 960px; 
 margin: 0 auto; 
}
```

#### 1.4.2 Avoid too many nesting levels

> Limit nesting depth to 3 levels. For nesting of more than 4 levels, a re-evaluation is given. This avoids overly detailed CSS selectors. Avoid large numbers of nested rules. Break when readability is affected. It is recommended to avoid nested rules with more than 20 lines.

**Not recommended:**

~~~css
.main {
   .title {
      .name { 
           color: #fff;  
         } 
     }
}
 ```
 **推荐：**
```css
.main-title {
   .name { color: #fff; }
    }
~~~

### 1.5、Javascript 规范

#### 1.5.1 命名

**lowerCamelCase is named with a lowercase hump, and the names in the code cannot end with an underscore or a dollar sign**

**Counterexample:** *name / name* / name$

**Method names, parameter names, member variables, and local variables all use lowerCamelCase, which must follow the hump form** 

**Positive example:** localValue / getHttpMessage() / inputUserId

**Where method method naming must be a verb or verb + noun form** 

**Positive example:** saveShopCarData /openShopCarInfoDialog
**Counterexample:**  save / open / show / go

**It is hereby explained that the following 5 words shall be used in the details, and others shall not be used (the purpose is to unify the various ends).**

```bash
add / update / delete / detail / get 
附： 函数方法常用的动词: 
get 获取/set 设置, 
add 增加/remove 删除, 
create 创建/destory 销毁, 
start 启动/stop 停止, 
open 打开/close 关闭, 
read 读取/write 写入, 
load 载入/save 保存,
begin 开始/end 结束, 
backup 备份/restore 恢复,
import 导入/export 导出, 
split 分割/merge 合并,
inject 注入/extract 提取,
attach 附着/detach 脱离, 
bind 绑定/separate 分离, 
view 查看/browse 浏览, 
edit 编辑/modify 修改,
select 选取/mark 标记, 
copy 复制/paste 粘贴,
undo 撤销/redo 重做, 
insert 插入/delete 移除,
add 加入/append 添加, 
clean 清理/clear 清除,
index 索引/sort 排序,
find 查找/search 搜索, 
increase 增加/decrease 减少, 
play 播放/pause 暂停, 
launch 启动/run 运行, 
compile 编译/execute 执行, 
debug 调试/trace 跟踪, 
observe 观察/listen 监听,
build 构建/publish 发布,
input 输入/output 输出,
encode 编码/decode 解码, 
encrypt 加密/decrypt 解密, 
compress 压缩/decompress 解压缩, 
pack 打包/unpack 解包,
parse 解析/emit 生成,
connect 连接/disconnect 断开,
send 发送/receive 接收, 
download 下载/upload 上传, 
refresh 刷新/synchronize 同步,
update 更新/revert 复原, 
lock 锁定/unlock 解锁, 
check out 签出/check in 签入, 
submit 提交/commit 交付, 
push 推/pull 拉,
expand 展开/collapse 折叠, 
enter 进入/exit 退出,
abort 放弃/quit 离开, 
obsolete 废弃/depreciate 废旧, 
collect 收集/aggregate 聚集
```

**The names of constants are all capitalized, and the words are separated by underscores, so that the semantic expression is complete and clear, and the names are not too long.**

**Positive example:** MAX_STOCK_COUNT

**Counterexample:** MAX_COUNT

#### 1.5.2 Code format

Use 2 spaces for indent

**Positive example:**

```js
if (x < y) {
 x += 10;
  } else {
   x += 1; 
}
```

**Insert a blank line to separate different logic, different semantics and different business codes to improve readability.**

Note: In any case, it is not necessary to insert multiple blank lines for separation.

#### 1.5.3 String

Single quotation marks (') are used uniformly, and double quotation marks (") are not used. This is very beneficial in creating HTML strings:**Positive example:**

```js
   let str = 'foo';
   let testDiv = '<div id="test"></div>'; 
```

**Counterexample:**

```js
let str = 'foo'; 
let testDiv = "<div id='test'></div>";
```

#### 1.5.4 Object Declaration

**Create an object using literal values**

**Positive example:** `let user = {};` **Counterexample:** `let user = new Object();`

**Use literals instead of object constructors**

**Positive example:** `var user = { age: 0, name: 1, city: 3};` **Counterexample:**

```js
var user = new Object(); 
user.age = 0; 
user.name = 0; 
user.city = 0; 
```

#### 1.5.5 Using ES6 +

> The new syntactic sugar and functions in ES6 + must be used first. This will simplify your program and make your code more flexible and reusable. Such as arrow function, await/async, deconstruction, let, for … Of etc.

#### 1.5.6 Brackets

> The following keywords must be followed by braces (even if the content of the code block is only one line): if, else, for, while, do, switch, try, catch, finally, with.

**Positive example:**

```js
if (condition) { 
doSomething();
 }
```

**Counterexample:**

```js
if (condition) doSomething();
```

#### 1.5.7 undefined judgment

Never use undefined directly for variable judgments; use typeof and string 'undefined' for variable judgments. **Positive example:**

```js
 if (typeof person === 'undefined') { ... }
```

**Counterexample:**

```js
if (person === undefined) { ... }
```

#### 1.5.8 Conditional Judgment and Cycling Up to Three Layers

> Conditional judgments can be solved by using ternary operators and logical operators, so do not use conditional judgments, but remember not to write too long ternary operators. If there are more than 3 layers, please draw a function and write a clear comment.

#### 1.5.9 Conversion naming of this

> References to the context this can only be named using the'self '.

#### 1.5.10 Use console. Log with caution.

> Use the log feature with caution in non-webpack projects because of the performance issues associated with heavy use of console. Log.

## II. Vue Project Specification

### 2.1. Vue coding basis

The vue project specification is based on the A specification in the Vue official specification ([https://cn.vuejs.org/v2/style-guide/](https://cn.vuejs.org/v2/style-guide/])), on which the project is developed, so all code complies with the specification.

#### 2.1.1 Component Specifications

**Component name is multiple words**

Component names should always be multiple words (greater than or equal to 2) and the naming convention should be KebabCase format.

This avoids conflicts with existing and future HTML elements because all HTML element names are single-word.

**Positive example:**

```js
export default {
  name: 'TodoItem'
  // ...
};
```

**Counterexample:**

```js
export default {
  name: 'Todo',
  // ...
}
export default {
  name: 'todo-item',
  // ...
}
```

**Component file names are in pascal-case format**

**Positive example:**

```js
components/
|- my-component.vue
```

**Counterexample:**

```js
components/
|- myComponent.vue
|- MyComponent.vue
```

**Base component file names begin with base and use full words instead of abbreviations**

**Positive example:**

```js
components/
|- base-button.vue
|- base-table.vue
|- base-icon.vue
```

**Counterexample:**

```js
components/
|- MyButton.vue
|- VueTable.vue
|- Icon.vue
```

**Child components that are tightly coupled to a parent component should be prefixed with the name of the parent component.**

**Positive example:**

```sql
components/
|- todo-list.vue
|- todo-list-item.vue
|- todo-list-item-button.vue
|- user-profile-options.vue （完整单词）
```

**Counterexample:**

```undefined
components/
|- TodoList.vue
|- TodoItem.vue
|- TodoButton.vue
|- UProfOpts.vue （使用了缩写）
```

**When using components in the Template template, use the PascalCase pattern and use self-closing components**

**Positive example:**

```javascript
<!-- 在单文件组件、字符串模板和 JSX 中 -->
<MyComponent />
<Row><table :column="data"/></Row>
```

**Counterexample:**

```javascript
<my-component /> <row><table :column="data"/></row>
```

**The component's data must be a function**

> When the data attribute is used in a component (anywhere except new Vue), its value must be a function that returns an object. Because if it is an object directly, the attribute values of child components will affect each other.

**Positive example:**

```javascript
export default {
  data () {
    return {
      name: 'jack'
    }
  }
}
```

**Counterexample:**

```javascript
export default {
  data: {
    name: 'jack'
  }
}
```

**Prop definitions should be as detailed as possible.**

The camelCase camel must be used for naming, the type must be specified, and the type must be annotated to indicate its meaning, and the meaning must be added either required or default, either of the two, and validator must be added if there is a business need

**Positive example:**

```javascript
 props: {
  // 组件状态，用于控制组件的颜色
   status: {
     type: String,
     required: true,
     validator: function (value) {
       return [
         'succ',
         'info',
         'error'
       ].indexOf(value) !== -1
     }
   },
    // 用户级别，用于显示皇冠个数
   userLevel：{
      type: String,
      required: true
   }
}
```

**Set the scope for the component style**

**Positive example:**

```javascript
<template>
  <button class="btn btn-close">X</button>
</template>
<!-- 使用 `scoped` 特性 -->
<style scoped>
  .btn-close {
    background-color: red;
  }
</style>
```

**Counterexample:**

```javascript
<template>
  <button class="btn btn-close">X</button>
</template>
<!-- 没有使用 `scoped` 特性 -->
<style>
  .btn-close {
    background-color: red;
  }
</style>
```

**If there are many attribute elements, active line breaks should be used**

**Positive example:**

```javascript
<MyComponent foo="a" bar="b" baz="c"
    foo="a" bar="b" baz="c"
    foo="a" bar="b" baz="c"
 />
```

**Counterexample:**

```javascript
<MyComponent foo="a" bar="b" baz="c" foo="a" bar="b" baz="c" foo="a" bar="b" baz="c" foo="a" bar="b" baz="c"/>
```

#### 2.1.2. Use simple expressions in templates

Component templates should contain only simple expressions, and complex expressions should be refactored into computed properties or methods. Complex expressions make your templates less declarative. We should try to describe what should appear, not how to calculate that value. And the calculated properties and methods make the code reusable.

**Positive example:**

```javascript
<template>
  <p>{{ normalizedFullName }}</p>
</template>
// 复杂表达式已经移入一个计算属性
computed: {
  normalizedFullName: function () {
    return this.fullName.split(' ').map(function (word) {
      return word[0].toUpperCase() + word.slice(1)
    }).join(' ')
  }
}
```

**Counterexample:**

```javascript
<template>
  <p>
       {{
          fullName.split(' ').map(function (word) {
             return word[0].toUpperCase() + word.slice(1)
           }).join(' ')
        }}
  </p>
</template>
```

#### 2.1.3 The instructions all use abbreviations.

Directives are recommended in abbreviated form, (v-bind: with:, v-on: with @, and v-slot: with #)

**Positive example:**

```javascript
<input
  @input="onInput"
  @focus="onFocus"
>
```

**Counterexample:**

```javascript
<input
  v-on:input="onInput"
  @focus="onFocus"
>
```

#### 2.1.4 Label order is consistent

Single-file components should always keep the label order as

**Positive example:**

```javascript
<template>...</template>
<script>...</script>
<style>...</style>
```

**Counterexample:**

```javascript
<template>...</template>
<style>...</style>
<script>...</script>
```

#### 2.1.5 The key value key must be set for v-for

#### 2.1.6 v-show and v-if selection

Use v-show if you need to switch very frequently while running, or v-if if conditions rarely change while running.

#### 2.1.7 internal structure sequence of script tags

Components > props > data > computed > watch > filter > hook functions (hook functions in their order of execution) > methods

#### 2.1.8 Vue Router Specification

**Routing parameters are used for page jump data delivery**

Page jump, for example, when page A jumps to page B, it is necessary to transfer the data of page A to page B. It is recommended to use routing parameters to transfer parameters, instead of saving the data to be transferred in vuex and then taking out the data of vuex from page B, because if the data is refreshed on page B, it will lead to the loss of vuex data. As a result, page B cannot display data normally.

**Positive example:**

```javascript
let id = ' 123';
this.$router.push({ name: 'userCenter', query: { id: id } });
```

**Use route lazy loading (lazy loading) mechanism**

```javascript
{
    path: '/uploadAttachment',
    name: 'uploadAttachment',
    meta: {
      title: '上传附件'
    },
    component: () => import('@/view/components/uploadAttachment/index.vue')
  },
```

**Naming conventions in router**

The path and childrenPoints naming conventions adopt the kebab-case naming convention (try to keep the directory structure of the vue file consistent, because the directory and file names are kebab-case, which makes it easy to find the corresponding files).

The name naming convention uses the KebabCase naming convention and is consistent with the component name! (Because keep-alive is cached according to the name of the component to maintain the keep-alive feature, the two must be highly consistent.)

```javascript
// 动态加载
export const reload = [
  {
    path: '/reload',
    name: 'reload',
    component: Main,
    meta: {
      title: '动态加载',
      icon: 'icon iconfont'
    },
    children: [
      {
        path: '/reload/smart-reload-list',
        name: 'SmartReloadList',
        meta: {
          title: 'SmartReload',
          childrenPoints: [
            {
              title: '查询',
              name: 'smart-reload-search'
            },
            {
              title: '执行reload',
              name: 'smart-reload-update'
            },
            {
              title: '查看执行结果',
              name: 'smart-reload-result'
            }
          ]
        },
        component: () =>
          import('@/views/reload/smart-reload/smart-reload-list.vue')
      }
    ]
  }
];
```

**Naming convention of path in router**

In addition to the kebab-case naming convention, the path must begin with/, even in children. The following example

**Purpose:**

There is often such a scenario: there is a problem with a page, and if you want to find the vue file immediately, if you do not start with/, and the path is composed of parent and children, you may often need to search in the router file many times to find it, but if you start with/, you can find the corresponding component immediately.

```javascript
{
    path: '/file',
    name: 'File',
    component: Main,
    meta: {
      title: '文件服务',
      icon: 'ios-cloud-upload'
    },
    children: [
      {
        path: '/file/file-list',
        name: 'FileList',
        component: () => import('@/views/file/file-list.vue')
      },
      {
        path: '/file/file-add',
        name: 'FileAdd',
        component: () => import('@/views/file/file-add.vue')
      },
      {
        path: '/file/file-update',
        name: 'FileUpdate',
        component: () => import('@/views/file/file-update.vue')
      }
    ]
  }
```

### 2.2. Vue Project Directory Specification

#### 2.2.1 Foundation

All naming in the vue project must be consistent with the backend naming.

Such as permissions: back-end privilege, front-end regardless of router, store, API, etc. Must use the word privielege!

#### 2.2.2 Use of Vue-cli scaffolding

Use vue-cli3 to initialize the project with the project name according to the naming convention above.

#### 2.2.3 Description of contents

The directory names follow the naming convention above, where the components component is capitalized with a hump, and all other directories except the components component directory are named kebab-case.

```javascript
src                                  源码目录
|-- api                              所有api接口
|-- assets                           静态资源，images, icons, styles等
|-- components                       公用组件
|-- config                           配置信息
|-- constants                        常量信息，项目所有Enum, 全局常量等
|-- directives                       自定义指令
|-- filters                          过滤器，全局工具
|-- datas                            模拟数据，临时存放
|-- lib                              外部引用的插件存放及修改文件
|-- mock                             模拟接口，临时存放
|-- plugins                          插件，全局使用
|-- router                           路由，统一管理
|-- store                            vuex, 统一管理
|-- themes                           自定义样式主题
|-- views                            视图目录
|   |-- role                                 role模块名
|   |-- |-- role-list.vue                    role列表页面
|   |-- |-- role-add.vue                     role新建页面
|   |-- |-- role-update.vue                  role更新页面
|   |-- |-- index.less                       role模块样式
|   |-- |-- components                       role模块通用组件文件夹
|   |-- employee                             employee模块
```

**The API directory**

- File and variable naming should be consistent with the back-end.
- This directory corresponds to the backend API interface, one controller and one API JS file according to the backend. If the project is large, it can be divided into subdirectories according to the business and keep consistent with the back-end.
- The method names in the API should be as semantically consistent as possible with the backend API URL.
- For each method in the API, add comments that are consistent with the backend swagger documentation.

**Positive example:**

Backend URL: EmployeeController. Java.

```javascript
/employee/add
/employee/delete/{id}
/employee/update
```

Front-end: employee. JS.

```javascript
  // 添加员工
  addEmployee: (data) => {
    return postAxios('/employee/add', data)
  },
  // 更新员工信息
  updateEmployee: (data) => {
    return postAxios('/employee/update', data)
  },
    // 删除员工
  deleteEmployee: (employeeId) => {
    return postAxios('/employee/delete/' + employeeId)
   },
```

**The assets directory**

Assets are static resources, in which static resources such as images, styles, and icons are stored. The static resource naming format is kebab-case

```javascript
|assets
|-- icons
|-- images
|   |-- background-color.png
|   |-- upload-header.png
|-- styles
```

**The components directory**

The directory shall be divided according to the components. The directory shall be named as KebabCase, and the component naming rule shall also be KebabCase

```javascript
|components
|-- error-log
|   |-- index.vue
|   |-- index.less
|-- markdown-editor
|   |-- index.vue
|   |-- index.js
|-- kebab-case
```

**The constants directory**

This directory holds all constants for the project. If constants are used in vue, use the vue-enum plugin (https://www.npmjs.com/package/vue-enum).

Directory structure:

```javascript
|constants
|-- index.js
|-- role.js
|-- employee.js
```

Example: employee. JS.

```javascript
export const EMPLOYEE_STATUS = {
  NORMAL: {
    value: 1,
    desc: '正常'
  },
  DISABLED: {
    value: 1,
    desc: '禁用'
  },
  DELETED: {
    value: 2,
    desc: '已删除'
  }
};
export const EMPLOYEE_ACCOUNT_TYPE = {
  QQ: {
    value: 1,
    desc: 'QQ登录'
  },
  WECHAT: {
    value: 2,
    desc: '微信登录'
  },
  DINGDING: {
    value: 3,
    desc: '钉钉登录'
  },
  USERNAME: {
    value: 4,
    desc: '用户名密码登录'
  }
};
export default {
  EMPLOYEE_STATUS,
  EMPLOYEE_ACCOUNT_TYPE
};
```

**The router and store directories**

These two directories must split the business and cannot be put into a JS file.

The router is as consistent as possible with the structure in view

The store splits the different JS files by business.

**The views directory**

Naming should be consistent with backend, router, API, etc. Components in components should use PascalCase rules

```javascript
|-- views                                    视图目录
|   |-- role                                 role模块名
|   |   |-- role-list.vue                    role列表页面
|   |   |-- role-add.vue                     role新建页面
|   |   |-- role-update.vue                  role更新页面
|   |   |-- index.less                      role模块样式
|   |   |-- components                      role模块通用组件文件夹
|   |   |   |-- role-header.vue             role头部组件
|   |   |   |-- role-modal.vue              role弹出框组件
|   |-- employee                            employee模块
|   |-- behavior-log                        行为日志log模块
|   |-- code-generator                      代码生成器模块
```

#### 2.2.4 Explanatory notes

Tidy up where notes must be added

- Instructions for use of common components
- The interface JS file in the API directory must be annotated
- The state, mutation, action, etc. in the store must be annotated
- The template in the vue file must be annotated. If the file is large, add the start end annotation.
- The methods of the vue file. Each method must be annotated
- The data of the vue file, and unusual words should be noted.

#### 2.2.5 Others

**Try not to manipulate the DOM manually**

Due to the use of the vue framework, try to use the data-driven update of the vue in the project development, and try not to manually operate the DOM (unless absolutely necessary), including adding, deleting and modifying dom elements, changing styles, adding events, etc.

**Delete the useless code**

Due to the use of code version tools such as git/svn, useless codes must be deleted in time, such as some debugging console statements and useless deprecation function codes.

​                        																													  

> Reference: Alibaba Front-end Development Manual





