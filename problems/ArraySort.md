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
public class Soluction {
    public static void main(String[] args) {
        String str = "hello world";
        // 变成字符数组
        char[] chs = str.toCharArray();
        int[] cs = new int[chs.length];
        int n = 0;
        // 转成ascii码数组
        for (char ch : chs) {
            int c = ch;
            cs[n] = c;
            n++;
        }
       // 冒泡排序
        int i,j;
        for (i = 0;i < cs.length - 1;i++) {
            for (j = 0;j < cs.length - 1- i;j++) {
                if (cs[j] < cs[j + 1]) {
                    int temp = cs[j];
                    cs[j] = cs[j + 1];
                    cs[j + 1] = temp;
                }
            }
        }
        // 输出
        for(int m : cs){
            System.out.printf(m+" ");
        }
    }
}
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
