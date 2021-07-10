# Leetcode 题解 - 树
 - [前中后序遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#前中后序遍历)
	 - [144.二叉树的前序遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#144二叉树的前序遍历)
	 - [145.二叉树的后序遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#145二叉树的后序遍历)
	 - [94.二叉树的中序遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#94二叉树的中序遍历)
- 序列化
	- 105.从前序与中序遍历序列构造二叉树
	- 106.从中序与后序遍历序列构造二叉树
	- 889.根据前序和后序遍历构造二叉树
- [BFS遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#BFS遍历)
	- [513.找树左下角的值](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#513找树左下角的值)
- [DFS遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#DFS遍历)
	- [104.二叉树的最大深度](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#104二叉树的最大深度)
	- [剑指 Offer 34. 二叉树中和为某一值的路径](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#剑指-Offer-34二叉树中和为某一值的路径)
- [其他](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#其他)
	- [1372.二叉树中的最长交错路径](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#1372二叉树中的最长交错路径)

## 前中后序遍历

#### [144.二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)
迭代写法
```javascript
var preorderTraversal = function (root) {
  if (!root) return []
  
  let stack = [root]
  let ans = []
  while(stack.length){
    let cur = stack.pop()
    ans.push(cur.val)
    if (cur.right) {
      stack.push(cur.right)
    }
    if (cur.left) {
      stack.push(cur.left)
    }
  }
  return ans
}
```
递归写法
```javascript
var preorderTraversal = function (root) {
  if (!root) return []
  let ans = []
  const preorder = function (root, ans) {
    if (!root) return

    ans.push(root.val)
    preorder(root.left, ans)
    preorder(root.right, ans)
  }
  preorder(root, ans)
  return ans
}
```
#### [145.二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)
迭代写法
```javascript
var postorderTraversal = function (root) {
    if (!root) return []
    let stack = [root]
    let ans = []
    let p = root
    while (stack.length) {
        let cur = stack[stack.length - 1]
        if (cur.right == p || cur.left == p || (cur.right == null && cur.left == null)) {
            p = stack.pop()
            ans.push(p.val)
        } else {
            if (cur.right) {
                stack.push(cur.right)
            }
            if (cur.left) {
                stack.push(cur.left)
            }
        }
    }
    return ans
}
```
递归写法
```javascript
var postorderTraversal = function (root) {
    if (!root) return []
    let ans = []
    const postorder = (root, ans) => {
        if(!root) return
        postorder(root.left, ans)
        postorder(root.right, ans)
        ans.push(root.val)
    }
    postorder(root, ans)
    return ans
}
```
#### [94.二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
迭代写法
```javascript
var inorderTraversal = function (root) {
  if (!root) return []
  const stack = [root]
  const ret = []
  let left = root.left
  
  let item = null; // stack 中弹出的当前项

  while (left) {
    stack.push(left)
    left = left.left
  }

  while ((item = stack.pop())) {
    ret.push(item.val)
    let t = item.right

    while (t) {
      stack.push(t)
      t = t.left
    }
  }

  return ret
}
```
递归写法
```javascript
var inorderTraversal = function (root) {
  if (!root) return []
  let ans = []
  const inorder = function (root, ans) {
    if (!root) return
    inorder(root.left, ans)
    ans.push(root.val)
    inorder(root.right, ans)
  }
  inorder(root, ans)
  return ans
}
```
## BFS遍历
#### [513.找树左下角的值](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)
```javascript
var findBottomLeftValue = function (root) {
  let queue = [root]
  let ans
  while (queue.length) {
    let queueLen = queue.length
    for (let i = 0; i < queueLen; i++) {
      let cur = queue.shift()
      if(cur.left) queue.push(cur.left)
      if(cur.right) queue.push(cur.right)
      if(i == 0) ans = cur
    }
    if(queue.length == 0) return ans.val
  }
}
```
## DFS遍历
#### [104.二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)
```javascript
var maxDepth = function (root) {
  // 迭代
  if (!root) return 0
  let queue = [root]
  let depth = 0
  while (queue.length) {
    let queueLen = queue.length
    for (let i = 0; i < queueLen; i++) {
      let cur = queue.shift()
      if (cur.left) queue.push(cur.left)
      if (cur.right) queue.push(cur.right)
    }
    depth++
  }
  return depth
}
```
#### [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)
前序遍历+回溯
```javascript
var pathSum = function (root, target) {
    if (!root) return []
    const dfs = function (root, target, path, res) {
        if (!root) return
        // 选择
        path.push(root.val)
        // 判断
        if (!root.left && !root.right && target === root.val) {
            res.push([...path])
        } else {
        	// 递归
            dfs(root.left, target - root.val, path, res)
            dfs(root.right, target - root.val, path, res)
        }
        // 撤销选择
        path.pop()
    }
    let ans = [], path = []
    dfs(root, target, path, ans)
    return ans
}
```
## 其他
#### [1372.二叉树中的最长交错路径](https://leetcode-cn.com/problems/longest-zigzag-path-in-a-binary-tree/)
```javascript
var longestZigZag = function (root) {
  if (!root) return 0
  let res = -Infinity
  // 节点的右拐值 = 1 + 右子节点的左拐值
  // 节点的左拐值 = 1 + 左子节点的右拐值
  const dfs = function (root) {
    if (!root) return [-1, -1]
    const [ll, lr] = dfs(root.left)
    const [rl, rr] = dfs(root.right)
    res = Math.max(res, 1 + lr, 1 + rl)
    return [1 + lr, 1 + rl]
  }
  dfs(root)
  return res
}
```