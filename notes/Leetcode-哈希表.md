# Leetcode 题解 - 哈希表
* [1.两数之和](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-哈希表.md#1两数之和)
* [217.存在重复元素](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-哈希表.md#217存在重复元素)
* [594.最长和谐子序列](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-哈希表.md#594最长和谐子序列)
* [128.最长连续序列](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-哈希表.md#128最长连续序列)

#### [1.两数之和](https://leetcode-cn.com/problems/two-sum/)
```javascript
var twoSum = function(nums, target) {
  let m = new Map()
  for (let i = 0; i < nums.length; i++) {
    if(m.has(target - nums[i])){
      return [m.get(target - nums[i]), i]
    }
    m.set(nums[i], i)
  }
  return []
}
```
#### [217.存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)
方法一：哈希表查重
```javascript
var containsDuplicate = function (nums) {
  let m = new Map()
  for (let i = 0; i < nums.length; i++) {
    if(m.has(nums[i])){
      return true
    }
    m.set(nums[i], i)
  }
  return false
}
```
方法二：先排序，再查找相邻元素是否相等
```javascript
var containsDuplicate = function (nums) {
  nums.sort((a, b) => a - b)
  for (let i = 1; i < nums.length; i++) {
    if (nums[i] == nums[i - 1]) {
      return true
    }
  }
  return false
}
```
#### [594.最长和谐子序列](https://leetcode-cn.com/problems/longest-harmonious-subsequence/)
方法一：暴力枚举
```javascript
var findLHS = function (nums) {
  // 暴力枚举
  let res = 0
  for (let i = 0; i < nums.length; i++) {
    let count = 0
    let flag = false
    for (let j = 0; j < nums.length; j++) {
      if(nums[j] - nums[i] == 1){
        flag = true
        count++
      }else if(nums[j] == nums[i]){
        count++
      }
    }
    if(flag){
      res = Math.max(res, count)
    }
  }
  return res
}
```
方法二：哈希表统计每个数出现的次数。再遍历哈希表，寻找比当前值大1的值，如果存在，则将二者次数相加
```javascript
var findLHS = function (nums) {
  let m = new Map()
  for (let n of nums) {
    if (m.has(n)) {
      m.set(n, m.get(n) + 1)
    }else{
      m.set(n, 1)
    }
  }
  let res = 0
  for(let [key, item] of m){
    if(m.has(key + 1)){
      res = Math.max(res, item + m.get(key + 1))
    }
  }
  return res
}
```
#### [128.最长连续序列](https://leetcode-cn.com/problems/longest-consecutive-sequence/)
方法一：使用Set
```javascript
var longestConsecutive = function (nums) {
  // 集合用于去重
  let s = new Set(nums)
  for(let n of nums){
    s.add(n)
  }
  let res = 0
  for(let num of s){
    // 如果num - 1不存在，说明num是连续序列起点
    if(!s.has(num - 1)){
      let count = 0
      while(s.has(num)){
        num++
        count++
      }
      res = Math.max(res, count)
    }
  }
  return res
}
```
方法二：使用哈希表，一次遍历即可，表中key存当前遍历的值num，value存当前num的连续长度。当前num的连续长度=(num-1)的连续长度+1+(num+1)的连续长度
```javascript
const longestConsecutive = function (nums) {
  let m = new Map()
  let max = 0
  for (let n of nums) {
    // 判断m中是否已经有当前遍历的数值
    if (!m.has(n)) {
      let preLen = m.get(n - 1) || 0
      let nextLen = m.get(n + 1) || 0
      let curLen = preLen + 1 + nextLen
      m.set(n, curLen)
      max = Math.max(max, curLen)  // 更新最大长度
      m.set(n - preLen, curLen) // 更新新序列的左端数字的value
      m.set(n + nextLen, curLen) // 更新新序列的右端数字的value
    }
  }
  return max
}
```
