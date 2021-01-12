## Trees

---
### [Height of a Binary Tree](https://www.hackerrank.com/challenges/tree-height-of-a-binary-tree/problem)
The height of a binary tree is the number of edges between the tree's root and its furthest leaf. For example, the following binary tree is of height 2.

![Description](https://s3.amazonaws.com/hr-assets/0/1527626183-88c8070977-isitBSTSample0.png)
#### Function Description
Complete the *getHeight* or *height* function in the editor. It must return the height of a binary tree as an integer.
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
#### EXPLANATION
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

### [Level Order Traversal](https://www.hackerrank.com/challenges/tree-level-order-traversal/problem)
Given a pointer to the root of a binary tree, you need to print the level order traversal of this tree. In level-order traversal, nodes are visited level by level from left to right. Complete the function **levelOrder** and print the values in a single line separated by a space.

For example:

```
     1
      \
       2
        \
         5
        /  \
       3    6
        \
         4
```
For the above tree, the level order traversal is **1 -> 2 -> 5 -> 3 -> 6 -> 4**.

#### INPUT FORMAT
You are given a function,
```
void levelOrder(Node * root) {

}
```

#### CONSTRAINTS
1 <= Nodes in the tree <= 500

#### OUTPUT FORMAT
Print the values in a single line separated by a space.

#### SAMPLE INPUT
```
     1
      \
       2
        \
         5
        /  \
       3    6
        \
         4  
```

#### SAMPLE OUTPUT
`1 2 5 3 6 4`

#### EXPLANATION
We need to print the nodes level by level. We process each level from left to right.
Level Order Traversal: **1 -> 2 -> 5 -> 3 -> 6 -> 4**.

#### SOLUTION
```python
"""
Node is defined as
self.left (the left child of the node)
self.right (the right child of the node)
self.info (the value of the node)
"""

def levelOrder(root):
      #Write code Here
      q=[]
      q.append(root)
      while (len(q) > 0):
            n = q.pop(0)
            print n.info,
            if (n.left is not None):
                  q.append(n.left)
            if (n.right is not None):
                  q.append(n.right)
```

---

### [Binary Search Tree: Lowest Common Ancestor](https://www.hackerrank.com/challenges/binary-search-tree-lowest-common-ancestor/problem)
You are given pointer to the root of the binary search tree and two values ***v*1** and ***v*2**. You need to return the lowest common ancestor ([LCA](https://en.wikipedia.org/wiki/Lowest_common_ancestor)) of ***v*1** and ***v*2** in the binary search tree.

![Description](https://s3.amazonaws.com/hr-assets/0/1529959649-81b68736f7-lcaexample.png)

In the diagram above, the lowest common ancestor of the nodes 4 and 6 is the node 3.
Node 3 is the lowest node which has nodes 4 and 6 as descendants.
#### Function Description
Complete the function *lca* in the editor below. It should return a pointer to the lowest common ancestor node of the two values given.
lca has the following parameter(s):
- *root*: a pointer to the root node of a binary search tree.
- *v1*: a node.data value.
- *v2*: a node.data value.
#### INPUT FORMAT
The first line contains an integer, ***n***, the number of nodes in the tree.
The second line contains ***n*** space-separated integersrepresenting *node.data* values.
The third line contains two space-separated integers,***v*1** and ***v*2**.
If you download the test data, you will have to create the binary search tree yourself. If you write your code within our platform, the tree will be created for you.
#### CONSTRAINTS
 - 1 ≤ ***n, node.data*** ≤ 25
 - 1 ≤ ***v*1** and ***v*2** ≤ 25
 - ***v*1** ≠ ***v*2**
The tree will contain nodes with *data* equal to *v*1 and *v*2.
#### OUTPUT FORMAT
Return the a pointer to the node that is the lowest common ancestor of *v*1 and *v*2.
#### SAMPLE INPUT 0 
```
6
4 2 3 1 7 6
1 7
```
![SampleInput](https://s3.amazonaws.com/hr-assets/0/1527870675-1cfffe0a8a-LCASample.png)

**v1 = 1** and **v2 = 7**.

#### SAMPLE OUTPUT 0
[reference to node 4]

#### EXPLANATION
LCA of 1 and 7 is 4, the root in this case.
Return a pointer to the node.

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

### [Swap Nodes](https://www.hackerrank.com/challenges/swap-nodes/problem)
A binary tree is a tree which is characterized by one of the following properties:
- It can be empty (null).
- It contains a root node only.
- It contains a root node with a left subtree, a right subtree, or both. These subtrees are also binary trees.
*In-order* traversal is performed as
1. Traverse the left subtree.
2. Visit root.
3. Traverse the right subtree.
For this in-order traversal, start from the left child of the root node and keep exploring the left subtree until you reach a leaf. When you reach a leaf, back up to its parent, check for a right child and visit it if there is one. If there is not a child, you've explored its left and right subtrees fully. If there is a right child, traverse its left subtree then its right in the same manner. Keep doing this until you have traversed the entire tree. You will only store the values of a node as you visit when one of the following is true:
- it is the first node visited, the first time visited
- it is a leaf, should only be visited once
- all of its subtrees have been explored, should only be visited once while this is true
- it is the root of the tree, the first time visited
**Swapping**: Swapping subtrees of a node means that if initially node has left subtree L and right subtree R, then after swapping, the left subtree will be R and the right subtree, L.
For example, in the following tree, we swap children of node 1.
```
                                Depth
    1               1            [1]
   / \             / \
  2   3     ->    3   2          [2]
   \   \           \   \
    4   5           5   4        [3]
```
In-order traversal of left tree is 2 4 1 3 5 and of rigth tree is 3 5 1 2 4.
#### SWAP OPERATION
We define depth of a node as follows:
- The root node is at depth 1.
- If the depth of the parent node is *d*, then the depth of current node will be *d+1*.
Given a tree and an integer, *k*, in one operation, we need to swap the subtrees of all the nodes at each depth *h* whereh *h* ∈ [k, 2k, 3k,...]. In other words, if *h* is a multiple of *k*, swap the left and right subtrees of that level.
You are given a tree of *n*  nodes where nodes are indexed from [1..n] and it is rooted at 1. You have to perform *t* swap operations on it, and after each swap operation print the in-order traversal of the current state of the tree.
#### Function Description
Complete the *swapNodes* function in the editor below. It should return a two-dimensional array where each element is an array of integers representing the node indices of an in-order traversal after a swap operation.
swapNodes has the following parameter(s):
- *indexes*: an array of integeres representing index values of each *node[i]* beginning with *node[1]*, the first element, as the root.
- *queries*: an array of integeres, each representing a *k* value.
#### INPUT FORMAT
The first line contains *n*, number of nodes in the tree.
Each of the next *n* lines contains two integers, a b, where *a* is the index of left child, and *b* is the index of right child of *i*^th node.
**Note**: -1 is used to represent a null node.
The next line contains an integer, ***t***, the size of ***queries***.
Each of the next *t* lines contains an integer [*queries[i]*], each being a value ***k***.
#### OUTPUT FORMAT
For each *k*, perform the swap operation and store the indices of your in-order traversal to your result array. After all swap operations have been performed, return your result array for printing.
#### CONSTRAINTS
 - 1 ≤ *n* ≤ 1024
 - 1 ≤ *t* ≤ 100
 - 1 ≤ *k* ≤ *n*
 - Either *a* = -1 or 2 ≤ *a* ≤ *n*
 - Either *b* = -1 or 2 ≤ *b* ≤ *n*
 - The index of a non-null child will always be greater than that of its parent.
#### SAMPLE INPUT 0 
```
3         // n = 3
2 3       // i = 1, the children of node 1 are 2 and 3
-1 -1     // i = 2, node 2 has no children
-1 -1     // i = 3, node 3 has no children
2         // t = 2
1         // query[0], k = 1, meaning swap the subtrees of all levels that are a multiple of 1
1         // query[1], k = 1, meaning swap the subtrees of all levels that are a multiple of 1
```
#### SAMPLE OUTPUT 0
```
3 1 2
2 1 3
```
#### EXPLANATION 0
As nodes 2 and 3 have no children, swapping will not have any effect on them. We only have to swap the child nodes of the root node.
```
    1   [s]       1    [s]       1   
   / \      ->   / \        ->  / \  
  2   3 [s]     3   2  [s]     2   3
```
**Note**: [s] indicates that a swap operation is done at this depth.
#### SAMPLE INPUT 1
```
5
2 3
-1 4
-1 5
-1 -1
-1 -1
1
2
```
#### SAMPLE OUTPUT 1
```
4 2 1 5 3
```
#### EXPLANATION 1
Swapping child nodes of nodes 2 and 3 we get
```
    1                  1  
   / \                / \ 
  2   3   [s]  ->    2   3
   \   \            /   / 
    4   5          4   5  
```
#### SAMPLE INPUT 2
```
11
2 3
4 -1
5 -1
6 -1
7 8
-1 9
-1 -1
10 11
-1 -1
-1 -1
-1 -1
2
2
4
```
#### SAMPLE OUTPUT 2
```
2 9 6 4 1 3 7 5 11 8 10
2 6 9 4 1 3 7 5 10 8 11
```
#### EXPLANATION 2
Here we perform swap operations at the nodes whose depth is either 2 or 4 for ***k = 2*** and then at nodes whose depth is 4 for ***k = 4***
```
         1                     1                          1             
        / \                   / \                        / \            
       /   \                 /   \                      /   \           
      2     3    [s]        2     3                    2     3          
     /      /                \     \                    \     \         
    /      /                  \     \                    \     \        
   4      5          ->        4     5          ->        4     5       
  /      / \                  /     / \                  /     / \      
 /      /   \                /     /   \                /     /   \     
6      7     8   [s]        6     7     8   [s]        6     7     8
 \          / \            /           / \              \         / \   
  \        /   \          /           /   \              \       /   \  
   9      10   11        9           11   10              9     10   11 
```
#### SOLUTION
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

### [Balanced Forest](https://www.hackerrank.com/challenges/balanced-forest/problem)
There is tree of nodes containing integer data. You want to insert a node with some non-zero integer value somewhere into the tree. Your goal is to be able to cut two edges and have the values of each of the three new trees sum to the same amount. This is called a *balaced forest* . Determine the minimal amount that a new node can have to allow creation of a balanced forest. If it's not possible to create a balanced forest, return -1.
For example, you are given node values *c* = [**15, 12, 8, 14, 13**] and *edges* = [[1,1], [1,3], [1,4], [4,5]]. It is the following tree.

![Descriptiom](https://s3.amazonaws.com/hr-assets/0/1528138409-097321b50e-forestExample.png)

The blue node is root, the first number in a node is node number and the second is its value. Cuts can be made between nodes 1 and 3 and nodes 1 and 4 to have three trees with sums  27, 27 and 8. Adding a new node *w* of *c[w]* = 19 to the third tree completes the solution.
#### Function Description
Complete the *balancedForest* function in the editor below. It must return an integer representing the minimum value of *c[w]* that can be added to allow creation of a balanced forest, or -1 if it is not possible.
balancedForest has the following parameter(s):
- *c*: an array of integers, the data values for each node
- *edges*: an array of 2 element arrays, the node pairs per edge
#### INPUT FORMAT
The first line contains a single integer, *q*, number of queries.
Each of the following *q* sets of lines is as follows:
- The first line contains an integer, *n*, the number of nodes in the tree.
- The second line contains *n* space-separated integers describing the respective values of ***c[1],c[2],...,c[n]***, where each *c[i]*  denotes the value at node ***i***
- Each of the following **n-1** lines contains two space-separated integers, ***x[j]*** and ***y[j]***, describing edge ***j*** connecting nodes ***x[j]*** and ***y[j]***

#### CONSTRAINTS
- 1 ≤ *q* ≤ 5
- 1 ≤ *n* ≤ 5x10^4
- 1 ≤ *c[i]* ≤ 10^9
- Each query forms a valid undirected tree.

#### OUTPUT FORMAT
For each query, return the minimum value of the integer *c[w]*. If no such value exists, return -1 instead
#### SAMPLE INPUT 0
```
2
5
1 2 2 1 1
1 2
1 3
3 5
1 4
3
1 3 5
1 3
1 2
```
#### SAMPLE OUTPUT 0
```
2
-1
```
#### EXPLANATION 0
We perform the following two queries:
1. The tree initially looks like this:

![Descriptiom](https://s3.amazonaws.com/hr-assets/0/1528140939-72f0001183-forestSample0-1.png)


You can add a new node ***w*** = **6** with ***c[w]*** = **2** and create a new edge connecting nodes 4 and 6. Then you can cut the edge connecting nodes 1 and 4 and the edge connecting nodes 1 and 3. We now have a three-tree balanced forest where each tree has a sum of 3.

![Descriptiom](https://s3.amazonaws.com/hr-assets/0/1528141184-a92a2f7cff-forestSample0-2.png)

2. In the second query, it's impossible to add a node in such a way that we can split the tree into a three-tree balanced forest so we return -1.

#### SOLUTION

---
