
### Greedy Florist
```js
// Complete the getMinimumCost function below.
function getMinimumCost(k, c) {
  // descending order
  const costSorted = c.sort((a, b) => b-a)
  // current friend
  let currentFriend = 0
  // friend purchases
  const purchases = [...new Array(k)].map(() => [])

  return costSorted.reduce((minCost, cost) => {
    if (currentFriend === k) currentFriend = 0
    
    const totalFlowers = purchases[currentFriend].length
    const newPrice = (totalFlowers + 1) * cost
    purchases[currentFriend].push(cost)
    currentFriend++
    return minCost + newPrice
  }, 0)
}
```
---
### Max Min Array
```js
// Complete the maxMin function below.
function maxMin(k, arr) {
  const sorted = arr.sort((a, b) => a-b)
  let minUnfairness = sorted[sorted.length-1]
  for (let i = 0; i < arr.length - k + 1; i++) {
      const subarr = sorted.slice(i, i + k)
      const unfairness = subarr[subarr.length-1] - subarr[0]
      if (unfairness < minUnfairness) minUnfairness = unfairness
  }
  return minUnfairness
}
```
---
