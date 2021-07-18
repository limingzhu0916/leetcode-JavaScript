# Leetcode 题解 - 堆
 	- [1046.最后一块石头的重量](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-堆.md#前中后序遍历)

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

