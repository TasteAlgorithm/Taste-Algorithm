## 题目地址

- [地址](https://m.nowcoder.com/questions?uuid=bf877f837467488692be703735db84e6)

## 题目描述

```
- 牛牛准备参加学校组织的春游, 出发前牛牛准备往背包里装入一些零食, 牛牛的背包容量为w
- 牛牛家里一共有n袋零食, 第i袋零食体积为v[i]
- 牛牛想知道在总体积不超过背包容量的情况下,他一共有多少种零食放法(总体积为0也算一种放法)

输入描述:
输入包括两行
第一行为两个正整数n和w(1 <= n <= 30, 1 <= w <= 2 * 10^9),表示零食的数量和背包的容量。
第二行n个正整数v[i](0 <= v[i] <= 10^9),表示每袋零食的体积。

输出描述:
输出一个正整数, 表示牛牛一共有多少种零食放法。

示例1
输入
3 10
1 2 4
输出
8
说明
三种零食总体积小于10,于是每种零食有放入和不放入两种情况，一共有2*2*2 = 8种情况。
```

## 思路

## 关键点解析

- 队列

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
// **一共有多少种零食放法**
knapSack = (capacity, weights, values, n) => { // 容量 物品依次重量 物品依次价值 物品个数
  const kS = [];
  for (let i = 0; i <= n; i++) {
    kS[i] = [];
  }
  for(let i=0;i<=n;i++){
      for(let w =0;w<=capacity;w++){
          if(i===0||w===0){
              kS[i][w] = 0;
          }else if(weights[i-1]<=w){
              const a = values[i-1] + kS[i-1][w-weights[i-1]];
              const b = kS[i-1][w];
              kS[i][w] = a > b? a : b;
          }else{
              kS[i][w] = kS[i-1][w];
          }
      }
  }
  return kS[n][capacity];
};
```

## 扩展
