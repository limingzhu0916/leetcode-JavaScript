# Leetcode 题解 - 栈和队列
* [232.用栈实现队列](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#232用栈实现队列)

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

