
### Balanced Brackets
```js
// Complete the isBalanced function below.
function isBalanced(s) {
  if (s.length % 2) return 'NO'
  const stack = []
  const leftPart = '({['
  const rightPart = ')}]'
  const closes = {
      ')' : '(',
      ']' : '[',
      '}' : '{' 
  }
  let isBalanced = true
  for (let i = 0; i < s.length; i++) {
      if (leftPart.includes(s[i])) {
          stack.push(s[i])
      } else if (rightPart.includes(s[i])) {
          if (!stack.length || stack.pop() !== closes[s[i]]) {
              isBalanced = false
              break
          }
      }
  }
  return isBalanced && stack.length === 0 ? 'YES' : 'NO'
}
```

---

### Largest Rectangle
```js
// Complete the largestRectangle function below.
function largestRectangle(h) {
    
    /* Time complexity => O (n*n)
    let maxArea = 0
    const maxHeight = h.length < 100 ? Math.max(...h) : Math.pow(10, 6)
    for (let i = 2; i < maxHeight; i++) {
        let maxBuildings = 0
        let tempBuildings = 0
        for (let j = 0; j < h.length; j++) {
            if (h[j] >= i) {
                tempBuildings++
            } else {
                if (tempBuildings > maxBuildings) {
                    maxBuildings = tempBuildings
                }
                tempBuildings = 0
            }
        }
        const newArea = Math.max(maxBuildings, tempBuildings) * i
        if (newArea > maxArea) maxArea = newArea
    }
    return maxArea*/

    // Time complexity => O(n)
    const positions = []
    const heights = [...h, 0]
    let area = 0
    let i = 0
    while (i < heights.length) {
        if (!positions.length || heights[positions[positions.length-1]] <= heights[i]) {
            positions.push(i++)
        } else {
            const top = positions.pop()
            const numberOfBuildings = positions.length ? (i - positions[positions.length-1] - 1) : i
            area = Math.max(area, heights[top] * numberOfBuildings)
        }
    }
    return area
}
```

---

### Min Max Riddle
```js
// Complete the solve function below.
function riddle(arr) {
    // solve here
    /* Time complexity => O (n*n)
    const stack = arr
    const windowSizes = []
    for (let i = 0; i < arr.length; i++) {
        let maxSize = 0
        for (let j = 0; j < arr.length - i; j++) {
            const value = i === 0 ? arr[j] : Math.min(stack[j], stack[j+1])
            stack[j] = value
            if (value > maxSize) maxSize = value
        }
        windowSizes.push(maxSize)
    }
    return windowSizes*/
    
    // Time complexity => O(n)
    arr.push(0)
    const n = arr.length
    const windowSizes = new Array(arr.length).fill(0)
    const positions = []
    let i = 0
    while (i < n) {
        if (!positions.length || arr[positions[positions.length-1]] <= arr[i]) {
            positions.push(i++)
        } else {
            const top = positions.pop()
            // Where range represents every window size
            const range = positions.length ? (i - positions[positions.length-1] - 1) : i
            if (range < 1 || range > arr.length || arr[top] === 0) continue
            windowSizes[range-1] = Math.max(windowSizes[range-1], arr[top])
        }
    }
    for (let i = n - 2; i >= 0; i--) {
        windowSizes[i] = Math.max(windowSizes[i], windowSizes[i+1])
    }
    windowSizes.pop()
    return windowSizes
}

```

---

### Poisonous Plants
https://www.hackerrank.com/challenges/poisonous-plants/problem

---
