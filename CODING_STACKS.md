## Coding Interview Prep
---
### Balanced Brackets
A bracket is considered to be any one of the following characters: (, ), {, }, [ or ].
Two brackets are considered to be a *matched pair* if the an opening bracket (i.e., (, [ or {) occurs to the left of a closing bracket (i.e., ), ] or } *of the exact same type*. There are three types of matched pairs of brackets: [], {}, ().
A matching pair of brackets is *not balanced* if the set of brackets it encloses are not matched. For example, {[)])} is not balanced because the contents in between { and } are not balanced. The pair of square brackets encloses a single, unbalanced opening bracket, [, and the pair of parentheses encloses a single, unbalanced closing square bracket, ].By this logic, we say a sequence of brackets is *balanced* if the following conditions are met:
- It contains no unmatched brackets.
- The subset of brackets enclosed within the confines of a matched pair of brackets is also a matched pair of brackets.
Given *n* strings of brackets, determine whether each sequence of brackets is balanced. If a string is balanced, return YES. Otherwise return NO.
#### Function Description
Complete the *isBalanced* in the editor below. It must return a string: YES if the sequence is balanced or NO if it is not.
isBalanced has the following parameter(s):
- *s*: a string of brackets
#### Input Format
The first line contains a single integer *n*, the number of strings.
Each of the next *n* lines contains a single string *s*, a sequence of brackets.
#### Constraints
- 1 <= *n* <= 10^3
- 1 <= |*s*| <= 10^3, where |*s*| is the length of the sequence.
- All characters in the sequences are **{, }, (, ), [ or ]**
#### Output Format
For each string, return YES or NO.
#### Sample Input
```
3
{[()]}
{[(])}
{{[[(())]]}}
```
#### Sample Output
```
YES
NO
YES
```
#### Explanation
1. The string {[()]} meets both criteria for being a balanced string, so we print YES on a new line.
2. The string {[(])} is not balanced because the brackets enclosed by the matched pair { and } are not balanced: [(])
3. The string {{[[(())]]}} meets both criteria for being a balanced string, so we print YES on a new line.
#### SOLUTION
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
 is planning to demolish a number of old, unoccupied buildings and construct a shopping mall in their place. Your task is to find the largest solid area in which the mall can be constructed.
 There are a number of buildings in a certain two-dimensional landscape. Each building has a height, given by *h[i]* where *i* represents the building number. If you join*k* adjacent buildings, they will form a solid rectangle of area *k* * [the minimum height of the adjacent buildings].
 For example, the heights array  h = [3,2,3]. A rectangle of height h = 2 and length k = 3 can be constructed within the boundaries. The area formed is h*k = 2*3 = 6.
#### Function Description
Complete the *largestRectangle* in the editor below. It should return an integer representing the largest rectangle that can be formed within the bounds of consecutive buildings.
largestRectangle has the following parameter(s):
- *h*: an array of integers representing building heights
#### Input Format
The first line contains *n*, the number of buildings.
The second line contains *n* space-separated integers, each representing the height of a building.
#### Constraints
- 1 <= *n* <= 10^5
- 1 <= *h[i]* <= 10^6
#### Output Format
Print a long integer representing the maximum area of rectangle formed.
#### Sample Input
```
5
1 2 3 4 5
```
#### Sample Output
```
9
```
#### Explanation
An illustration of the test case follows.
![Explanation](https://s3.amazonaws.com/hr-challenge-images/8136/1436794554-75e178e325-drawing47.svg)
#### SOLUTION
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
Given an integer array of size *n*, find the maximum of the minimum(s) of every window size in the array. The window size varies from 1 to *n*.
For example, given *arr* = [6, 3, 5, 1, 12], consider window sizes of 1 through 5. Windows of size 1 are (6), (3), (5), (1), (12). The maximum value of the minimum values of these windows is 12. Windows of size 2 aare (6, 3), (3, 5), (5, 1), (1, 12) and their minima are (3, 3, 1, 1). The maximum of these values is 3. Continue this process through window size 5 to finally consider the entire array. All of the answers are 12, 3, 3, 1, 1.
#### Function Description
Complete the *riddle* function in the editor below. It must return an array of integers representing the maximum minimum value for each window size from 1 to *n*.
riddle has the following parameter(s):
- *arr*: an array of integers.
#### Input Format
The first line contains a single integer *n*, the size of *arr*
The second line contains *n* space-separated integers.
#### Constraints
- 1 <= *n* <= 10^6
- 0 <= *arr[i]* <= 10^9
#### Output Format
Single line containing *n* space-separated integers denoting the output for each window size from 1 to *n*.
#### Sample Input 0
```
4
2 6 1 12
```
#### Sample Output 0
```
12 2 1 1
```
#### Explanation 0
Here *n* = 4 *arr* = [2, 6, 1, 12]

TABLA PENDIENTE!!! EJERCICIO 37

#### Sample Input 1
```
7
1 2 3 5 1 13 3
```
#### Sample Output 1
```
13 3 2 1 1 1 1
```
#### Explanation 1
Here *n* = 7 *arr* = [1, 2, 3, 5, 1, 13, 3]

TABLA PENDIENTE!!! EJERCICIO 37

#### SOLUTION
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
There are a number of plants in a garden. Each of these plants has been treated with some amount of pesticide. After each day, if any plant has more pesticide than the plant on its left it dies.
You are given the initial values of the pesticide in each of the plants. Print the number of days after which no plant dies, i.e. the time after which there are no plants with more pesticide content than the plant to their left.
For example, pesticide levels *p* = [3, 6, 2, 7, 5]. Using a 1-indexed array, day 1 plants 2 and 4 die leaving *p* = [3, 2, 5]. On day 2, plant 3 of the current array dies leaving *p* = [3, 2]. As there is no plant with a higher concentration of pesticide than the one to its left, plants stop dying after day 2.
#### Function Description
Complete the *poisonousPlants* in the editor below. It must return an integer representing the number of days until plants no longer die from pesticide.
poisonousPlants has the following parameter(s):
- *p*: an array of integers representing pesticide levels in each plant
#### Input Format
The first line contains an integer *n*, the size of the array *p*.
The next line contains *n* space-separated integers *p[i]*
#### Constraints
- 1 <= *n* <= 10^5
- 0 <= *p[i]* <= 10^9
#### Output Format
Output an integer equal to the number of days after which no plants die.
#### Sample Input
```
7
6 5 8 4 7 10 9
```
#### Sample Output
```
2
```
#### Explanation
Initially all plants are alive.
Plants = [6, 5, 8, 4, 7, 10, 9]
After the 1^st day, 4 plants remain as plants 3, 5, and 6 die.
Plants = [6, 5, 4, 9]
After the 2^nd day, 3 plants survive as plant 4 dies.
Plants = [6, 5, 4]
After the 2^nd day the plants stop dying.
#### SOLUTION
---
