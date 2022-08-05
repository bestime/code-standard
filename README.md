# 前端技术规范



为了同一团队代码风格，规定了部分代码规范:

1. 开发前请阅读本规范
2. 尽可能地使代码容易阅读

目录:
1.  [markdown语法参考](https://github.com/google/styleguide/blob/gh-pages/docguide/style.md#document-layout)
2.  [JS/TS规范](#JS/TS规范)
    1.  [命名规范](#命名规范)
    1.  [对所有流控制结构使用花括号](#对所有流控制结构使用花括号)

## JS/TS规范

虽然前端流行不加分号，但还是建议养成行末添加分号的习惯 `";"`

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