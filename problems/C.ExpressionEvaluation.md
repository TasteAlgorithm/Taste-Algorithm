## 题目地址

- [地址](https://www.nowcoder.com/practice/3e483fe3c0bb447bb17ffb3eeeca78ba?tpId=98&tqId=32836&tPage=1&rp=1&ru=/ta/2019test&qru=/ta/2019test/question-ranking)

## 题目描述

```
题目描述
今天上课，老师教了小易怎么计算加法和乘法，乘法的优先级大于加法，但是如果一个运算加了括号，那么它的优先级是最高的。例如：
1+2*3=7
1*(2+3)=5
1*2*3=6
(1+2)*3=9
现在小易希望你帮他计算给定3个数a，b，c，在它们中间添加"+"， "*"， "("， ")"符号，能够获得的最大值。
输入描述:
一行三个数a，b，c (1 <= a, b, c <= 10)
输出描述:
能够获得的最大值
示例1
输入
复制
1 2 3
输出
复制
9
```

## 思路

## 关键点解析

-

## 代码

- 语言支持：Python，Java，JS
  Python Code:

```python
import sys
arr = list(map(int,sys.stdin.readline().split()))
arr.sort()
#第一个数若为1，则前两数先相加
if arr[0] == 1:
    print((arr[0]+arr[1])*arr[2])
#否则，三个数直接相乘
else:
    print(arr[0]*arr[1]*arr[2])

```

Java Code:

```java

```

Javascript Code:
**知识点：**

```js
let line = readline().split(" "); // 输入内容用空格分隔开
let arr = line.sort((a, b) => {
  return a - b;
}); // 进行正序排列
let result;
for (let i = 0; i < arr.length; i++) {
  if (arr[0] == "1") {
    result = (parseInt(arr[0]) + parseInt(arr[1])) * parseInt(arr[2]);
  } else {
    result = parseInt(arr[0]) * parseInt(arr[1]) * parseInt(arr[2]);
  }
}
print(result);
```

## 扩展
