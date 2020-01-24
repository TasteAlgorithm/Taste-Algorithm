## 题目地址

- [地址](https://www.nowcoder.com/practice/b31734e46ba644de85a9cf95bbd57a5f?tpId=98&tqId=32840&tPage=1&rp=1&ru=/ta/2019test&qru=/ta/2019test/question-ranking)

## 题目描述

```
给满出二叉树，编写算法将其转化为求和树

什么是求和树：二叉树的求和树， 是一颗同样结构的二叉树，其树中的每个节点将包含原始树中的左子树和右子树的和。

二叉树：
                  10
               /      \
             -2        6
           /   \      /  \
          8    -4    7    5

求和树：
                 20(4-2+12+6)
               /      \
           4(8-4)      12(7+5)
            /   \      /  \
          0      0    0    0

二叉树给出前序和中序输入，求和树要求中序输出；
所有处理数据不会大于int；

输入描述:
2行整数，第1行表示二叉树的前序遍历，第2行表示二叉树的中序遍历，以空格分割
输出描述:
1行整数，表示求和树的中序遍历，以空格分割
示例1
输入
复制
10 -2 8 -4 6 7 5 8 -2 -4 10 7 6 5
输出
复制
0 4 0 20 0 12 0
```

## 思路

二叉树加一个 sum 属性。
根据先序中序的序列，构建二叉树。
利用后序遍历来更新节点 sum 值。
最后通过中序遍历得到答案序列。

## 关键点解析

- 树

## 代码

- 语言支持：Python，Java，JS

Python Code:

```python

```

Java Code:

```java

class STNode {
    int val;
    int sum;
    STNode left = null;
    STNode right = null;

    public STNode(int val) {
        this.val = val;
    }
}

public class Main {
    static int[] preOrder;
    static int[] inOrder;
    static List<Integer> ans;    //存和的中序遍历。

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        String s1 = in.nextLine();
        String s2 = in.nextLine();
        String[] str1 = s1.split(" ");
        String[] str2 = s2.split(" ");
        int len = str1.length;
        preOrder = new int[len];
        inOrder = new int[len];
        for (int i = 0; i < len; i++) {
            preOrder[i] = Integer.parseInt(str1[i]);
        }
        for (int i = 0; i < len; i++) {
            inOrder[i] = Integer.parseInt(str2[i]);
        }
        STNode sroot = creatTree(0, 0, len - 1);
        sumNode(sroot);
        ans = new ArrayList<>();
        inOrderGo(sroot);
        for (int i : ans) {
            System.out.print(i + " ");
        }
        System.out.println();
    }

    //根据先序和中序遍历构建二叉树。
    static STNode creatTree(int root, int beg, int end) {
        if (beg > end) return null;
        STNode node = new STNode(preOrder[root]);
        int loc = 0;
        int cnt = 0;
        for (loc = beg; loc <= end; loc++) {
            cnt++;
            if (preOrder[root] == inOrder[loc])
                break;
        }
        node.left = creatTree(root + 1, beg, loc - 1);
        node.right = creatTree(root + cnt, loc + 1, end);
        return node;
    }

    //更新sum值。
    static void sumNode(STNode node) {
        if (node.left == null && node.right == null) {
            node.sum = 0;
        } else if (node.left == null) {
            sumNode(node.right);
            node.sum = node.right.sum + node.right.val;
        } else if (node.right == null) {
            sumNode(node.left);
            node.sum = node.left.sum + node.left.val;
        } else {
            sumNode(node.left);
            sumNode(node.right);
            node.sum = node.left.sum + node.left.val + node.right.sum + node.right.val;
        }
    }

     //中序遍历。
    static void inOrderGo(STNode node) {
        if (node == null) return;
        inOrderGo(node.left);
        ans.add(node.sum);
        inOrderGo(node.right);
    }

}
```

Javascript Code:

```js
var fir = readline()
  .split(" ")
  .map(Number);
var mid = readline()
  .split(" ")
  .map(Number);
function tree(p, m) {
  if (p.length === 0 || !p) {
    return null;
  }
  var root = {
    val: p[0],
    add: 0
  };
  var index = m.indexOf(p[0]);
  root.l = tree(p.slice(1, index + 1), m.slice(0, index));
  root.r = tree(p.slice(index + 1), m.slice(index + 1));
  if (root.l != null) root.add = root.add + root.l.val + root.l.add;
  if (root.r != null) root.add = root.add + root.r.val + root.r.add;
  return root;
}
var arr = [];
var t = tree(fir, mid);
function sum(t) {
  if (!t) {
    return;
  }
  sum(t.l);
  arr.push(t.add);
  sum(t.r);
}
sum(t);
print(arr.join(" "));
```

## 扩展
