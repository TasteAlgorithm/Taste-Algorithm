## 题目地址

- [地址](https://www.nowcoder.com/practice/a1792d443f914f2b928d2a157cd7900d?tpId=98&tqId=33003&tPage=9&rp=9&ru=/ta/2019test&qru=/ta/2019test/question-ranking)

## 题目描述

```
小明同学在参加一场考试，考试时间2个小时。试卷上一共有n道题目，小明要在规定时间内，完成一定数量的题目。  
考试中不限制试题作答顺序，对于第 i 道题目，小明有三种不同的策略可以选择:  
(1)直接跳过这道题目，不花费时间，本题得0分。
(2)只做一部分题目，花费pi分钟的时间，本题可以得到ai分。
(3)做完整个题目，花费qi分钟的时间，本题可以得到bi分。 
小明想知道，他最多能得到多少分。

输入描述:
第一行输入一个n数表示题目的数量。

接下来n行，每行四个数p_i，a_i，q_i，b_i。(1≤n≤100，1≤p_i≤q_i≤120，0≤a_i≤b_i≤1000)。
输出描述:
输出一个数，小明的最高得分。

示例1
输入
4
20 20 100 60
50 30 80 55
100 60 110 88
5 3 10 6
输出
94
```

## 思路

## 关键点解析
- 背包问题

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python

```

Java Code:

```java
public class TheStrategyOfTest {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n= Integer.parseInt(scanner.nextLine());
        // 存放数据，除n外，其他的数据可以用一个二维数组来存放
        int[][] record = new int[n][4];
        //接下来n行，每行四个数p_i，a_i，q_i，b_i
        for (int i = 0; i < n; i++) {
            String[] s = scanner.nextLine().split(" ");
            for (int j = 0; j < 4; j++) {
                record[i][j]=Integer.parseInt(s[j]);
            }
        }
        int[] dp=new int[121];
        for(int i = 0; i < n; i++)
            for(int j = 120; j >= 0; j--) {
                if(record[i][0] <= j) dp[j] = Math.max(dp[j], dp[j-record[i][0]] + record[i][1]);
                if(record[i][2] <= j) dp[j] = Math.max(dp[j], dp[j-record[i][2]] + record[i][3]);
            }
        System.out.println(dp[120]);
    }
}
```

Javascript Code:
**待理解**
```js
let N = parseInt(readline()); // readline()为牛客网针对传统ACM题的输入
let value = new Array(N).fill(0).map(()=> new Array(2).fill(0))
let weight = new Array(N).fill(0).map(()=> new Array(2).fill(0))
for(let i = 0 ; i < N ; i++){
    let line = readline().split(' ').map(e => +e);
    weight[i][0] = line[0]
    weight[i][1] = line[2]
    value[i][0] = line[1]
    value[i][1] = line[3]
}
let dp = new Array(121).fill(0);
for(let i = 0; i < N; i++) {
    for(let j = 120; j >= weight[i][0] || j >= weight[i][1]; j--) {
        if(j >= weight[i][0] && j >= weight[i][1]) {
            dp[j] = Math.max(Math.max(dp[j-weight[i][0]] + value[i][0], dp[j-weight[i][1]] + value[i][1]), dp[j]);
        }else if(j >= weight[i][0]) {
            dp[j] = Math.max(dp[j-weight[i][0]] + value[i][0], dp[j]);
        }else {
            dp[j] = Math.max(dp[j-weight[i][1]] + value[i][1], dp[j]);
        }
    }
}
console.log(dp[120]);
```

## 扩展
