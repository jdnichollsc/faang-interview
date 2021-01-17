## Graphs

### [Find the Nearest Clone](https://www.hackerrank.com/challenges/find-the-nearest-clone/problem)
There is a connected undirected graph where each of the nodes is a color. Given a color, find the shortest path connecting any two nodes of that color. Each edge has a weight of 1. If there is not a pair or if the color is not found, print -1.
For example, given *graph_nodes* and 4 edges *g_from* = [1, 2, 2, 3] and *g_to* = [2, 3, 4, 5] and colors for each node are *arr* = [1, 2, 3, 1, 3] we can draw the following graph:
![Description](https://s3.amazonaws.com/hr-assets/0/1529952915-a96eba7baa-nearestcloneexample.png)

Each of the nodes is labeled [node]/[color] and is colored appropriately. If we want the shortest path between color 3, blue, we see there is a direct path between nodes 3 and 5. For green, color 1, we see the path length 2 from 1 → 2 → 4. There is no pair for node 4 having color 2, red.
#### Function Description
Complete the *findShortest* function in the editor below. It should return an integer representing the length of the shortest path between two nodes of the same color, or -1 if it is not possible.
findShortest has the following parameter(s):
- *g_nodes*: an integer, the number of nodes
- *g_from*: an array of integers, the start nodes for each edge
- *g_to*: an array of integers, the end nodes for each edge
- *ids*: an array of integers, the color id per node
- *val*: an integer, the id of the color to match
#### Input Format
The first line contains two space-separated integers *n* and *m*, the number of nodes and edges in the graph.
Each of the next *m* lines contains two space-separated integers *g_from[i]* and *g_to[i]*, the nodes connected by an edge.
The next line contains *n* space-seperated integers, *ids[i]*, representing the color id of each node from  to *n*
The last line contains the id of the color to analyze.
**Note**: The nodes are indexed from 1 to *n*
#### Constraints
- 1 <= *n* <= 10^6
- 1 <= *m* <= 10^6
- 1 <= *ids[i]* <= 10^8
#### Output Format
Print the single integer representing the smallest path length or -1
#### Sample Input 0
```
4 3       // n = 4, m = 3, meaning there are 4 nodes and 3 edges in the graph
1 2       // there is an edge from node 1 to node 2
1 3       // there is an edge from node 1 to node 3
4 2       // there is an edge from node 4 to node 2
1 2 1 1   // nodes 1, 3, and 4 are color 1, node 2 is color 2
1         // find the shortest path connecting nodes of color 1
```
#### Sample Output 0
`1`
#### Explanation 0
![Explanation](https://s3.amazonaws.com/hr-assets/0/1529953948-1e4fee4daf-nearestclonesample0.png)

In the above image the distance between the closest nodes having color label 1 is 1
#### Sample Input 1
```
4 3      
1 2       
1 3       
4 2       
1 2 3 4   
2         
```
#### Sample Output 1
`-1`
#### Explanation 1
![Explanation](https://s3.amazonaws.com/hr-assets/0/1530566003-c7e0b27b06-nearestclonesample1.png)

#### Sample Input 2
```
5 4      
1 2       
1 3       
2 4 
3 5
1 2 3 3 2
2
```
#### Sample Output 2
`3`
#### Explanation 2
![Explanation](https://s3.amazonaws.com/hr-assets/0/1530566304-daec2771f0-nearestclonesample2.png)

#### SOLUTION
```js
function findShortest(graphNodes, graphFrom, graphTo, ids, val) {
    // solve here
    let startIndex = null
    // Generate Adjacency List
    const nodes = graphFrom.reduce((nodes, from, index) => {
        const fromIndex = from - 1
        const toIndex = graphTo[index] - 1
        nodes[fromIndex] = nodes[fromIndex] || []
        nodes[fromIndex].push(toIndex)
        nodes[toIndex] = nodes[toIndex] || []
        nodes[toIndex].push(fromIndex)
        if (ids[fromIndex] === val && startIndex === null) startIndex = fromIndex
        else if (ids[toIndex] === val && startIndex === null) startIndex = toIndex
        return nodes
    }, [])
    
    const bfs = []
    bfs[startIndex] = {
        distance: 0,
        predecessor: null,
        color: val
    }
    const queue = []
    queue.push(startIndex)
    let minDistance = -1
    while (queue.length) {
        const current = queue.shift()
        if (!nodes[current]) return -1
        for (let i = 0; i < nodes[current].length; i++) {
            const nodeIndex = nodes[current][i]
            if (!bfs[nodeIndex]) {
                let distance = bfs[current].distance + 1
                if (ids[nodeIndex] === val && (
                    minDistance === -1 ||
                    minDistance > distance
                )) {
                    minDistance = distance
                    distance = 0
                }
                bfs[nodeIndex] = {
                    distance,
                    predecessor: current,
                    color: val
                }
                queue.push(nodeIndex)
            }
        }
    }
    return minDistance
}
```

---

### [DFS: Connected Cell in a Grid](https://www.hackerrank.com/challenges/ctci-connected-cell-in-a-grid/problem)
Consider a matrix where each cell contains either a 0 or a 1 and any cell containing a 1 is called a *filled* cell. Two cells are said to be *connected* if they are adjacent to each other horizontally, vertically, or diagonally. In the diagram below, the two colored regions show cells connected to the filled cells. Black on white are not connected.

![Description](https://s3.amazonaws.com/hr-assets/0/1528204809-ea89cbdef6-connected.png)

If one or more filled cells are also connected, they form a *region*. Note that each cell in a region is connected to at least one other cell in the region but is not necessarily directly connected to all the other cells in the region.  In the diagram below, the two colors represent two different regions.

![Description](https://s3.amazonaws.com/hr-assets/0/1528205314-6fa4d1c8c7-connected2.png)

Given an *n x m* matrix, find and print the number of cells in the largest *region* in the matrix.

#### Function Description
Complete the *maxRegion*  in the editor below. It must return an integer value, the size of the largest region.
maxRegion has the following parameter(s):
- *grid*: a two dimensional array of integers
#### Input Format
The first line contains an integer *n*, the number of rows in the matrix, *grid*
The second line contains an integer, *m*, the number of columns in the matrix.
Each of the following *n* lines contains a row of *m* space-separated integers, *grid[i][j]*
#### Constraints
- 0 < *n, m* < 10
- *grid[i][j]* ϵ {0, 1}
#### Output Format
Print the number of cells in the largest *region* in the given matrix.
#### Sample Input
```
4
4
1 1 0 0
0 1 1 0
0 0 1 0
1 0 0 0
```
#### Sample Output
`5`
#### Explanation
The diagram below depicts two regions of the matrix:

![Explanation](https://s3.amazonaws.com/hr-assets/0/1528205939-1a630369ad-connectedSample.png)


The first region has five cells and the second region has one cell. We choose the larger region.
#### SOLUTION
```js
const cellKey = (row) => (col) => row + '_' + col
const findRegion = (grid, visited, row, col) => {
    const key = cellKey(row)(col)
    if (
        row < 0
        || row >= grid.length
        || col < 0
        || col >= grid[0].length
        || !grid[row][col]
        || visited[key]
    ) return 0
    visited[key] = true
    let count = 1
    count += findRegion(grid, visited, row + 1, col)
    count += findRegion(grid, visited, row, col + 1)
    count += findRegion(grid, visited, row + 1, col + 1)
    count += findRegion(grid, visited, row - 1, col)
    count += findRegion(grid, visited, row, col - 1)
    count += findRegion(grid, visited, row - 1, col - 1)
    count += findRegion(grid, visited, row - 1, col + 1)
    count += findRegion(grid, visited, row + 1, col - 1)
    return count
}
function maxRegion(grid) {
    const visited = {}
    let bigRegion = 0
    const numColumns = grid[0].length
    for (let row = 0; row < grid.length; row++) {
        for (let col = 0; col < numColumns; col++) {
            if (!visited[cellKey(row)(col)]) {
                bigRegion = Math.max(
                    bigRegion,
                    findRegion(grid, visited, row, col)
                )
            }
        }
    }
    return bigRegion
}
```
---

### [BFS: Shortest Reach in a Graph](https://www.hackerrank.com/challenges/ctci-bfs-shortest-reach/problem)
Consider an undirected graph consisting of **n** nodes where each node is labeled from **1** to **n** and the edge between any two nodes is always of length **6**. We define node **s** to be the starting position for a BFS. Given a graph, determine the distances from the start node to each of its descendants and return the list in node number order, ascending. If a node is disconnected, it's distance should be **-1**.

For example, there are **n = 6** nodes in the graph with a starting node **s = 1**. The list of **edges = [[1, 2], [2, 3], [3, 4], [1, 5]]**, and each has a weight of **6**.

![Shortest Example](https://s3.amazonaws.com/hr-assets/0/1528143002-2e9a521ad9-bfs_shortestExample.png)

Starting from node **1** and creating a list of distances, for nodes **2** through **6** we have **distances = [6, 12, 18, 6, -1]**.

#### Function Description
Define a Graph class with the required methods to return a list of distances.

#### Input Format
The first line contains an integer, **q**, the number of queries.

Each of the following **q** sets of lines is as follows:
- The first line contains two space-separated integers, **n** and **m**, the number of nodes and the number of edges.
- Each of the next **m** lines contains two space-separated integers, **u** and **v**, describing an edge connecting node **u** to node **v**.
- The last line contains a single integer, **s**, the index of the starting node.

#### Constraints
- **1 <= q <= 10**
- **2 <= n <= 1000**
- **1 <= m <= n*(n-1)/2**

#### Output Format
For each of the **q** queries, print a single line of **n - 1** space-separated integers denoting the shortest distances to each of the **n - 1** other nodes from starting position **s**. These distances should be listed sequentially by node number (i.e., **1, 2, ..., n**), but should not include node **s**. If some node is unreachable from **s**, print **-1** as the distance to that node.

#### Sample Input
```
2
4 2
1 2
1 3
1
3 1
2 3
2
```

#### Sample Output
```
6 6 -1
-1 6
```

#### Explanation
We perform the following two queries:

1. The given graph can be represented as:

![BFS shortest sample 1](https://s3.amazonaws.com/hr-assets/0/1528143514-a6a60ebfaa-bfs_shortest_sample0.png)

where our start node, **s**, is node **1**. The shortest distances from **s** to the other nodes are one edge to node **2**, one edge to node **3**, and there is no connection to node **4**.

2. The given graph can be represented as:

![BFS shortest sample 2](https://s3.amazonaws.com/hr-assets/0/1528143628-62469f0450-bfs_shortestSample1.png)

where our start node, **s**, is node **2**. There is only one edge here, so node **1** is unreachable from node **2** and node **3** has one edge connecting it to node **2**. We then print node **2**'s distance to nodes **1** and **3** (respectively) as a single line of space-separated integers: -1 6.

Note: Recall that the actual length of each edge is **6**, and we print **-1** as the distance to any node that's unreachable from **s**.

#### SOLUTION
```js
function getShortestDistance (graph) {
    const shortestDistance = new Array(graph.numberOfNodes).fill(-1)
    const visited = []
    const queue = []
    queue.push({
        node: graph.startingNode,
        distance: 0
    })
    visited[graph.startingNode] = true
    while (queue.length > 0) {
        const { node, distance } = queue.shift()
        shortestDistance[node-1] = distance
        const nodesConnected = graph.nodes[node]
        for (var i = 0; i < nodesConnected.length; i += 1) {
            if (!visited[nodesConnected[i]]) {
                visited[nodesConnected[i]] = true
                queue.push({
                    node: nodesConnected[i],
                    distance: distance + 6
                })
            }
        }
    }
    shortestDistance.splice(graph.startingNode-1, 1)
    return shortestDistance
}

function processData(input) {
    const [numberOfQueries, ...lines] = input.split('\n')
    const graphs = []
    let nodes = {}
    let numberOfNodes = 0
    let numberOfEdges = 0
    //Enter your code here
    for (let i = 0; i < lines.length; i++) {
        const line = lines[i].split(' ').map((edge) => Number(edge))
        if (line.length > 1) {
            if (!numberOfNodes) {
                numberOfNodes = line[0]
                numberOfEdges = line[1]
            } else {
                const [nodeA, nodeB] = line
                nodes[nodeA] = (nodes[nodeA] || [])
                nodes[nodeA].push(nodeB)
                nodes[nodeB] = (nodes[nodeB] || [])
                nodes[nodeB].push(nodeA)
            }
        }
        else {
            graphs.push({
                startingNode: line[0],
                nodes,
                numberOfNodes,
                numberOfEdges
            })
            nodes = {}
            numberOfNodes = 0
            numberOfEdges = 0
        }
    }
    const result = graphs.reduce((shortestDistances, graph) => {
        const shortestDistance = getShortestDistance(graph)
        console.log(shortestDistance.join(' '))
        shortestDistances.push(shortestDistance)
        return shortestDistances
    }, [])
    return result
}
```

---

### [Choosing in a Graph](https://www.hackerrank.com/challenges/matrix/problem)
The kingdom has cities connected by bidirectional roads. There is a unique path between any pair of cities. The machines have risen up and are planning to destroy the whole kingdom. If two machines can join forces, they will attack. You have to destroy roads connecting cities with machines in order to stop them from joining forces. There must not be any path connecting two machines.
Each of the roads takes an amount of time to destroy, and only one can be worked on at a time. Given a list of edges and times, determine the minimum time to stop the attack.
For example, there are *n = 5* cities called 0 - 4. Three of them have machines and are colored red. The time to destroy is shown next to each road. If we cut the two green roads, there are no paths between any two machines. The time required is 3 + 2 = 5

![Explanation](https://s3.amazonaws.com/hr-assets/0/1528209077-f7699103c6-matrixExample.png)

#### Function Description
Complete the *minTime* in the editor below. It must return an integer representing the minimum time to cut off access between the machines.
minTime has the following parameter(s):
- *roads*: a two-dimensional array of integers, each *roads[i]* = *[city1, city2, time]* where cities are connected by a road that takes *time* to destroy.
- *machines*: an array of integers representing cities with machines.
#### Input Format
The first line of the input two space-separated integers *n* and *k*, the number of cities and the number of machines.
Each of the following *n-1* lines contains three space-separated integers *city1*, *city2* and *time*. There is a bidirectional road connecting *city1* and *city2*, and to destroy this road it takes *time* units.
Each of the last *k* lines contains an integer, *machine[i]*, the label of a city with a machine.
#### Constraints
- 2 <= *n* <= 10^5
- 2 <= *k* <= *n*
- 1 <= *time[i]* <= 10^6
#### Output Format
Return an integer representing the minimum time required to disrupt the connections among all machines.
#### Sample Input 0
```
5 3
2 1 8
1 0 5
2 4 5
1 3 4
2
4
0
```
#### Sample Output 0
`10`
#### Explanation 0
![Explanation](https://s3.amazonaws.com/hr-assets/0/1528209926-cda6d7fb35-matrixSample.png)

The machines are located at the cities 0, 2 and 4. You can destroy the green roads resulting in a time of 5 + 5 = 10. Destroying the road between cities 2 and 1 instead of between 1 and 0 would work, but it's not minimal.

#### SOLUTION
```js
function minTime(roads, machines) {
    const n =  + 1
    const isMachine = new Array(n).fill(false)
    machines.forEach(m => isMachine[m] = true)
    // Adjacency List of roads
    const adj = new Array(n);
    for(let i = 0; i < roads.length; i++) {
        const road = roads[i]
        const fromCity = road[0]
        const toCity = road[1]
        const time = road[2]
        adj[fromCity] = adj[fromCity] || []
        adj[toCity] = adj[toCity] || []
        adj[fromCity].push([toCity, time])
        adj[toCity].push([fromCity, time])
    }

    const visited = {}
    let total = 0
    const dfs = (city, time) => {
        visited[city] = true
        let maxTime = 0
        let sumTime = 0
        for(let i = 0; i < adj[city].length; i++) {
            const neighbor = adj[city][i]
            if(visited[neighbor[0]]) continue

            const neighborTime = dfs(neighbor[0], neighbor[1])
            sumTime += neighborTime
            maxTime = Math.max(maxTime, neighborTime)
        }

        if(isMachine[city]) {
            total += sumTime
            return time;
        } else  {
            total += sumTime - maxTime
            return Math.min(maxTime, time)
        }
    }
    dfs(0, 0)
    return total
}
```
---
