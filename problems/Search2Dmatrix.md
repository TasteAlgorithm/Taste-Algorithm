# 搜索二维矩阵
编写一个高效的算法来判断mxn矩阵中，是否存在一个目标值。 该矩阵具有如下特性:
- 每行中的整数从左到右按升序排列
- 每行的第一个整数大于前一行的最后一个整数
示例1:
```
输入:
matrix = [
[1，3， 5， 7]，
[10，11, 16, 20]，
[23，30, 34, 50]
target = 3
输出: true
```

示例2:
```
输入:
matrix = [
[1， 3， 5， 7],
[10，11, 16, 20],
[23，30，34, 50]
target = 13
输出: false
```

## 思路

## 关键点解析

- 递归

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python

```

Java Code:

```java
class Solution {
  public boolean searchMatrix(int[][] matrix, int target) {
      // 可以将矩阵看成一个数组，但是不用真的建立一个数组
        int m = matrix.length; // 矩阵的高
        if (m == 0){ //  空矩阵
            return false;
        }
        int n = matrix[0].length; // 矩阵的宽

        // 对数组进行二分查找
        int left = 0;
        int right = m * n - 1;
        int pivotIdx,pivotElement;
        while (left <= right){
            pivotIdx = (right + left)/2; // 中间点的下标
            pivotElement = matrix[pivotIdx/n][pivotIdx%n]; //从矩阵中找到值
            if (target == pivotElement) {
                return true;
            } else {
                if (target < pivotElement) {
                    right = pivotIdx - 1;
                }else {
                    left = pivotIdx + 1;
                }
            }
        }
        return false;
    }
}
```

Javascript Code:
```js

```

## 扩展