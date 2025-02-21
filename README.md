# 前端项目规范
为了统一团队代码风格，尽可能地使代码容易阅读，规定了部分代码规范:

1. 代码缩进用`2个空格`代替`tab`
2. 代码检测使用 `eslint`
3. 代码风格
    1. 代码风格不作要求
    1. 美化推荐使用 `prettier`风格（不做强制要求）
    1. 不要配置自动格式化所有文件（有时格式化结果并不理想）

详细目录:
1. [markdown语法参考](https://github.com/google/styleguide/blob/gh-pages/docguide/style.md#document-layout)
2. [项目结构](#项目结构)
3. [Javascript规范](#Javascript规范)
    1.  [命名规范](#命名规范)
    1.  [模块导出](#模块导出)
    1.  [慎用订阅模式](#慎用订阅模式)
    1.  [箭头函数](#箭头函数)
    1.  [JS注释](https://jsdoc.app/tags-param.html)
    1.  [TS注释](http://typedoc.org/tags/param/)
4.  [vue规范](#vue规范)
    1.  [组件文件结构](#组件文件结构)
    1.  [组件注册及使用](#组件注册及使用)
5.  [css规范](#css规范)
    

## 项目结构
```
env 环境变量配置
  ├── .env.development 开发模式
  ├── .env.production-test 生产模式：测试
  ├── .env.production 生产模式：正式
  └── .env.development[?-xxx] 其他环境变量配置
public
  ├── static - 静态文件（套一层static是为了防止和后端部署冲突后方便修改）
  ├──├── js - 脚本文件
  ├──├── css - 样式
  ├──├── files - 文件
  ├──├── images - 图片
  ├──├── fonts - 字体文件
  ├──├── json - json文件
  ├──├── demos - 测试相关
  └──└── plugins - 插件相关
src
  ├── components - 公共组件
  ├── utils - 工具集
  ├── styles - 样式相关
  ├── pages - 路由相关
  ├── request - http请求相关
  ├── services - 后端api接口
  ├── extends - 修改过的第三方扩展
  └── app.vue
index.html - 入口模板文件
vite.config.ts - 构建工具配置文件
package.json - 包文件
package-lock.json - 包版本锁定文件
README.md - 项目介绍
env.d.ts - 项目声明文件
tsconfig.json - ts配置文件
tsconfig.app.json - ts配置文件
tsconfig.app.json - ts配置文件
.gitignore - git忽略配置文件
... - 其它配置相关
```


## Javascript规范
- `明确声明`每一个文件中用到的所有资源，保证可以直接`跳转到引用`
- 养成按需引入的习惯，不要造成个别文件雍总
- 少写看上去高级，却不容易阅读的代码（交给构建工具去做），逻辑步骤要明确
- 不要将多个复杂语句写成一行代码
- 不要`三元运算`嵌套
- 使用了定时器 `setInterval` 和 `setTimeout` 必须有`清空`操作，不然导致无用实例堆积，可能出现意料之外的`bug`

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


### 模块导出

零散的方法，请按需导出，比如：
```javascript
export function A () {}

export function B () {}

export function C () {}
```

不要 `export default` 一大堆可能用不上的方法，不利于 `webpack` 体积优化
```javascript
export default {
  A: function () {},
  B: function () {},
  C: function () {}
}
```


### 慎用订阅模式

- 尽量少用`event bus`进行事件订阅，如果某些场景非用不可，请把订阅名取复杂一点
- 有`订阅`必须有`取消订阅`。重复订阅或者未销毁的订阅，不但影响性能，还会造成意料之外的`bug`

```javascript
// 订阅
bus.on('gEvent-demo', handler)

// 取消订阅
bus.off('gEvent-demo', handler)
```

### 箭头函数
箭头函数不要嵌套：
```javascript
const getInfo = () => () => () => () => {
  return true
}
```



## vue规范
- 禁止使用标签的 `全局样式`，造成不必要的样式重写，比如：
  ```css
  div, span, h1 {
    color: red;
  }
  ```
- 不允许将图片等`静态资源`放入`src`文件夹，请放在`public`文件夹里，通过静态服务访问
- 保持 `main.ts` 干净
- 不建议使用全局变量
- 不建议使用`vuex`或`pinia` 。（如果用：请把变量名取复杂一点，且不能同时存在）
- 不建议使用 `provide` 和 `injecet`。 （如果用：请把方法名取复杂一点）
- `vue3.x` 中不允许使用 `options api` 语法

### 组件文件结构
注：不允许是单文件组件 `YourWidget.vue`

```
YourWidget
    ├── pages <可选>文件夹：路由相关
    ├── components <可选>文件夹：用到的组件
    ├── styles 文件夹：<可选>样式相关
    ├── lib.ts <可选> 当前组件所分离的工具包
    └── index.vue 组件入口
```

### 组件注册及使用
导入时用的生么变量名，就使用什么标签
```vue
<template>
  <MyWidget></MyWidget>
</template>

<script lang="ts" setup>
import Vue from 'vue';
import MyWidget from '@/src/MyWidget/index.vue';
```

