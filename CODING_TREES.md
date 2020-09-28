
### Height of a Binary Tree
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
