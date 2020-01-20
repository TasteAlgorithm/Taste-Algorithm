# 创新题
## 题目描述
```
输入
包含多组测试数据，每组数组
第一行有三个正整数N，A，X分别表示bug的总数，喝一杯咖啡在一小时内debug效率的倍数，最多可以喝的咖啡数目。(1<=N<=100，1<=A<=8,1<=X<=8)
第二行有N个正整数，由空格分割开，第i个正整数ti表示解决第i个bug需要的分钟数(1<=ti<=1000)

输出
对于每组测试数据:
输出一个数字，如果不能解完所有bug，则输出0，如果可以，则输出最少需要的分钟数T(T为正整数，如不满一分钟则按一分钟计算，一旦超过8小时则认为不能解完)

示列1.
输入:
8 2 8
60 60 60 60 60 60 60 60
4 3 3
333 77 100 13

输出:
240
175
```

## 思路

## 关键点解析

- 深度优先搜索

## 代码

- 语言支持：Python，Java，JS
  Python Code:

```python

```

Java Code:

```java
public class TestDataSegmentation {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);

        int N = in.nextInt();  //bug的总数
        int A = in.nextInt();  //喝一杯咖啡在一小时内debug效率的倍数
        int X = in.nextInt();  //最多可以喝的咖啡数目
        int[] arr = new int[N];

        for(int i = 0 ; i < N ;i++) {
            arr[i] = in.nextInt();
        }
        System.out.println(coffee(N,A,X,arr));
    }

    /**
     *
     * @param N bug的总数
     * @param A 喝一杯咖啡在一小时内debug效率的倍数
     * @param X 最多可以喝的咖啡数目
     * @param arr 第i个正整数ti表示解决第i个bug需要的分钟数
     * @return
     */
    private static int coffee(int N,int A,int X,int[] arr) {
        int sum = 0; // 没喝咖啡前的debug时间总数
        for (int i = 0;i < arr.length;i++) {
            sum += arr[i];
        }
        int time1 = X*60*A; // 咖啡能维持的时间
        int time2 = (8-X) * 60; //剩余时间

        if (sum < time1) { // 表示一直加倍改bug中
           if (time1 % A != 0 ) {
               return sum / A +1;
           } else {
               return sum / A;
           }
        } else if ( time1 < sum && sum < time1 + time2) {
            return X * 60 + time2;  // 加倍的时间加上没加倍的时间
        } else {
            return 0; // 不能完成
        }
    }
}
```

Javascript Code:
**知识点：**

```js
```

## 扩展
