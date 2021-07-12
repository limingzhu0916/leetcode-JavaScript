# Leetcode 题解 - 树
 - [前中后序遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#前中后序遍历)
	 - [144.二叉树的前序遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#144二叉树的前序遍历)
	 - [145.二叉树的后序遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#145二叉树的后序遍历)
	 - [94.二叉树的中序遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#94二叉树的中序遍历)
- [序列化构造二叉树](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#序列化构造二叉树)
	- [105.从前序与中序遍历序列构造二叉树](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#105从前序与中序遍历序列构造二叉树)
	- [106.从中序与后序遍历序列构造二叉树](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#106从中序与后序遍历序列构造二叉树)
	- [889.根据前序和后序遍历构造二叉树](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#889根据前序和后序遍历构造二叉树)
	- [1008.前序遍历构造二叉搜索树](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#1008前序遍历构造二叉搜索树)
- [BFS遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#BFS遍历)
	- [102.二叉树的层序遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#102二叉树的层序遍历)
	- [513.找树左下角的值](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#513找树左下角的值)
	- [116.填充每个节点的下一个右侧节点指针](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#116填充每个节点的下一个右侧节点指针)
- [DFS遍历](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#DFS遍历)
	- [104.二叉树的最大深度](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#104二叉树的最大深度)
	- [剑指 Offer 34. 二叉树中和为某一值的路径](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#剑指-Offer-34二叉树中和为某一值的路径)
- [二叉树与链表](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#二叉树与链表)
	- [116.填充每个节点的下一个右侧节点指针](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#116填充每个节点的下一个右侧节点指针)
	- [117.填充每个节点的下一个右侧节点指针 II](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#117填充每个节点的下一个右侧节点指针II)
- [序列化与反序列化](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#序列化与反序列化)
	- [449.序列化和反序列化二叉搜索树](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#449序列化和反序列化二叉搜索树)
	- [297.二叉树的序列化与反序列化](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#297二叉树的序列化与反序列化)
- [其他](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#其他)
	- [1372.二叉树中的最长交错路径](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#1372二叉树中的最长交错路径)
	- [863.二叉树中所有距离为 K 的结点](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#863二叉树中所有距离为-K-的结点)
	- [98.验证二叉搜索树](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#98验证二叉搜索树)
	- [99.恢复二叉搜索树](https://github.com/limingzhu0916/leetcode-JavaScript/blob/main/notes/Leetcode-%E6%A0%91.md#99恢复二叉搜索树)

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
## 序列化构造二叉树
#### [105.从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
```javascript
var buildTree = function (preorder, inorder) {
    if (!preorder.length) return null
	// 使用map存储，方便查找
    let m = new Map()
    for (let i = 0; i < inorder.length; i++) {
        m.set(inorder[i], i)
    }
    const handle = (p_start, p_end, i_start, i_end) => {
        if (p_end < p_start) return null
        const root = new TreeNode(preorder[p_start])
        const mid = m.get(preorder[p_start])
        let leftNum = mid - i_start
        root.left = handle(p_start + 1, p_start + leftNum, i_start, mid - 1)
        root.right = handle(p_start + leftNum + 1, p_end, mid + 1, i_end)
        return root
    }

    return handle(0, preorder.length - 1, 0, inorder.length - 1)
}
```
#### [106.从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
```javascript
var buildTree = function (inorder, postorder) {
    if (!inorder.length) return null

    let m = new Map()
    for (let i = 0; i < inorder.length; i++) {
        m.set(inorder[i], i)
    }

    const handle = (i_start, i_end, p_start, p_end) => {
        if (p_start > p_end) return null
        const root = new TreeNode(postorder[p_end])
        const mid = m.get(postorder[p_end])
        const leftNum = mid - i_start
        root.left = handle(i_start, mid - 1, p_start, p_start + leftNum - 1)
        root.right = handle(mid + 1, i_end, p_start + leftNum, p_end - 1)
        return root
    }
    return handle(0, inorder.length - 1, 0, postorder.length - 1)
};
```
#### [889.根据前序和后序遍历构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)
```javascript
var constructFromPrePost = function (pre, post) {
    if (!pre.length) return null
    let m = new Map()
    for (let i = 0; i < post.length; i++) {
        m.set(post[i], i)
    }

    const handle = (pre_start, pre_end, post_start, post_end) => {
        if (pre_start > pre_end) return null
        const root = new TreeNode(pre[pre_start])
        if (pre_start == pre_end) return root
        const leftNum = m.get(pre[pre_start + 1]) - post_start
        root.left = handle(pre_start + 1, pre_start + 1 + leftNum, post_start, post_start + leftNum)
        root.right = handle(pre_start + 2 + leftNum, pre_end, post_start + leftNum + 1, post_end - 1)
        return root
    }
    return handle(0, pre.length - 1, 0, post.length - 1)
};
```
#### [1008.前序遍历构造二叉搜索树](https://leetcode-cn.com/problems/construct-binary-search-tree-from-preorder-traversal/)
```javascript
var bstFromPreorder = function (preorder) {
  const bulid = function (start, end) {
    if (start > end) return null
    const node = new TreeNode(preorder[start])
    if (start == end) return node
    // 比根节点大的值为右节点
    let left = end
    for (let i = start + 1; i <= end; i++) {
      if (preorder[start] < preorder[i]) {
        // 找到右节点的起始位置，就可以退出循环
        left = i - 1
        break
      }
    }
    // 继续递归
    node.left = bulid(start + 1, left)
    node.right = bulid(left + 1, end)
    return node
  }
  return bulid(0, preorder.length - 1)
}
```
## BFS遍历
#### [102.二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)
```javascript
var levelOrder = function (root) {
    if (!root) return []
    let ans = []
    let queue = [root]
    while(queue.length){
        let queueLen = queue.length
        ans.push([])
        for(let i = 0; i< queueLen; i++){
            let cur = queue.shift()
            ans[ans.length-1].push(cur.val)
            if(cur.left) queue.push(cur.left)
            if(cur.right) queue.push(cur.right)
        }
    }
    return ans
}
```
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
#### [116.填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)
BFS
```javascript
var connect = function (root) {
    if (!root) return null
    let queue = [root]
    let last = null
    let queueLen
    while (queue.length) {
        queueLen = queue.length
        for (let i = 0; i < queueLen; i++) {
            let cur = queue.shift()
            if (cur.left) {
                queue.push(cur.left)
                queue.push(cur.right)
            }
            if (i) {
                last.next = cur
            }
            last = cur
        }
    }
    return root
}
```
利用已经生成的链表遍历，由于不使用队列，可以减少内存空间
```javascript
var connect = function (root) {
    if (!root) return null

    let last = null
    let startNode = null
    const handle = (node) => {
        if (last) {
            last.next = node
        }
        if (!startNode) {
            startNode = node
        }
        last = node
    }

    let start = root
    while (start) {
        startNode = null
        last = null
        for (let p = start; p != null; p = p.next) {
            if (p.left) {
                handle(p.left)
                handle(p.right)
            }
        }
        start = startNode
    }
    return root
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
## 二叉树与链表
#### [116.填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)
```javascript
var connect = function (root) {
    if (!root) return null

    let last = null
    let startNode = null
    const handle = (node) => {
        if (last) {
            last.next = node
        }
        if (!startNode) {
            startNode = node
        }
        last = node
    }

    let start = root
    while (start) {
        startNode = null
        last = null
        for (let p = start; p != null; p = p.next) {
            if (p.left) {
                handle(p.left)
                handle(p.right)
            }
        }
        start = startNode
    }
    return root
}
```
#### [117.填充每个节点的下一个右侧节点指针II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)
```javascript
var connect = function (root) {
    if (!root) return null
    let queue = [root]
    let queueLen = null
    let last = null
    while (queue.length) {
        queueLen = queue.length
        for (let i = 0; i < queueLen; i++) {
            let cur = queue.shift()
            if(cur.left) queue.push(cur.left)
            if(cur.right) queue.push(cur.right)
            if(i) last.next = cur
            last = cur
        }
    }
    return root
}
```
## 序列化与反序列化
#### [449.序列化和反序列化二叉搜索树](https://leetcode-cn.com/problems/serialize-and-deserialize-bst/)
```javascript
var serialize = function (root) {
    // 后序遍历
    // 递归写法
    if (!root) return ''
    let ans = []
    const postTraversal = (root, ans) => {
        if (!root) return
        postTraversal(root.left, ans)
        postTraversal(root.right, ans)
        ans.push(root.val)
    }
    postTraversal(root, ans)
    return ans.join(',')
}

var deserialize = function (data) {
    if (data.length == 0) return null
    post = data.split(',').map(item => Number.parseInt(item))
    let inorder = [...post].sort((a, b) => a - b)
    // 从后序和中序遍历恢复树结构
    let m = new Map()
    for (let i = 0; i < inorder.length; i++) {
        m.set(inorder[i], i)
    }
    const buildTree = (i_start, i_end, p_start, p_end) => {
        if (i_start > i_end) return null
        const root = new TreeNode(post[p_end])
        const mid = m.get(post[p_end])
        const leftNum = mid - i_start
        root.left = buildTree(i_start, mid - 1, p_start, p_start + leftNum - 1)
        root.right = buildTree(mid + 1, i_end, p_start + leftNum, p_end - 1)
        return root
    }
    return buildTree(0, inorder.length - 1, 0, post.length - 1)
}
```
#### [297.二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)
```javascript
var serialize = function(root) {
    if(!root) return 'X'
    const left = serialize(root.left)
    const right = serialize(root.right)
    return root.val + ',' + left + ',' + right
}

var deserialize = function(data) {
    if(data.lenght == 0) return null
    data = data.split(',')
    const buildTree = (data) => {
        let cur = data.shift()
        if(cur === 'X') return null
        const root = new TreeNode(cur)
        root.left = buildTree(data)
        root.right = buildTree(data)
        return root
    }
    return buildTree(data)
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
#### [863.二叉树中所有距离为 K 的结点](https://leetcode-cn.com/problems/all-nodes-distance-k-in-binary-tree/)
```javascript
var distanceK = function (root, target, k) {
  let targetNode = null
  // 使用递归寻找target值的节点
  // 并保存目标值的父节点，方便向下查找
  const findTarget = function (root, target) {
    if (root.val === target) {
      targetNode = root
      return
    }
    if (root.left) {
      root.left.parent = root
      findTarget(root.left, target)
    }
    if (root.right) {
      root.right.parent = root
      findTarget(root.right, target)
    }
  }
  findTarget(root, target)
  // 目标节点向下遍历
  // path用来保存已经访问过的值
  let path = []
  let ans = []
  const findNode = function (node, k) {
    // 树遍历完或已经遍历过该节点
    if (!node || path.indexOf(node.val) !== -1) {
      return
    }
    path.push(node.val)
    if (k == 0){
      ans.push(node.val)
    }else{
      k--
      findNode(node.left, k)
      findNode(node.right, k)
    }
  }
  findNode(targetNode, k)
  // 从目标节点开始向上遍历
  while(targetNode.parent && k){
    targetNode = targetNode.parent
    // 向上走了一步，k--
    k--
    findNode(targetNode, k)
  }
  return ans
}
```
#### [98.验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)
```javascript
var isValidBST = function (root) {
  // 二叉搜索树的中序遍历是递增的
  // 此题可简化为求中序遍历结果，并在遍历过程中判断是否递增
  // 中序遍历有多种写法，这边是迭代写法
  if (!root) return false
  let stack = [root]
  let left = root.left
  while(left){
    stack.push(left)
    left = left.left
  }
  let pre = -Infinity
  while(stack.length){
    let cur = stack.pop()
    // 如果非递增，直接返回false
    if(pre > cur.val) return false
    pre = cur.val
    let right = cur.right
    while(right){
      stack.push(right)
      right = right.left
    }
  }
  return true
}
```
#### [99.恢复二叉搜索树](https://leetcode-cn.com/problems/recover-binary-search-tree/)
```javascript
var recoverTree = function(root) {
  // 题目思路：中序遍历过程中交换错误节点
  // 题目中提到只有两个节点被交换，因此两个节点要么相邻，要么不相邻
  let stack = [root]
  let left = root.left
  const swap = function (x, y) {
    // 交换
    let temp = x.val
    x.val = y.val
    y.val = temp
  }
  // 左节点先入栈
  while(left){
    stack.push(left)
    left = left.left
  }
  let pre = null
  let x = null, y = null
  while(stack.length){
    let cur = stack.pop()
    if(pre !== null && pre.val > cur.val){
      y = cur
      if(!x){
        x = pre
      }else{
        // 遍历到第二个错误节点
        break
      }
    }
    pre = cur
    let right = cur.right
    while(right){
      stack.push(right)
      right = right.left
    }
  }
  swap(x, y)
  return root
}
```