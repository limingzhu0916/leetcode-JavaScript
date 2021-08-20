# Leetcode 题解 - 动态规划
 - [斐波那契数列](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#斐波那契数列)
	 - [70.爬楼梯](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#70爬楼梯)
	 - [198.打家劫舍](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#198打家劫舍)
	 - [213.打家劫舍II](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#213打家劫舍II)
- [矩阵](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#矩阵)
	 - [221.最大正方形](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#221最大正方形)

## * 斐波那契数列
#### [70.爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

> 爬 n 阶楼梯，每次可以爬 1 或 2 个台阶。那么爬上n阶楼梯前，要么是在 n-1 阶楼梯上，要么是在 n-2 阶楼梯上。所以可以写出
> f(n) = f(n - 1) + f(n - 2)。符合求解斐波那契数列。

方法一：递归。这道题会超时
方法二：定义数组 dp 纪录之前的值
```javascript
var climbStairs = function(n) {
    let dp = new Array(n + 1)
    dp[0] = dp[1] = 1
    for(let i = 2; i <= n; i++){
        dp[i] = dp[i - 1] + dp[i - 2]
    }
    return dp[n]
};
```
方法二的优化：由于最后的结果只与 n - 1 项和 n - 2项有关。所以可以用两个变量纪录
```javascript
var climbStairs = function(n) {
    if(n == 0 || n == 1) return 1
    let a = 1, b = 1
    let c
    for(let i = 2; i <= n; i++){
        c = b + a
        a = b
        b = c
    }
    return c
};
```
#### [198.打家劫舍](https://leetcode-cn.com/problems/house-robber/)

> 给定一个代表每个房屋存放金额的非负整数数组，在不触动警报装置的情况下，能够偷窃到的最高金额。 
> 如数组： [2,7,9,3,1]。偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。偷窃到的最高金额 = 2 + 9 + 1 = 12 。

解题诀窍在于找到动态规划方程。在偷窃一号房屋后，要么去 3 号房屋偷窃，要么去 4 号房屋偷窃。取决于 3 号和 4 号房屋金额大小。哪个房间钱多去哪。因此我们可以很自然的想到使用递归循环。但是此题会超时。

所以继续优化。当小偷偷到某一间房间 n，那他偷到的总金额大小，是  n 房间的钱 加  偷到（n - 2）房间时的总金额 或者 偷到（n - 3）房间时的总金额。取决于两个房间哪个钱多。因此我们可以将（n - 2）房间的钱 和（n - 3）房间的钱 在之前的遍历中纪录下来。
所以可以写出动态方程： 
dp[i] = nums[i] + Max(dp[i - 2], dp[i - 3])
```javascript
var rob = function (nums) {
    let dp = new Array(nums.length)
    for (let i = 0; i < nums.length; i++) {
        if (i >= 2) {
            if (i >= 3) {
                dp[i] = nums[i] + Math.max(dp[i - 2], dp[i - 3])
            } else {
                dp[i] = nums[i] + nums[i - 2]
            }
        } else {
            dp[i] = nums[i]
        }

    }
    return Math.max(...dp)
};
```
#### [213.打家劫舍II](https://leetcode-cn.com/problems/house-robber-ii/)
原理和上一题相同，但是由于是环形房屋，所以要分成两种情况讨论。
偷第一个房屋，就不能偷最后一个房屋
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function (nums) {
    if (nums.length == 1) {
        return nums[0]
    }
    if (nums.length == 2) {
        return Math.max(nums[0], nums[1])
    }
    const robByIndex = function (start, end) {
        let dp = new Array(end - start).fill(0)
        for (let i = start; i < end; i++) {
            if (i >= (2 + start)) {
                if (i >= (3 + start)) {
                    dp[i] = nums[i] + Math.max(dp[i - 2], dp[i - 3])
                } else {
                    dp[i] = nums[i] + dp[i - 2]
                }
            } else {
                dp[i] = nums[i]
            }
        }
        return Math.max(...dp)
    }
    // 偷了第一家，不偷最后一家
    return Math.max(robByIndex(0, nums.length - 1), robByIndex(1, nums.length))
};
```

## * 矩阵
#### [221.最大正方形](https://leetcode-cn.com/problems/maximal-square/)
方法一：暴力求解
```javascript
var maximalSquare = function (matrix) {
  let rowLength = matrix.length
  let colLength = matrix[0].length
  let res = 0
  for (let row = 0; row < rowLength; row++) {
    for (let col = 0; col < colLength; col++) {
      // 如果点大于0，则计算其最大可能的正方形
      let flag = true
      if (matrix[row][col] == '0') {
        continue
      } else {
        let maxLength = Math.min((rowLength - row), (colLength - col))
        if (maxLength == 1) {
          res = Math.max(res, maxLength)
          continue
        }
        // 在最大正方形内求解是否满足条件
        let i = row + 1
        let j = col + 1
        while (flag && i < row + maxLength) {
          if (matrix[i][j] == '0') {
            flag = false
          }
          // 向上检索
          let up = i - 1
          while (flag && up >= row) {
            if (matrix[up][j] == '0') {
              flag = false
              break
            }
            up--
          }
          // 向左检索
          let left = j - 1
          while (flag && left >= col) {
            if (matrix[i][left] == '0') {
              flag = false
              break
            }
            left--
          }
          if (flag) {
            res = Math.max(res, (i - row + 1) * (i - row + 1))
          } else {
            res = Math.max(1, res)
          }
          i++
          j++
        }
      }
    }
  }
  return res
};
```
方法二：动态规划
矩阵 [i, j] 点能否构成合格的正方形，取决于 [i -1, j - 1]、 [i -1, j]、 [i, j - 1]是否都是1。所以我们可以写出动态规划方程为：
当矩阵 [i, j] 点 为 ‘0’ , 不用考虑，dp(i, j) 为0
当矩阵 [i, j] 点 为 ‘1’ ，dp(i, j)=min(dp(i−1, j), dp(i−1, j−1), dp(i, j−1)) + 1
```javascript
var maximalSquare = function (matrix) {
    let row = matrix.length
    let col = matrix[0].length
    let dp = new Array(row).fill(0).map(() => new Array(col).fill(0))
    let res = 0
    for (let i = 0; i < row; i++) {
        for (let j = 0; j < col; j++) {
            if (i == 0 || j == 0) {
                dp[i][j] = +matrix[i][j]
            } else if (matrix[i][j] === '1') {
                dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j], dp[i][j - 1]) + (+matrix[i][j])
            }
        }
        res = Math.max(...dp[i], res)
    }
    return res * res
}
```
