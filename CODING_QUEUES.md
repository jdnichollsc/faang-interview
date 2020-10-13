
### Castle On the Grid
```js
// Complete the minimumMoves function below.
function minimumMoves(grid, startX, startY, goalX, goalY) {
    if (grid[startX][startY] === 'X' || grid[goalX][goalY] === 'X') return 0
    const queue = []
    const startCell = {
        position: { x: startX, y: startY },
        moves: 0
    }
    queue.push(startCell)
    // HASH MAP X_Y
    const visited = {}
    visited[getCellKey(startX, startY)] = true

    const markCellAsVisited = (x, y, moves, parent) => {
        const cellKey = getCellKey(x, y)
        if (grid[x][y] === 'X' || visited[cellKey]) return null
        visited[cellKey] = true
        const newCell = {
            position: { x, y },
            moves,
            parent
        }
        queue.push(newCell)
        return newCell
    }
    while (queue.length > 0) {
        const currentCell = queue.shift()
        if (
            currentCell.position.x === goalX &&
            currentCell.position.y === goalY
        ) {
            return currentCell.moves
        }
        const { position } = currentCell
        const moves = currentCell.moves + 1
        // LEFT
        for (let y = position.y - 1; y >= 0; y--) {
            if (!markCellAsVisited(position.x, y, moves, currentCell)) break
        }
        // TOP
        for (let x = position.x - 1; x >= 0; x--) {
            if (!markCellAsVisited(x, position.y, moves, currentCell)) break
        }
        // RIGHT
        for (let y = position.y + 1; y < grid.length; y++) {
            if (!markCellAsVisited(position.x, y, moves, currentCell)) break
        }
        // BOTTOM
        for (let x = position.x + 1; x < grid.length; x++) {
            if (!markCellAsVisited(x, position.y, moves, currentCell)) break
        }
    }
    return 0
}
function getCellKey (x, y) {
    return `${x}_${y}`
}
```

---

### Shortest Cell Path
In a given grid of `0`s and `1`s, we have some starting row and column `sr`, `sc` and a target row and column `tr`, `tc`. Return the length of the shortest path from `sr`, `sc` to `tr`, `tc` that walks along `1` values only.

Each location in the path, including the start and the end, must be a `1`. Each subsequent location in the path must be 4-directionally adjacent to the previous location.

It is guaranteed that `grid[sr][sc] = grid[tr][tc] = 1`, and the starting and target positions are different.

If the task is impossible, return `-1`.

#### Examples
```
input:
grid = [[1, 1, 1, 1], [0, 0, 0, 1], [1, 1, 1, 1]]
sr = 0, sc = 0, tr = 2, tc = 0
output: 8
(The lines below represent this grid:)
1111
0001
1111

grid = [[1, 1, 1, 1], [0, 0, 0, 1], [1, 0, 1, 1]]
sr = 0, sc = 0, tr = 2, tc = 0
output: -1
(The lines below represent this grid:)
1111
0001
1011
```

#### Constraints
- [time limit] 5000ms
- [input] array.array.integer grid
    * 1 ≤ arr.length = arr[i].length ≤ 10
- [input] integer sr
- [input] integer sc
- [input] integer tr
- [input] integer tc
    * All sr, sc, tr, tc are valid locations in the grid, grid[sr][sc] = grid[tr][tc] = 1, and (sr, sc) != (tr, tc).
- [output] integer

#### SOLUTION
```js
function shortestCellPath(grid, sr, sc, tr, tc) {
	/**
	@param grid: integer[][]
	@param sr: integer
	@param sc: integer
	@param tr: integer
	@param tc: integer
	@return: integer
	*/

	// your code goes here
  
  const visited = {}
  const queue = []
  const startCell = {
    x: sr,
    y: sc,
    distance: 0
  }
  queue.push(startCell)
  
  const markCellAsVisited = (x, y, distance) => {
    const cellKey = getCellKey(x, y)
    if (grid[x][y] !== 1 || visited[cellKey]) return
    visited[cellKey] = true
    queue.push({
      x,
      y,
      distance
    })
  }
  
  while (queue.length) {
    const currentCell = queue.shift()
    if (currentCell.x === tr && currentCell.y === tc)
        return currentCell.distance
    const newDistance = currentCell.distance + 1
    
    // RIGHT
    if (currentCell.y < grid[0].length - 1)
      markCellAsVisited(currentCell.x, currentCell.y + 1, newDistance)
    // BOTTOM
    if (currentCell.x < grid.length - 1)
        markCellAsVisited(currentCell.x + 1, currentCell.y, newDistance)
    // LEFT
    if (currentCell.y > 0)
        markCellAsVisited(currentCell.x, currentCell.y - 1, newDistance)
    // TOP
    if (currentCell.x > 0)
        markCellAsVisited(currentCell.x - 1, currentCell.y, newDistance)
  }
  return -1
}

function getCellKey (row, col) {
  return row + '_' + col
}
const grid = [[1, 1, 1, 1], [0, 0, 0, 1], [1, 1, 1, 1]]
const sr = 0, sc = 0, tr = 2, tc = 0
console.log(shortestCellPath(grid, sr, sc, tr, tc))
```
