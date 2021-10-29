> [剑指 Offer 32 - III. 从上到下打印二叉树 III - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

**例如:**
给定二叉树: `[3,9,20,null,null,15,7]`

        3
       / \
      9  20
        /  \
       15   7

返回其层次遍历结果：

```
[
  [3],
  [20,9],
  [15,7]
]
```



**提示：**

节点总数 <= 1000



**思路：**

用队列实现层序遍历。从队首取出元素并把左右子节点加入到队列中。

*注意*，由于需要之字形打印，需要用一个数组和一个变量来记录每一行的节点和行的奇偶性。

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrder = function (root) {
    if (!root) return []
    let queue = [root]
    let res = []
    let deep = 1
    while (queue.length) {
        let rows = []
        let iter = queue.length
        while (iter) {
            const node = queue.shift()
            // 奇数插队尾，偶数插队头
            if (deep & 1) rows.push(node.val)
            else rows.unshift(node.val)
            node.left && queue.push(node.left)
            node.right && queue.push(node.right)
            iter--
        }
        deep++
        res.push(rows)
    }
    return res
};
```

