# Leetcode 题解 - 链表
* [25.K个一组翻转链表](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-链表.md#25K个一组翻转链表)

#### [25.K个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)
```javascript
var reverseKGroup = function(head, k) {
    // 因为要翻转头节点，所以定义一个哨兵节点指向头节点
    let dummy = new ListNode()
    dummy.next = head
    let start = dummy
    let end = head
    let count = 0
    while(end){
        count++
        // k个节点进行一次翻转
        if(count == k){
            start = reverseList(start, end.next)
            end = start.next
            count = 0
        }else{
            end = end.next
        }
    }
    // 翻转节点函数
    function reverseList(start, end){
        let pre = start
        let cur = start.next
        let first = cur
        while(cur !== end){
            let temp = cur.next
            cur.next = pre 
            pre = cur
            cur = temp
        }
        start.next = pre
        first.next = cur
        return first
    }

    return dummy.next
};
```
