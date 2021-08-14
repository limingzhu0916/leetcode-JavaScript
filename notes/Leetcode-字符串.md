# Leetcode 题解 - 字符串
* [242.有效的字母异位词](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-字符串.md#242有效的字母异位词)
* [409.最长回文串](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-字符串.md#409最长回文串)

#### [242.有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/)
方法一：使用哈希表
```javascript
var isAnagram = function(s, t) {
  if(s.length !== t.length) return false
  let m = new Map()
  for(let l of s){
    if(m.has(l)){
      m.set(l, m.get(l) + 1)
    }else{
      m.set(l, 1)
    }
  }
  for(let l of t){
    if(m.get(l) == 0){
      return false
    }
    if(m.get(l) == 1){
      m.delete(l)
    }else{
      m.set(l, m.get(l) - 1)
    }
  }
  return !m.size
}
```
方法二：数组
```javascript
var isAnagram = function(s, t) {
  if(s.length !== t.length) return false
  let arr = new Array(26).fill(0)
  let aCode = 'a'.charCodeAt(0)
  for(let l of s){
    arr[l.charCodeAt(0) - aCode]++
  }
  for(let l of t){
    arr[l.charCodeAt(0) - aCode]--
  }
  for(let a of arr){
    if(a !== 0){
      return false
    }
  }
  return true
}
```
#### [409.最长回文串](https://leetcode-cn.com/problems/longest-palindrome/)
```javascript
var longestPalindrome = function(s) {
  let m = new Map()
  // 统计字母出现次数
  for(let l of s){
    if(m.has(l)){
      m.set(l, m.get(l)+1)
    }else{
      m.set(l, 1)
    }
  }
  let res = 0
  for(let item of m){
    // 凑偶数
    if(item[1] % 2 == 0){
      res += item[1]
    }else{
      res += (item[1] - 1)
    }
  }
  return res == s.length ? res : res + 1
}
```
