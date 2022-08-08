# 前端项目规范
为了同一团队代码风格，尽可能地使代码容易阅读，规定了部分代码规范:


1. 代码缩进用`2个空格`代替tab
2. 文件结束符使用 `LF`，如果是 `CRLF`，请自行配置编辑器、git等工具
3. 代码风格检测使用`eslint+prettier`（编辑器插件自行配置，读取本地项目的配置文件）
4. 禁用 `全局样式`，造成不必要的样式重写
5. 少写看上去高级，却不容易阅读的代码（交给构建工具去做），逻辑步骤要明确

详细目录:
1.  [markdown语法参考](https://github.com/google/styleguide/blob/gh-pages/docguide/style.md#document-layout)
2.  [Javascript规范](#Javascript规范)
    1.  [命名规范](#命名规范)
    1.  [对所有流控制结构使用花括号](#对所有流控制结构使用花括号)
    1.  [JS注释](https://jsdoc.app/tags-param.html)
    1.  [TS注释](http://typedoc.org/tags/param/)
4.  [vue规范](#vue规范)
    1.  [部分技术建议](#部分技术建议)
    1.  [组件文件结构](#组件文件结构)
    1.  [组件注册及使用](#组件注册及使用)
    

## Javascript规范

- 虽然前端流行不加分号，但还是建议养成行末添加分号的习惯 `";"`
- `明确声明`每一个文件中用到的所有资源，保证可以直`接跳转到引用`
- 养成按需引入的习惯

### 命名规范

`UpperCamelCase`：  每个单词的首字母都大写，包含第一个单词。

 类名、组件名、类型定义，都应该首字母大写

```ts
class GoodStudent {}

const user: GoodStudent = new GoodStudent();

type Major = '语文' | '数学';

```

`lowerCamelCase`： 除了第一个字母始终是小写（即使是缩略词），每个单词的首字母都大写。

常量、函数、普通变量，每个单词首字母都应大写，并且不使用分隔符。

```javascript
var count = 13

let name = 'Jone'

const tokenName = 'user-token'

function getBasicInfo () {}
```

### 对所有流控制结构使用花括号
```javascript
if (isWeekDay) {
  print('Bike to work!');
} else {
  print('Go dancing or read a book!');
}
```

这里有一个例外：一个没有 else 的 if 语句，并且这个 if 语句以及它的执行体适合在一行中实现。在这种情况下，如果您愿意，可以不用括号：

```javascript
if (arg == null) return defaultValue;
```

但是，如果执行体包含下一行，请使用大括号：

```javascript
if (overflowChars !== other.overflowChars) {
  return overflowChars < other.overflowChars;
}
```


## vue规范

### 组件文件结构

> 注：可以是单文件组件 `YourWidget.后缀名`

```
YourWidget
    ├── views <可选>文件夹：路由相关
    ├── components <可选>文件夹：用到的组件
    ├── styles 文件夹：<可选>样式相关
    ├── utils <可选>文件夹：用到工具
    ├── index.ts/index.js <可选>
    └── index.vue 组件入口
```

### 部分技术建议
- 不允许将图片等`静态资源`放入`src`文件夹，请放在`public`文件夹里
- 保持`main.js`干净
- 不建议使用`vuex` 。（如果用：请把变量名取复杂一点）
- 不建议使用`event-bus`等类似的订阅发布模式。（如果用：请把订阅名取复杂一点）
- 不建议使用 `provide` 和 `injecet`。 （如果用：请把方法名取复杂一点）

### 组件注册及使用

组件使用时需保持与注册时的`key`一至（可不与组件内部`name`相同），方便明确追踪到未知组件的来源

第一种
```vue
<template>
  <MyWidget></MyWidget>
</template>

<script lang="ts">
import Vue from 'vue';
import MyWidget from '@/src/MyWidget/index.vue';
export default Vue.extend({
  components: {
    MyWidget
  }
})
```

第二种
```vue
<template>
  <my-name-box></my-name-box>
</template>

<script lang="ts">
import Vue from 'vue';
import MyWidget from '@/src/MyWidget/index.vue';
export default Vue.extend({
  components: {
    'my-name-box': MyWidget
  }
})
```
