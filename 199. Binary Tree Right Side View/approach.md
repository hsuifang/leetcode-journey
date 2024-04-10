題目：199. Binary Tree Right Side View

> 連結：[Link](https://leetcode.com/problems/binary-tree-right-side-view/description/?envType=study-plan-v2&envId=leetcode-75)
> 難度：`Medium`
> 分類：[Tree](https://leetcode.com/tag/tree/)[Depth-First Search](https://leetcode.com/tag/depth-first-search/)[Binary Tree](https://leetcode.com/tag/binary-tree/)[Breadth-First Search](https://leetcode.com/tag/breadth-first-search/)

#BinaryTree #leetcode

# 題目描述

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return *the values of the nodes you can see ordered from top to bottom*.
`Example 1`
![](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

**Input:** root = [1,2,3,null,5,null,4]
**Output:** [1,3,4]

## 理解問題

**產出 / Output：**
回傳一個清單，清單內的值是二元樹由上至下，每層最右邊的節點。

# 解題思路

可以透過 `廣度優先搜尋(BFS)`一層一層遍歷二元樹，每一層只取最右邊的節點。

## 解題步驟

### 初始化待處理 Queue

- 如果 root 沒有值則回傳空陣列
- 建立一個 變數 result 儲存每層最右邊節點
- 建立一個 queue 用來儲存每一層的節點
- 將 root 加入 queue

### 遍歷當前層

- 在遍歷前，先記錄當前層的長度
- 遍歷每一層的每個節點後，移除該節點
- 遍歷每一層，儲存該層最右邊的節點
- 遍歷每一層，依序將當前層的每個節點的子節點由左至右儲存至 queue
- 遍歷到 queue 為空

## 程式碼

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 * this.val = (val===undefined ? 0 : val)
 * this.left = (left===undefined ? null : left)
 * this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */

var rightSideView = function (root) {
  if (!root) return [];
  let queue = [root];
  // 建立一個 變數result 儲存每層最右邊節點
  let result = [];

  while (queue.length > 0) {
    let currentLength = queue.length;
    for (let i = 0; i < currentLength; i++) {
      // 遍歷每一層的每個節點後，移除該節點
      const currentNode = queue.shift();
      // 儲存最右邊
      if (i === currentLength - 1) {
        result.push(currentNode.val);
      }
      // 遍歷每一層，依序將當前層的每個節點的子節點由左至右儲存至queue
      if (currentNode.left) {
        queue.push(currentNode.left);
      }
      if (currentNode.right) {
        queue.push(currentNode.right);
      }
    }
  }
  return result;
};
```

## Complexity

**Time complexity: O(N)**

- 其中 N 是樹中節點的總數
- 每個節點都會被訪問一次

**Space complexity:O(n)**

- 取決於 Queue 中同時存在的節點數
- 最壞的情況下，樹的最後一層包含了約 N/2 個節點，因此空間複雜度為 O(N)
