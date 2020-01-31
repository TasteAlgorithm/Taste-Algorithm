# 对字符串对应数组的 ASCII 并逆序排序

## 题目描述

**时间限制：C/C++语言 1000MS；其他语言 3000MS**
**内存限制：C/C++语言 65536KB；其他语言 589824KB**

```
求字符串`hello world`对应的ASCII码数组，并按照编码大小逆序
```

输入

```
字符串'hello world'
```

输出

```
ASCII数组[119,114,111,111,108,108,108,104,101,100,32]
```

样例输入

```
hello world
```

样例输出

```
119,114,111,111,108,108,108,104,101,100,32
```

温馨提示

## 思路
- 先将字符串分割为是一个个字符，并返回为一个新的数组
- 遍历数组中的每一个值通过charCodeAt转换为Unicode编码，返回一个新数组
- 再对应新数组进行降序操作

## 关键点解析

- 排序

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python

```

Java Code:

```java

```

Javascript Code:

```js
function ASCIIReverse(str) {
  return str
    .split("")
    .map(array => {
      return array.charCodeAt();
    })
    .sort((a, b) => b - a);
}
ASCIIReverse("hello world");
```

## 扩展
