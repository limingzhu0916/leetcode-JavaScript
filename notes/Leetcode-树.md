# Leetcode 题解 - 树
 - 前中后序遍历
	 - 144.二叉树的前序遍历
	 - 145.二叉树的后序遍历
	 - 94.二叉树的中序遍历
- 序列化
	- 105.从前序与中序遍历序列构造二叉树
	- 106.从中序与后序遍历序列构造二叉树
	- 889.根据前序和后序遍历构造二叉树
- BFS遍历
	- 513.找树左下角的值
- DFS遍历
	- 104.二叉树的最大深度

## 前中后序遍历

##### [144.二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)
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
##### [145.二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)
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
##### [94.二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
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
