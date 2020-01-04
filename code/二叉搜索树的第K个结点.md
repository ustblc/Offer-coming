#### 二叉搜索树的第k个结点

##### 题目描述

给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）  中，按结点数值大小顺序第三小结点的值为4。

<!--more-->

##### 法一：对于一颗二叉搜索树（也就是二叉排序树）进行中序遍历，就会得到一个递增的序列，所以要找第k小的结点，只需要中序遍历输出第k个结点即可。

```java
TreeNode KthNode(TreeNode pRoot, int k){
    if (pRoot == null) {
        return null;
    }
    Deque<TreeNode> nodes = new LinkedList<>();
    TreeNode p = pRoot;
    int count = 0;
    while (!nodes.isEmpty() || p != null) {
        while (p != null) {
            nodes.push(p);
            p = p.left;
        }
        p = nodes.pop();
        count++;
        if (count == k) {
            return p;
        }
        p = p.right;
    }
    return null;
}
```

