## 题目地址

- [地址](https://www.nowcoder.com/practice/79b289947d854a759525dd937aa14762?tpId=98&tqId=32947&tPage=7&rp=7&ru=/ta/2019test&qru=/ta/2019test/question-ranking)

## 题目描述

```
有一个X*Y的网格，小团要在此网格上从左上角到右下角，只能走格点且只能向右或向下走。请设计一个算法，计算小团有多少种走法。给定两个正整数int x,int y，请返回小团的走法数目。

输入描述:
输入包括一行，空格隔开的两个正整数x和y，取值范围[1,10]。
输出描述:
输出一行，表示走法的数目

示例1
输入
3 2
输出
10
```

## 思路

## 关键点解析
- dp问题

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python
""""
动态规划，dp[x][y]表示所有走法的数目
到达x,y点的路径只有两条，从上边和从左边
dp[x][y] = dp[x - 1][y] + dp[x][y - 1]
边界 dp[0][y] = dp[x][0] = 1
"""
  
if __name__ == "__main__":
    n, m = map(int, input().strip().split())
    dp = [[1] * (m + 1) for _ in range(n + 1)]
    for i in range(1, n + 1):
        for j in range(1, m + 1):
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
    print(dp[n][m])

```

Java Code:

```java
 /** 思路：动态规划法
 * 第一行和第一列的走法全为1，其他空格的走法为上方空格的走法加上左方空格的走法，可以画表来直观的看出
 *
 * 注意点：
 * 只能在格点上走，也就是可以看成是（x+1）*（y+1）个格子，在格子上走
 **/
public class TheWayOfGrid {
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int x,y;
        x = scanner.nextInt();
        y = scanner.nextInt();

        // 首先定义一个二维数组，数组内的值为这点的走法
        int[][] ints = new int[x + 1][y + 1];
        // 初始化第一行全为1
        for(int i = 0;i < y + 1;i ++){
            ints[0][i] = 1;
        }
        // 初始化第一列全为1
        for(int i = 0;i < x + 1;i ++){
            ints[i][0] = 1;
        }
        // 从ints[1][1]起，这点的走法等于左方的点和上方的点的走法的和
        for(int i = 1;i < x + 1;i ++){
            for (int j = 1;j < y + 1;j ++) {
                ints[i][j] = ints[i - 1][j] + ints[i][j - 1];
            }
        }
        System.out.println(ints[x][y]);
    }
}
```

Javascript Code:

```js

```

## 扩展
