# Leetcode 题解 - 堆
* [1046.最后一块石头的重量](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-堆.md#1046最后一块石头的重量)
* [313.超级丑数](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-堆.md#313超级丑数)

#### [1046.最后一块石头的重量](https://leetcode-cn.com/problems/last-stone-weight/)
sort函数 + 递归
```javascript
var lastStoneWeight = function (stones) {
  stones.sort((a, b) => a - b)
  if(stones.length > 1){
    let res = stones.pop() - stones.pop()
    if(res) stones.push(res)
    return lastStoneWeight(stones)
  }
  return stones.length ? stones.pop() : 0 
}
```
最大堆
```javascript
var lastStoneWeight = function (stones) {
  const priQueue = new MaxPriorityQueue()
    for (let stone of stones) {
        priQueue.enqueue('x', stone)
    }
    while (priQueue.size() > 1) {
        const x = priQueue.dequeue()['priority']
        const y = priQueue.dequeue()['priority']
        if (x > y) priQueue.enqueue('x', x - y)
    }
    return priQueue.size() ? priQueue.dequeue()['priority'] : 0
}
```
#### [313.超级丑数](https://leetcode-cn.com/problems/super-ugly-number/)
最小堆
```javascript
var nthSuperUglyNumber = function (n, primes) {
  const priQueue = new MinPriorityQueue()
  let ans = 1
  let count = 0
  // map纪录，避免重复
  let m = new Map()
  priQueue.enqueue('x', ans)
  while (count < n) {
      ans = priQueue.dequeue()['priority']
      count++
      // 入堆
      for (let i = 0; i < primes.length; i++) {
          let res = ans * primes[i]
          if(!m.get(res)){
              priQueue.enqueue('x', res)
              m.set(res, 1)
          }
      }
  }
  return ans
}
```

