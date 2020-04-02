## 题目地址

- [地址](https://www.nowcoder.com/question/next?pid=16516564&qid=362294&tid=32189245)

## 题目描述

```
时间限制：C/C++ 1秒，其他语言2秒
空间限制：C/C++ 32M，其他语言64M

Z国的货币系统包含面值1元、4元、16元、64元共计4种硬币，以及面值1024元的纸币。现在小Y使用1024元的纸币购买了一件价值为N(0<N<=1024)的商品，请问最少他会收到多少硬币？

输入描述:
一行，包含一个数N。

输出描述:
一行，包含一个数，表示最少收到的硬币数。

输入例子1:
200

输出例子1:
17

例子说明1:
花200，需要找零824块，找12个64元硬币，3个16元硬币，2个4元硬币即可。
```

## 思路

## 关键点解析

- 排序
- 贪心
- 递归
- 动态规划

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python

```

Java Code:

```java

```

Javascript Code:
**动态规划**


**贪心算法**
```js
function minCoinChange(amount) {
  const change = [];
  let coins = [1, 4, 16, 64],
    total = 0;
  for(let i = coins.length;i>=0;i--){
      // 将零钱从大到校开始遍历
      const coin = coins[i];
      while(total+coin<amount){
          // 找出去的零钱+遍历到的零钱<找钱总数时
          change.push(coin);
          total += coin; // 统计以找出零钱总和
      }
  }
  return change; // 返回找钱结果
}
console.log(minCoinChange(1024)); // 测试
```

## 扩展

使用贪心算法在有些情况无法得到最优解，本题是要求输出最少硬币数，所以这里不能用贪心！
- 如用[1, 3, 4]面额执行贪心算法找6元钱，会得到结果[4, 1, 1]
- 如用动态规划的解法，会得到最优的结果[3, 3]
