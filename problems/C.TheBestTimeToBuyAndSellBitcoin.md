## 题目地址

- [地址](https://www.nowcoder.com/practice/08f70daa78bf45fea64d72523a3641f3?tpId=98&tqId=32862&tPage=2&rp=2&ru=/ta/2019test&qru=/ta/2019test/question-ranking)

## 题目描述

```
题目描述
给定一个正整数数组，它的第 i 个元素是比特币第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一次），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入比特币前卖出。

输入描述:
正整数数组，为以空格分隔的n个正整数
输出描述:
最大利润
示例1
输入
复制
7 1 5 3 6 4
输出
复制
5
```

## 思路
循环数组，找到最小的值的时候买入，找到最大利润的时候卖出
## 关键点解析

-

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python
```

Java Code:

```java
public class TheBestTimeToBuyAndSellBitcoin {

    public static void main(String[] args) {
        int[] prices = {7,1,5,3,6,4};
        System.out.println(maxBit(prices));
    }

    public static int maxBit(int[] prices){
        int min = Integer.MAX_VALUE; // 买入
        int max = 0; // 卖出
        for (int i = 0; i < prices.length; i ++) {
            min = Math.min(min,prices[i]); //找到最小值买入
            max = Math.max(max,prices[i] - min); //找到最大利润的时候卖出
        }
        return max;
    }

}
```

Javascript Code:

```js
```

## 扩展
