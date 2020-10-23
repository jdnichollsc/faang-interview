## Graphs

### Find the Nearest Clone
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

---

### Choosing in a Graph
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

---

### DFS: Connected Cell in a Grid
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

---
