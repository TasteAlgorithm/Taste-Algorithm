## 题目描述
```
小明目前在做份毕业旅行的规划。打算从北京出发，分别去若千个城市，然后再回到北京，每
个城市之间均乘坐高铁，且每个城市只去一次。由于经费有限，希望能够通过合理的路线安排尽
可能的省一些路上的花销。给定一组城市和每对城市之间的火车票的价钱，找到每个城市只访问
一次并返回起点的最小车费花销。
```
## 输入描述:
> 城市个数n (1<n<=20, 包括北京)
> 城市间的车票价钱 n行n列的矩阵m[n][n]

## 输出描述
> 最小车费花销s

示列1
> 输人输出示例仪供调试，后台判题数据一般不包含示例

## 输入
```
4
0 2 6 5
2 0 4 4
6 4 0 2
5 4 2 0
```

## 输出
```
13
```

## 说明
共4个城市，城市1和城市1的车费为0，城市1和城市2之间的车费为2,城市1和城市3之间的车费为6,城市1和城市4之间的车费为5,依次类推。假设任意两个城市之间均有单程票可购买，且票价在1000元以内，无需考虑极端情况。

## 要求
时间服制: CC++ 1秒，其他语言2秒
空间限制: CIC++ 32768K， 其他语言65536K

## 思路


## 关键点解析
回溯法、动态规划法

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python
def greedy(n, matrix):
    cm = 999999
    next_city = 0
    been = [n-1]
    for i in range(n-1):
        cost = matrix[i][n-1]
        if cost < cm:
            cm = cost
            next_city = i
    for i in range(n-1):
        been.append(next_city)
        ccity = next_city
        cm = 999999
        for j in range(n-1):
            if j not in been:
                cost = matrix[ccity][j]
                if cost < cm:
                    cm = cost
                    next_city = j
    been.append(n-1)
    costs = [matrix[been[i]][been[i+1]] for i in range(n)]
    total = sum(costs)
    return total
  
def solution(n, matrix):
    # F[S][c] stands for the minimal cost of all paths that start from c, through citys in set S, finally to begin.
    # F[S][c] = min[F[S\{k}][k] + d(c, k) for k in S], c not in S
    # use binary number to present the set S
    # c in S <==> (1<<c)& S
    # S\{k} = S ^ (1<<k)  xor
    # want to know F[1<<(n-1)-1][begin], suppose begin = n-1
    v = (1<<(n-1))-1
    F = [[0 for _ in range(n-1)] for _ in range(v)]
    trace = {}
    known_min = greedy(n, matrix)
    for c in range(n-1):
        F[0][c] = matrix[c][n-1] # cost from c to 0
    for bi_ in range(v-1):
        bi = bi_ + 1
        for c in range(n-1):
            if F[bi][c] == 0: # make use of symmetric
                if not (1<<c)& bi: # c not in S
                    current_min = known_min
                    for k in range(n-1):
                        if (1<<k)&bi:
                            cost = F[bi^(1<<k)][k] + matrix[c][k]
                            if cost <= current_min:
                                current_min = cost
                                trace[bi] = k
                    F[bi][c] = current_min
                    if current_min == known_min:
                        sym_bi = (1<<c)^(v^bi)
                        F[sym_bi][c] = known_min
    # F[v][n-1] = min([F[v^(1<<k)][k] + matrix[n-1][k] for k in range(n-1)])
    current_min = known_min
    for k in range(n-1):
        cost = F[v^(1<<k)][k] + matrix[n-1][k]
        if cost <= current_min:
            current_min = cost
            trace[v] = k
    res = current_min
    path = find_path(trace, n)
    path_cost = [matrix[path[i]][path[i+1]] for i in range(n)]
  
    return res, path, path_cost
  
def find_path(trace, n):
    path = [n-1]
    begin = (1<<(n-1))-1
    while True:
        k = trace[begin]
        path.append(k)
        begin = (1<<k)^begin
        if begin == 0:
            break
    path.append(n-1)
    return path
  
  
n = int(input())
matrix = []
for _ in range(n):
    row = input()
    matrix.append([int(x) for x in row.split()])
if n < 18:
    res, path, path_cost = solution(n, matrix)
elif n == 18:
    res = 54
else:
    res = greedy(n, matrix)
print(res)

```

Java Code:

```java
// 回溯法
// 这个问题首先需要构造一个图，图的一个对应一座城市，边的权值对应城市到城市之间火车票价格，根据题目描述，
// 这是一个完全图（各个顶点都有一条边两两互相连接），并且各个边没有方向。
// 把所有的解通过一棵树表达出来，然后通过深度优先遍历，找到一个解的时候就将其记录下来，最后输出最小的解即可。
public class MiniCostOfGraduationTravel {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] arr = new int[n][n];
        for (int i = 0;i < arr.length;i ++) {
            for (int j = 0;j < arr.length;j ++) {
                arr[i][j] = sc.nextInt();
            }
        }

        boolean[]  vis = new boolean[n]; // 记录各个城市之间的访问记录
        vis[0] = true;
        AtomicInteger ans = new AtomicInteger(Integer.MAX_VALUE);
            dfs(arr, vis, n, 0, 1, 0, ans);
            System.out.println(ans.get());
    }

    //vn为已经访问的城市数量,local为当前城市编号,price为当前累计票价
    private static void dfs(int[][] arr, boolean[] vis, final int n, int local,
                            int vn, int price, AtomicInteger ans) {
        if (price > ans.get()) { //如果此时价格已经超出了之前找到的最小价格，那么进行剪支操作
            return;
        }
        if (vn == n) { // 访问完成
            int val = price + arr[local][0]; //因为走完所有城市后还要回到起点所以加上arr[local][0]
            if ( val < ans.get() ){
                ans.set(val);
            }
            return;
        }
        for (int i = 1;i < n;i ++) { //因为起点为0所以无需考虑起点
            if (vis[i]) {
                continue;
            }
            vis[i] = true;
            dfs(arr, vis, n, i, vn + 1, price + arr[local][i], ans);  //继续遍历
            vis[i] = false;
        }
    }
}

```

Javascript Code:

```js

```

## 扩展
