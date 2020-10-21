## Coding Interview Prep

---
### Height of a Binary Tree
The height of a binary tree is the number of edges between the tree's root and its furthest leaf. For example, the following binary tree is of height 2.
![Description](https://s3.amazonaws.com/hr-assets/0/1527626183-88c8070977-isitBSTSample0.png)
#### Function Description
Complete the `getHeight` or *height* function in the editor. It must return the height of a binary tree as an integer.
getHeight or height has the following parameter(s):
- *root*: a reference to the root of a binary tree.
**Note**: the height of binary tree with single node is taken as zero.
#### INPUT FORMAT
The first line contains an integer ***n***, the number of nodes in the tree.
Next line contains ***n*** space separated integer where ***i***th integer denotes node[i].data. 
**Note**: Node values are inserted into a binary search tree before a reference to the tree's root node is passed to your function. In a binary search tree, all nodes on the left branch of a node are less than the node value. All values on the right branch are greater than the node value.

#### CONSTRAINTS
- 1 ≤ ***node.data[i]*** ≤ 20
- 1 ≤ ***n*** ≤ 20
#### OUTPUT FORMAT
Your function should return the height of the binary tree.
#### SAMPLE INPUT 0 
![SampleInput](https://s3.amazonaws.com/hr-assets/0/1527625966-0f80a8e1a4-treeDepthSample0.png)
#### SAMPLE OUTPUT 0
```
3
```
#### EPLANATION
The longest root-to-leaf path is shown below:
![Explanation](https://s3.amazonaws.com/hr-assets/0/1527626088-807ca5fc63-treeDepthSample1.png)
There are 4 nodes in this path that are connected by 3 edges, meaning our binary tree's *height* = 3.
#### SOLUTION
```python
# Enter your code here. Read input from STDIN. Print output to STDOUT
'''
class Node:
      def __init__(self,info): 
          self.info = info  
          self.left = None  
          self.right = None 
           

       // this is a node of the tree , which contains info as data, left , right
'''

def height(root):
    if root is None:
        return -1
    else:
        return 1 + max(height(root.left), height(root.right))

```

---

### Binary Search Tree: Lowest Common Ancestor
```python
# Enter your code here. Read input from STDIN. Print output to STDOUT
'''
class Node:
      def __init__(self,info): 
          self.info = info  
          self.left = None  
          self.right = None 
           

       // this is a node of the tree , which contains info as data, left , right
'''

def lca(root, v1, v2):
    if (root is None):
        return None
    if (v1 < root.info and v2 < root.info):
        return lca(root.left, v1, v2)
    if (v1 > root.info and v2 > root.info):
        return lca(root.right, v1, v2)
    return root
```

---

### Swap Nodes
```js

/*
 * Complete the swapNodes function below.
 */
function swapNodes(indexes, queries) {
    const root = new Node(1)
    const levels = [[root]]
    let level = 0
    let node = 0
    let currentNode = root

    for (let i = 0; i < indexes.length; i++) {
        const index = indexes[i]
        currentNode = levels[level][node]
        levels[level+1] = levels[level+1] || []
        if (index[0] !== -1) {
            currentNode.left = new Node(index[0])
            levels[level+1].push(currentNode.left)
        }
        if (index[1] !== -1) {
            currentNode.right = new Node(index[1])
            levels[level+1].push(currentNode.right)
        }
        node++
        if (levels[level].length === node) {
            level++
            node = 0
        }
    }
    printNode(root)
    return queries.reduce((result, swapLevel) => {
        swapTree(root, swapLevel)
        result.push(inOrder(root))
        return result
    }, [])
}
class Node {
  constructor (value) {
    this.value = value
    this.left = null
    this.right = null
  }
}
function swapTree (node, levelToSwap = 0, level = 1) {
  if (!node) return
  if (level % levelToSwap === 0) {
      const leftNode = node.left
      node.left = node.right
      node.right = leftNode
  }
  const nextLevel = level + 1
  swapTree(node.left, levelToSwap, nextLevel)
  swapTree(node.right, levelToSwap, nextLevel)
}
function inOrder (node) {
  if (!node) return []
  return [
    ...inOrder(node.left),
    node.value,
    ...inOrder(node.right)
  ]
}
function printNode(node, indent = '') {
  // current item's indentation prefix
  var prefix = indent+'\\-';
  
  var leftChild  = node['left'],
      rightChild = node['right'];
  
  var displayStr = node['value'];
  console.log(prefix+' '+displayStr);
  
  // recurse left
  if (!!leftChild) printNode(leftChild, indent+(!!rightChild?' |':'  '));
  // recurse right
  if (!!rightChild) printNode(rightChild, indent+'  ');
}
```

---

### Balanced Forest
https://www.hackerrank.com/challenges/balanced-forest/problem

---
