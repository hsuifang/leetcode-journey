# 872. Leaf-Similar Trees
#leetcode #tree

> 題目：872. Leaf-Similar Trees
> 連結：[Link](https://leetcode.com/problems/leaf-similar-trees/?envType=study-plan-v2&envId=leetcode-75)
> 難度：`Easy`
> 分類：[Tree](https://leetcode.com/tag/tree/)[Depth-First Search](https://leetcode.com/tag/depth-first-search/)[Binary Tree](https://leetcode.com/tag/binary-tree/)

# 題目描述
`原文`
Consider all the leaves of a binary tree, from left to right order, the values of those leaves form a **leaf value sequence**_._

For example, in the given tree above, the leaf value sequence is `(6, 7, 4, 9, 8)`.
Two binary trees are considered _leaf-similar_ if their leaf value sequence is the same.

Return `true` if and only if the two given trees with head nodes `root1` and `root2` are leaf-similar.

![](https://assets.leetcode.com/uploads/2020/09/03/leaf-similar-1.jpg)
(image from leetcode)

## 理解題目
- 假定每一個二元樹的所有的葉節點的值，是由左至右連續
- 給予兩個二元素比較兩個葉節點的是否相同

# 解題思路
- 所謂的二元樹為每個節點至多有兩個 children，分為左和右，一旦該節點沒有 children 則為所謂的葉節點 (leaf)。
- 最終每棵樹會回傳一個葉節點的List，List 為葉節點有左至右。 
- 比較兩棵樹的值是否完全一樣

## 解題步驟
### 找尋 Leaf Values
- 以根節點開始
- 如果該節點沒有左或右的孩子，則為葉節點，並依序儲存該資料
- 如果該節點有左邊孩子，則遞迴左邊孩子直到找到葉節點
- 如果該節點有右邊孩子，則遞迴右邊孩子直到找到葉節點

### 比較兩個二元樹的 leaf values 的值
- 長度是否相同
- 內容是否相同

## 程式碼
``` js
function TreeNode(val, left = null, right = null) { 
	this.val = val;
	this.left = left;
	this.right = right; 
}

function dfs (node, leaves) {
  if (!node) return;
  // 如果該節點沒有左或右的孩子，則為葉節點，並依序儲存該資料
  if (!node.left && !node.right) {
	  leaves.push(node.val)
  } else {
 	// 如果該節點有左邊孩子，則遞迴左邊孩子直到找到葉節點
    //如果該節點有右邊孩子，則遞迴右邊孩子直到找到葉節點
	  dfs(node.left, leaves)
	  dfs(node.right, leaves)
  }
}

/**
* @param {TreeNode} root1
* @param {TreeNode} root2
* @return {boolean}
*/

var leafSimilar = function(root1, root2) {
   let leaves1 = [], leaves2 = []
   dfs(root1, leaves1)
   dfs(root2, leaves2)
   return leaves1.length === leaves2.length && leaves1.every((v, i) => v === leaves2[i])
}; 
```

> Recursive DFS with generators - JavaScript 
> - [code](https://leetcode.com/problems/leaf-similar-trees/solutions/4536923/recursive-dfs-with-generators-javascript/?envType=study-plan-v2&envId=leetcode-75)
> - by [SylvainMarty](https://leetcode.com/SylvainMarty/)
# DFS & BFS
DFS(Depth-First Search,深度優先搜尋)和BFS(Breadth-First Search,廣度優先搜尋)都是用來搜尋樹或圖的演算法。

兩者的差異在於，DFS 會優先探索當前節點的子節點，而 BFS 會優先探索當前節點的相鄰節點。

[維基百科](https://zh.wikipedia.org/zh-tw/%E6%B7%B1%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2)
## Depth-First Search (DFS)
- 從一個起始節點開始，沿著一條路徑向下探索直到終點或無法探索; 接著返回上層節點繼續尋找其他路徑。
- 會把某一邊的路徑都走完才會走另一邊
- 實作上通常使用堆疊(Stack)這種資料結構作為輔助
- 優點是：節省記憶體、只需要追蹤目前路徑
- 缺點是：如果目標節點在底層，效率會比較差

> 如果有一個想像的漸變器，就是由左到右

## BFS(廣度優先搜尋)
- 從起點開始，先探索相鄰節點，再探索節點的相鄰節點，直到找到目標
- 實作上通常使用Queue這種資料結構作為輔助
- 優點是：如果目標在起點附近，可以快速找到
- 缺點是：如果節點太多，會消耗大量記憶體儲存探索節點

> 如果有一個想像的漸變器，就是由上到下
