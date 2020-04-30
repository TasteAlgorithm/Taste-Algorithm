**来源：今日头条2019**
**时/空限制：3s / 64MB**

## 题目描述

```
机器人正在玩一个古老的基于DOS的游戏。
游戏中有N+1座建筑——从0到N编号，从左到右排列。
编号为0的建筑高度为0个单位，编号为 i 的建筑高度为H(i)个单位。
起初，机器人在编号为0的建筑处。
每一步，它跳到下一个（右边）建筑。
假设机器人在第k个建筑，且它现在的能量值是E，下一步它将跳到第k+1个建筑。
如果H(k+1)>E，那么机器人就失去H(k+1)-E的能量值，否则它将得到E-H(k+1)的能量值。
游戏目标是到达第N个建筑，在这个过程中能量值不能为负数个单位。
现在的问题是机器人以多少能量值开始游戏，才可以保证成功完成游戏？
```

### 输入格式
```
第一行输入整数N
第二行是N个空格分隔的整数，H(1),H(2),…,H(N)代表建筑物的高度
```

### 输出格式
```
输出一个整数，表示所需的最少单位的初始能量值
```

### 数据范围
```
1≤N<=10^5
1<H(i)≤10^5
```

### 输入样例1：
```
5
3 4 3 2 4
```
### 输出样例1：
```
4
```
### 输入样例2：
```
3
4 4 4
```
### 输出样例2：
```
4
```
### 输入样例3：
```
3
1 6 4
```
### 输出样例3：
```
3
```


## 思路
- 机器人从高点跳到低点就是增加能量（能量 + （能量 - 高度））
- 机器人从低点跳到高点就是减少能量（能量 - （高度 - 能量））
- 在给定的数据范围给的是0~10^5间用二分法来找到最合适的那个数据值，每次找到一个之后，就推算一遍看看这个能量值能不能跳到最后（跳到最后的条件就是能量值不会为负数）
- 用二分查找来找到最小能量值，start=0，end=max(H),高度小于能量值时，能量只增不减，最大值为max(H)
- 遍历建筑物，更新E值，若中间E小于0，则更新start=mid+1；
- 反之end=mid；
-  最后返回end


## 关键点解析
- 二分查找

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python
import math
N = int(input())
heights = list(map(int, input().split()))
if len(heights) == 0:
    print(0)
ans = 0 #最后的能量恰好为0，保证初始能量为最少
for i in range(len(heights) - 1,-1,-1):
    ans = math.ceil((heights[i] + ans) / 2)
print(math.ceil(ans))

```

Java Code:

```java
public class RobotJumpingProblem {
    public static void main(String[] args) {
        //输入所需要进行运算的值
        Scanner input = new Scanner(System.in);
        int N = input.nextInt();
        int[] H = new int[N+1];
        H[0] = 0;
        for(int i = 1; i < N+1; i++) {
            H[i] = input.nextInt();
        }
        //关闭输入
        input.close();
        System.out.println(Solution(N, H));
    }
    //写一个进行计算的方法方法
    public static int Solution(int N, int[] H) {
        int[] E = new int[N+1];
        E[N] = 0;
        for(int i = N; i > 0; i--) {
            E[i-1] = (H[i] + E[i] + 1) / 2;
        }
        return E[0];
    }

}
```

Javascript Code:
- [参考](https://www.acwing.com/solution/acwing/content/8410/)
- 如果h > E,那么 E = E - (h - E) = 2E - h
- 否则 E = E + E - h = 2E - h
假设当前位置为k，能量为E（k）。
当 H(k+1) > E（k）时，E（k+1）=E（k）-[H(k+1）-E（k）]
当 H(k+1) <= E（k）时，E（k+1）=E（k）+[E（k）-H(k+1）]
整理后两式均为： E（k+1）=2*E（k）-H(k+1）
E（k）=(E（k+1）+H(k+1))/2
**二分法**
```js
const N = 1e5+10; // 100010
let h[N],n; //h[N]记录塔高
check=(e)=>{
    for(let i =1;i<=n;i++){
        e=e*2-h[i];
        if(e>=1e5) return true;
        if(e<0) return false;
    }
    return true;
}
(function main(){
    for(let i=1;i<=n;i++){
        console.log(h[i]);
    }
    let l  =0;r = 1e5; //0-100000 在可选择范围内
    while(l<r){
        const mid = l+r;
        if(check(mid)){
            r = mid; // 找最小值，所以肯定是r=mid
        }else{
            l= mid+1;
        }
        console.log(r);
        return 0;
    }
})()
```

**总计公示**
```js
const arr = list(map(int,input().split()))
let E = 0
arr.reverse()
for(let H in arr){
    E = math.ceil((E+H)/2)
}
```


## 扩展
