題目：700. Search in a Binary Search Tree

> 連結：[Link](https://leetcode.com/problems/search-in-a-binary-search-tree/description/?envType=study-plan-v2&envId=leetcode-75)
> 難度：`Easy`
> 分類：[Tree](https://leetcode.com/tag/tree/)[Binary Search Tree](https://leetcode.com/tag/binary-search-tree/)[Binary Tree](https://leetcode.com/tag/binary-tree/)

#BinaryTree #leetcode

# 題目描述

[700. Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/)
You are given the `root` of a binary search tree (BST) and an integer `val`.

Find the node in the BST that the node's value equals `val` and return the subtree rooted with that node. If such a node does not exist, return `null`.

`Example 1`
![](https://assets.leetcode.com/uploads/2021/01/12/tree1.jpg)

**Input:** root = [4,2,7,1,3], val = 2
**Output:** [2,1,3]

## 理解問題

**產出 / Output：**
傳入一個 BST 及 val 至函數，在 BST 找尋節點值等於 val，若找到則回傳當前該節點的 tree，若否則回傳 null

# 解題思路

直覺透過`廣義優先搜尋(BFS)`去尋找，但忘了題目為 BST 以及其特性，並將空間複雜度由原先 O(n) 轉成 O(1)

## BST

BST 有一個特性為該左子節點的值永遠小於父節點的值，而右子節點的值永遠大於父節點的值。

## 解題步驟

- 定義一個 currentNode 的變數儲存當前處理的 node
- 定義一個 while 的迴圈判斷及處理當前情境
  - 判斷 currentNode 是否有值
  - 判斷 currentNode 的值是否等於傳入 val
  - 透過 currentNode 跟 val 比大小作為下個判斷的節點

## 程式碼

```js
var searchBST = function (root, val) {
  let currentNode = root;
  while (currentNode !== null) {
    if (currentNode.val === val) {
      return currentNode;
    } else if (val < currentNode.val) {
      currentNode = currentNode.left;
    } else {
      currentNode = currentNode.right;
    }
  }
  return null;
};
```

## Complexity

Time complexity: O(N)
Space complexity:O(1)
