标题 | 思路 | 链接
---|---|---
二叉树中序遍历 |  stack({root,0\|1}) | [94](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
二叉树层序遍历 | queue 每 pop 一个,需要 push queue 个| [102](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)
二叉树最近公共祖先(二叉搜索树) | 或左找,或右找,否则就已找到 | [235](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
二叉树最近公共祖先(一般情况) | | [236](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)
堆排序 |buildheap 从右下到上依次 heapfy; 总控交换 root 与右下,再次 buildheap | [912](https://leetcode-cn.com/problems/sort-an-array/)
快排 | 开头返回,ij, privot=arr[i],驱动参数右界有界 | [912](https://leetcode-cn.com/problems/sort-an-array/)
最长公共子序列 |  | [1143](https://leetcode-cn.com/problems/longest-common-subsequence/)
3 sum | 排序,固定,双指针 | [15](https://leetcode-cn.com/problems/3sum/)
top k | | [215](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)
