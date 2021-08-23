# Leetcode 题解 - 动态规划
 - [斐波那契数列](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#斐波那契数列)
	 - [70.爬楼梯](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#70爬楼梯)
	 - [爬楼梯扩展问题](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#爬楼梯扩展问题)
	 - [198.打家劫舍](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#198打家劫舍)
	 - [213.打家劫舍II](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#213打家劫舍II)
- [矩阵](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#矩阵)
	 - [221.最大正方形](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#221最大正方形)
	 - [64.最小路径和](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#64最小路径和)
	 - [62.不同路径](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#62不同路径)
- [数组区间](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#数组区间)
	 - [413.等差数列划分](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#413等差数列划分)
	 - [300.最长递增子序列](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#300最长递增子序列)
	 - [354.俄罗斯套娃信封问题](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#354俄罗斯套娃信封问题)
- [分割整数](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#分割整数)
	 - [343.整数拆分](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-动态规划.md#343整数拆分)

## 斐波那契数列
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
#### [爬楼梯扩展问题](https://www.nowcoder.com/practice/22243d016f6b47f2a6928b4313c85387?tpId=13&tags=&title=&difficulty=0&judgeStatus=0&rp=1)

> 一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶(n为正整数)总共有多少种跳法。

假设青蛙在 n 级台阶，那么它可能是从 n - 1 级台阶上来的，也可能是 n - 2 级台阶上来的，或者 n - 3 级台阶.......，或者 0 级台阶上来的。
于是可以写出动态规划方程：
f(n) = f(n - 1) + f(n - 2) + ····· + f(0) 
继续观察可以发现：
f(n - 1) = f(n - 2) + f(n - 3) + ····· + f(0) 
也就是说 f(n) = f(n - 1)  + f(n - 1) = 2 * f(n - 1)

```javascript
function jumpFloorII(number){
    // write code here
    let pre = 1
    let ans
    for(let i = 2; i <= number; i++){
    // 左移乘2
        ans = pre << 1
        pre = ans
    }
    return pre
}
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

## 矩阵
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

#### [64.最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)

> 给定一个包含非负整数的 m x n 网格 grid ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

矩阵中第一行的元素，只能是从左边走来
矩阵中第一列的元素，只能是从上面走来
而矩阵中的元素（除第一行、第一列）要么是从上面走下来，要么是从左边走过来。从哪边下来取决于哪边的值小。
于是我们可以写出动态规划方程：
i = 0时，dp(i, j) = dp(i - 1, j) + grid(i, j)
j = 0时，dp(i, j) = dp(i, j - 1) + grid(i, j)
i > 1, j > 1时，dp(i, j) = Math.min(dp(i - 1, j), dp(i, j - 1)) + grid(i, j)

```javascript
var minPathSum = function(grid) {
    let row = grid.length
    let col = grid[0].length
    let dp = new Array(row).fill(0).map(() => new Array(col).fill(0))
    dp[0][0] = grid[0][0]
    for(let i = 0, j = 1; j < col; j++){
        dp[i][j] = grid[i][j] + dp[i][j - 1]
    }
    for(let i = 1, j = 0; i < row; i++){
        dp[i][j] = grid[i][j] + dp[i - 1][j]
    }
    for(let i = 1; i < row; i++){
        for(let j = 1; j < col; j++){
            dp[i][j] = grid[i][j] + Math.min(dp[i - 1][j], dp[i][j - 1])
        }
    }
    return dp[row - 1][col - 1]
};
```
#### [62.不同路径](https://leetcode-cn.com/problems/unique-paths/)

> 一个机器人位于一个 m x n 网格的左上角。机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角。
问总共有多少条不同的路径？

思路与上一题很像，不同的是这题要统计路径总数。依旧可以分成三种情况
* 当走在第一行的元素上时，只能是从左边走过来，所以第一行上的路径条数都是1
* 当走在第一列的元素上时，只能是从上面走下来，所以第一列上的路径条数都是1
* 当走到矩阵内部时，要么从上面走下来，要么从左边走过来，所以路径总数应该是上面元素的路径总数加上左边元素的路径总数

因此，动态规划方程可以写为：
i = 0时，dp(i, j) = 1
j = 0时，dp(i, j) = 1
i > 1, j > 1时，dp(i, j) = dp(i - 1, j) + dp(i, j - 1)
```javascript
var uniquePaths = function(m, n) {
    let dp = new Array(m).fill(0).map(() => new Array(n).fill(0))
    dp[0][0] = 1
    for(let i = 0, j = 1; j < n; j++){
        dp[i][j] = 1
    }
    for(let i = 1, j = 0; i < m; i++){
        dp[i][j] = 1
    }
    for(let i = 1; i < m; i++){
        for(let j = 1; j < n; j++){
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        }
    }
    return dp[m - 1][n - 1]
};
```

## 数组区间
#### [413.等差数列划分](https://leetcode-cn.com/problems/arithmetic-slices/)

> 如果一个数列 至少有三个元素 ，并且任意两个相邻元素之差相同，则称该数列为等差数列。给你一个整数数组 nums ，返回数组 nums 中所有为等差数组的 子数组 个数。

等差数组满足 nums[i] - nums[i - 1] = nums[i - 1] - nums[i - 2]。如数组[1, 2, 3]为等差数组，子数组为1。当在其后面添加一个数字4。由于数字4满足等差数组公式，因此和数组[1, 2, 3]构成等差数组。
子数组个数 = 数组[1, 2, 3]的子数组个数 + 添加4后增加的子数组数。
添加4的子数组增加的子数组为 [2, 3, 4] 、[1, 2, 3, 4]
因此可以定义动态规划方程为：
满足nums[i] - nums[i - 1] = nums[i - 1] - nums[i - 2]时，dp[i] = dp[i - 1] + 1
```javascript
var numberOfArithmeticSlices = function(nums) {
    if(nums.length < 3) return 0
    let dp = new Array(nums.length).fill(0)
    for(let i = 2; i < nums.length; i++){
        if(nums[i - 1] - nums[i - 2] == nums[i] - nums[i - 1]){
            dp[i] = dp[i - 1] + 1
        }
    }
    return dp.reduce((prevalue, curvalue) => {
        return curvalue + prevalue
    })
};
```
#### [300.最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)
```javascript
var lengthOfLIS = function(nums) {
    let dp = new Array(nums.length).fill(1)
    for(let i = 0; i < nums.length; i++){
        // 从 i 点往前统计有多少个小于nums[i]的值
        for(let j = 0; j < i; j++){
            if(nums[j] < nums[i]){
                // 小于则将dp[j] + 1, 并与dp[i]相比取最大值
                dp[i] = Math.max(dp[j] + 1, dp[i])
            }
        }
    }
    return Math.max(...dp)
};
```
#### [354.俄罗斯套娃信封问题](https://leetcode-cn.com/problems/russian-doll-envelopes/)
该问题可以简化为：
* 将数组排序，0维度按升序排列，0维度相等按照降序排列。（由于0维度相等的数组只能取一个，所以降序排列是为了第二步不出问题）
* 对排序后的数组求最长递增子序列（也就是上一题的思路）
```javascript
var maxEnvelopes = function (envelopes) {
    // 对数组排序，0维度按升序排列，0维度相等按照降序排列
    envelopes.sort((a, b) => {
        if (a[0] == b[0]) {
            return b[1] - a[1]
        }else{
            return a[0] - b[0]
        }
    })
    // 求排序后数组的最长子序列
    let dp = new Array(envelopes.length).fill(1)
    for(let i = 0; i < envelopes.length; i++){
        for(let j = 0; j < i; j++){
            if(envelopes[j][1] < envelopes[i][1]){
                dp[i] = Math.max(dp[i], dp[j] + 1)
            }
        }
    }
    return Math.max(...dp)
};
```

## 分割整数
#### [343.整数拆分](https://leetcode-cn.com/problems/integer-break/)
```javascript
var integerBreak = function (n) {
    let dp = new Array(n + 1).fill(0)
    dp[2] = 1
    for(let i = 3; i <= n; i++){
        for(let j = 1; j < i; j++){
            dp[i] = Math.max(dp[i], j * (i - j), j * dp[i - j])
        }
    }
    return dp[n]
};
```
