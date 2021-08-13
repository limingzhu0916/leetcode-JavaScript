## 问题描述
给定一个无序数组arr, 其中元素可正、可负、可0。给定一个整数k，求arr所有连续子数组中累加和为k的最长子数组长度。保证至少存在一个合法的子数组。
##

>输入：[1,-2,1,1,1],0
返回值：3

## 方法分析
* 此题除了用暴力遍历求解，还有另外一个巧妙的方法，如下：
* 对于一个数组a，其中s[i] = a[0] + a[1] + ... + a[i]， s[j] = a[0] + a[1] + ... + a[j]。由于 i < j， 所以 **s[j] - s[i] = a[i + 1] + ... + a[j]**。该式表明数组前 j 项和 减去 数组前 i 项和 等于 数组第 i + 1 项到第 j 项的和。
* 该题求解数组中子数组和为k的最大子数组长度。假设a[i + 1] + ... + a[j] = k，那么子数组长度就是 j - i。 因此只需要计算 s[j] - s[i] = k 也就是求出满足 s[j] - k = s[i]的 i 和 j 。
* 因此只需要在遍历数组时，将累加和 s[i] 和对应的 i 存入哈希表中。并且在之后的遍历中，查找哈希表中是否存在满足 s[j] - k 的值。如果存在 那么 j - i 就是一个子数组长度

##题解
#### [NC125 未排序数组中累加和为给定值的最长子数组长度](https://www.nowcoder.com/practice/704c8388a82e42e58b7f5751ec943a11?tpId=196&&tqId=37127&rp=1&ru=/ta/job-code-total&qru=/ta/job-code-total/question-ranking)

```javascript
function maxlenEqualK( arr ,  k ) {
    // write code here
    let m = new Map()
    m.set(0, -1)
    let sum = 0
    let len = 0
    for(let i = 0; i < arr.length; i++){
        sum += arr[i]
        if(m.has(sum - k)){
            len = Math.max(len, i - m.get(sum - k))
        }
        if(!m.has(sum)){
            m.set(sum, i)
        }
    }
    return len
}
```
