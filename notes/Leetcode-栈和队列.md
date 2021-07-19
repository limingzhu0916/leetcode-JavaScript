# Leetcode 题解 - 栈和队列
* [232.用栈实现队列](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#232用栈实现队列)
* [225.用队列实现栈](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#225用队列实现栈)
* [155.最小栈](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-栈和队列.md#155最小栈)

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


