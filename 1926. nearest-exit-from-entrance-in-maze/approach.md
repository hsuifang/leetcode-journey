題目：199. nearest-exit-from-entrance-in-maze

> 連結：[Link](https://leetcode.com/problems/nearest-exit-from-entrance-in-maze/submissions/?envType=study-plan-v2&envId=leetcode-75)
> 難度：`Medium`
> 分類：[Breadth-First Search](https://leetcode.com/tag/breadth-first-search/)

#leetcode #BFS

# 題目描述

You are given an `m x n` matrix `maze` (**0-indexed**) with empty cells (represented as `'.'`) and walls (represented as `'+'`). You are also given the `entrance` of the maze, where `entrance = [entrancerow, entrancecol]` denotes the row and column of the cell you are initially standing at.

In one step, you can move one cell **up**, **down**, **left**, or **right**. You cannot step into a cell with a wall, and you cannot step outside the maze. Your goal is to find the **nearest exit** from the `entrance`. An **exit** is defined as an **empty cell** that is at the **border** of the `maze`. The `entrance` **does not count** as an exit.

Return *the **number of steps** in the shortest path from the* `entrance` *to the nearest exit, or* `-1` *if no such path exists*.`

**Example 1**
![s](https://assets.leetcode.com/uploads/2021/06/04/nearest1-grid.jpg)

**Input:** maze = `[["+","+",".","+"],[".",".",".","+"],["+","+","+","."]], entrance = [1,2]`
**Output:** 1
**Explanation:** There are 3 exits in this maze at [1,0], [0,2], and [2,3].
Initially, you are at the entrance cell [1,2].

- You can reach [1,0] by moving 2 steps left.
- You can reach [0,2] by moving 1 step up.
  It is impossible to reach [2,3] from the entrance.
  Thus, the nearest exit is [0,2], which is 1 step away.

## 理解問題

**產出 / Output：**
回傳從起點到出口的最小步數，如果是死路則回傳 -1

# 解題思路

可以透過 `廣度優先搜尋(BFS)`一層一層確認四周的格子是終點、牆或是可以行走的路

## 解題步驟

- 定義一個待處理的 queue 、方向
  - 每個 queue 會存取的內容為 `[row, col, 從entrance 走到的步數]`
- 將 entrance 作為 queue 第一個要執行
- 當 dequeue 出來的值是出口則回傳 step
- 否則則透過 dequeue 值去取得當前位置四周可走的位置，並加入 queue
- 當 queue 已經空時，則回傳 -1

## 程式碼

```js
/**

* @param {character[][]} maze
* @param {number[]} entrance
* @return {number}
*/

var nearestExit = function (maze, entrance) {
  const WALL = "+",
    VISITED = "visited";
  // initialize a queue for BFS
  const [entranceRow, entranceCol] = entrance;
  const queue = [[entranceRow, entranceCol, 0]]; // Queue will store [row, col, steps

  // Define directions for movement:
  const directions = [
    [-1, 0],
    [1, 0],
    [0, -1],
    [0, 1],
  ]; // Up, down, left, right

  const isExit = (row, col) => {
    // 邊邊 && 不是 entrance
    const isBorder =
      row === 0 ||
      col === 0 ||
      row === maze.length - 1 ||
      col === maze[0].length - 1;
    const isNotEntrance = !(row === entrance[0] && col === entrance[1]);
    return isBorder && isNotEntrance;
  };

  while (queue.length) {
    const [row, col, steps] = queue.shift(); // Dequeue the first cell
    if (isExit(row, col)) {
      return steps;
    }
    // 周圍有沒有可以拜訪的
    // 有的話加入 queue

    for (const [dirX, dirY] of directions) {
      let [neighborRow, neighborCol] = [row + dirX, col + dirY];
      let inBounds = (row, col) =>
        row >= 0 && row < maze.length && col >= 0 && col < maze[0].length;
      if (
        inBounds(neighborRow, neighborCol) &&
        maze[neighborRow][neighborCol] !== WALL
      ) {
        maze[neighborRow][neighborCol] = VISITED;
        queue.push([neighborRow, neighborCol, steps + 1]); // Enqueue adjacent cell
      }
    }
  }

  return -1;
};
```

## Complexity

**Time complexity: O(M x N)**
**Space complexity:O(MxN)**

- 紀錄 Queue
