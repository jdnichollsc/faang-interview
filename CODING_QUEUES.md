
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
