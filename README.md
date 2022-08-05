# 前端技术规范

[markdown语法参考](https://github.com/google/styleguide/blob/gh-pages/docguide/style.md#document-layout)

为了同一团队代码风格，规定了部分代码规范:

1. 开发前请阅读本规范
2. 尽可能地使代码容易阅读

目录:
1.  [javascript规范](#javascript规范)
    1.  [命名规范](#命名规范)
    1.  [Add spacing to headings](#add-spacing-to-headings)

## javascript规范

### 命名规范

在`JavaScript`中使用两种变量命名
- `UpperCamelCase` 每个单词的首字母都大写，包含第一个单词。
- `lowerCamelCase` 除了第一个字母始终是小写（即使是缩略词），每个单词的首字母都大写。

`UpperCamelCase`： 类名、组件名、类型定义 都应该首字母大写

```typescript
class GoodStudent {}

const user: GoodStudent = new GoodStudent();

type Major = '语文' | '数学';

```

`lowerCamelCase`： 常量、普通变量每个单词首字母都应大写，并且不使用分隔符。

```javascript
var count = 13

let name = 'Jone'

const tokenName = 'user-token'

function getBasicInfo () {}
```