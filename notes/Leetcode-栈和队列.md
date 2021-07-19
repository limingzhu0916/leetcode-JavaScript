# Leetcode 题解 - 栈和队列
* [232.用栈实现队列](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#232用栈实现队列)
* [225.用队列实现栈](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#225用队列实现栈)
* [155.最小栈](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#155最小栈)
* [20.有效的括号](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#20有效的括号)
* [739.每日温度](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#739每日温度)
* [503.下一个更大元素II](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#503下一个更大元素II)

#### [232.用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)
双栈
```javascript
/**
 * Initialize your data structure here.
 */
var MyQueue = function () {
    this.inStack = []
    this.outStack = []
};
/**
 * Push element x to the back of queue. 
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function (x) {
    this.inStack.push(x)
};
/**
 * Removes the element from in front of queue and returns that element.
 * @return {number}
 */
MyQueue.prototype.pop = function () {
    if (!this.outStack.length) {
        while (this.inStack.length) {
            this.outStack.push(this.inStack.pop())
        }
    }
    return this.outStack.pop()
};
/**
 * Get the front element.
 * @return {number}
 */
MyQueue.prototype.peek = function () {
    if(!this.outStack.length){
        while(this.inStack.length){
            this.outStack.push(this.inStack.pop())
        }
    }
    return this.outStack[this.outStack.length - 1]
};
/**
 * Returns whether the queue is empty.
 * @return {boolean}
 */
MyQueue.prototype.empty = function () {
    return !this.inStack.length && !this.outStack.length
};
```
#### [225.用队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues/)
```javascript
/**
 * Initialize your data structure here.
 */
var MyStack = function () {
    this.inQueue = []
    this.outQueue = []
};
/**
 * Push element x onto stack. 
 * @param {number} x
 * @return {void}
 */
MyStack.prototype.push = function (x) {
    this.inQueue.push(x)
};
/**
 * Removes the element on top of the stack and returns that element.
 * @return {number}
 */
MyStack.prototype.pop = function () {
    if (!this.inQueue.length) {
        while (this.outQueue.length) {
            this.inQueue.push(this.outQueue.shift())
        }
    }
    while (this.inQueue.length > 1) {
        this.outQueue.push(this.inQueue.shift())
    }
    return this.inQueue.shift()
};
/**
 * Get the top element.
 * @return {number}
 */
MyStack.prototype.top = function () {
    if (this.inQueue.length) {
        return this.inQueue[this.inQueue.length - 1]
    }else{
        return this.outQueue[this.outQueue.length - 1]
    }
};
/**
 * Returns whether the stack is empty.
 * @return {boolean}
 */
MyStack.prototype.empty = function () {
    return !this.inQueue.length && !this.outQueue.length
};
```
#### [155.最小栈](https://leetcode-cn.com/problems/min-stack/)
```javascript
/**
 * initialize your data structure here.
 */
var MinStack = function() {
    this.Stack = []
    this.minStack = [Infinity]
};
/** 
 * @param {number} val
 * @return {void}
 */
MinStack.prototype.push = function(val) {
    this.Stack.push(val)
    this.minStack.push(Math.min(this.minStack[this.minStack.length - 1], val))
};
/**
 * @return {void}
 */
MinStack.prototype.pop = function() {
    this.minStack.pop()
    return this.Stack.pop()
};
/**
 * @return {number}
 */
MinStack.prototype.top = function() {
    return this.Stack[this.Stack.length - 1]
};
/**
 * @return {number}
 */
MinStack.prototype.getMin = function() {
    return this.minStack[this.minStack.length - 1]
};
```
#### [20.有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)
```javascript
var isValid = function(s) {
  let stack = []
  for (let c of s) {
    if (c == '{') {
      stack.push('}')
    } else if (c == '[') {
      stack.push(']')
    } else if (c == '(') {
      stack.push(')')
    } else {
      if(c != stack.pop()){
        return false
      }
    }
  }
  return !stack.length
}
```
#### [739.每日温度](https://leetcode-cn.com/problems/daily-temperatures/)
维护一个栈用于存放温度的索引
```javascript
var dailyTemperatures = function (temp) {
  // stack用于存放温度值的索引
  let stack = []
  let res = new Array(temp.length).fill(0)
  // 因为要计算等几天才会有更高的温度，所以从后往前遍历
  for (let i = temp.length - 1; i >= 0; i--) {
    while (stack.length && temp[i] >= temp[stack[stack.length - 1]]) {
      // 如果当前遍历的温度比栈顶的高，则把栈顶的pop出去
      stack.pop()
    }
    if (stack.length) {
      // 栈顶的索引对应的温度，就是比当前遍历的温度更高的一个温度
      res[i] = stack[stack.length - 1] - i
    }
    stack.push(i)
  }
  return res
}
```
#### [503.下一个更大元素II](https://leetcode-cn.com/problems/next-greater-element-ii/)
```javascript
var nextGreaterElements = function (nums) {
  const len = nums.length
  let stack = []
  let res = new Array(len).fill(-1)
  // 由于要计算循环数组，一种方法是将其重复一次
  for (let i = 0; i < len * 2; i++) {
    // 因此求索引时需要除数组长度取余数
    // 当前遍历的数大于栈顶的数时，弹出栈顶元素的索引，该索引对应的位置放入当前遍历的数
    while (stack.length && nums[stack[stack.length - 1] % len] < nums[i % len]) {
      let index = stack.pop()
      if (index < len) {
        res[index] = nums[i % len]
      }
    }
    stack.push(i)
  }
  return res
}
```

