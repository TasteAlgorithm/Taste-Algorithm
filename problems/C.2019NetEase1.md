## 题目地址

- [地址](https://www.nowcoder.com/practice/fc72d3493d7e4be883e931d507352a4a?tpId=98&tqId=32827&tPage=1&rp=1&ru=%2Fta%2F2019test&qru=%2Fta%2F2019test%2Fquestion-ranking)

## 题目描述

```
题目描述
牛牛去犇犇老师家补课，出门的时候面向北方，但是现在他迷路了。虽然他手里有一张地图，但是他需要知道自己面向哪个方向，请你帮帮他。
输入描述:
每个输入包含一个测试用例。
每个测试用例的第一行包含一个正整数，表示转方向的次数N(N<=1000)。
接下来的一行包含一个长度为N的字符串，由L和R组成，L表示向左转，R表示向右转。
输出描述:
输出牛牛最后面向的方向，N表示北，S表示南，E表示东，W表示西。
示例1
输入
复制
3
LRR
输出
复制
E
```

## 思路

## 关键点解析

-

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python

```

Java Code:

```java
// 先创建一个数组表示四个方向，然后向左的话下标减一，向右的话下标加一
// 如果下标小于0了加上4即可
public class Main{
    public static void main(String[] args){
        Scanner in = new Scanner(System.in);
        String[] dire = new String[]{"N", "E", "S", "W"};
        int n = in.nextInt();
        String s = in.next();
        int ret = 0;
        for(int i = 0; i < n; i ++){
            if(s.charAt(i) == 'R'){
                ret ++;
            }else{
                ret --;
            }
        }
        ret %= 4;
        if(ret < 0){
            ret += 4;
        }
        System.out.println(dire[ret]);
    }
}
```

Javascript Code:
**解法一**
```js
let dir=["N","E","S","W"];
let n=readline();
let turn=readline();
let k=0;
for(let i=0;i<turn.length;i++){
    if(turn[i]=="L"){
        k+=3;
    }else{
        k++;
    }
}
k=k%4;
console.log(dir[k]);
```
**解法二**
```js
readline();
let arr = ["N", "E", "S", "W"];
let now = 0;
let direct = readline().split('')
for (let i = 0; i < direct.length; i++) {
  if (direct[i] === "R") {
    now = now + 1 > 3 ? now - 3 : now + 1;
  } else {
    now = now - 1 < 0 ? now + 3 : now - 1;
  }
}
console.log(arr[now])
```
readline():逐行读取、写入文件内容（Read a single line from stdin）

## 扩展
