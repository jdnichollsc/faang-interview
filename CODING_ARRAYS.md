## Arrays
---

### [Count Matching Pairs of Numbers](https://www.hackerrank.com/challenges/sock-merchant/problem)
Given an array of integers, determine how many pairs of matching integers there are.
For example, in an array of length 7, sampleArray = [1, 2, 1, 2, 1, 3, 2],  there is one pair of 1's and one pair of 2's. There are three unpaired numbers left, a 1, a 2 and a 3. The number of pairs is 2.
#### Function Description
Complete the *numberPairs* function in the editor below. It must return the number of matching pairs in the array.
numberPairs has the following parameter(s):
- n: the length of the array
- a: the array of numbers
#### Input Format
The first line contains an integer n, the length of the array. The second line contains n space-separated integers within the array.
#### Constraints
- 1 <= n <= 100
- The numbers contained in the array a are between 1 and 100
#### Output Format
Return the total number of *matching pairs of numbers*
#### Sample Input
```
9
10 20 20 10 10 30 50 10 20
```
#### Sample Output
`3`
#### Explanation
![Explanation](https://s3.amazonaws.com/hr-challenge-images/25168/1474122392-c7b9097430-sock.png)
#### SOLUTION
```js
function numberPairs(n, ar) {
  const indices = new Set()
  return ar.reduce(function (result, currentNumber, index, ar) {
    if (!indices.has(index)) {
      for(let i = index + 1; i < n; i++) {
        if (ar[i] === currentNumber) {
          indices.add(i)
          result++
          break
        }
      }
    }
    return result
  }, 0)
}
```

---

### [Jumping on the Clouds](https://www.hackerrank.com/challenges/jumping-on-the-clouds/problem)
Emma is playing a new mobile game that starts with consecutively numbered clouds. Some of the clouds are dangerous rain clouds, but others are safe, normal clouds. She can jump on any cloud having a number that is equal to the number of the current cloud plus 1 or 2 (meaning she can only skip over a maximum of one cloud). She must avoid the rain clouds. Determine the minimum number of jumps it will take Emma to jump from her starting position to the last cloud. It is always possible to win the game.
For each game, Emma will get an array of clouds, each with a number 0 or 1: 0 if they are safe or 1 if they must be avoided. For example, `c = [0, 1, 0, 0, 0, 1, 0]`. The number on each cloud is its index in the list so she must avoid the clouds at indexes 1 and 5. She could follow the following two paths:  0→2→4→6 or 0→2→3→4→6. The first path takes 3 jumps while the second takes 4.
#### Function Description
Complete the `jumpingOnClouds` function in the editor below. It should return the minimum number of jumps required, as an integer.
`jumpingOnClouds` has the following parameter:
- c: an array of  0s and 1s
#### Input Format
The first line contains an integer *n*, the total number of clouds. The second line contains *n* space-separated 0s and 1s describing clouds.
#### Constraints
- n <= 100
- The first and last cloud must be labeled 0
#### Output Format
Print the minimum number of jumps needed to win the game.
#### Sample Input 0
```
7
0 0 1 0 0 1 0
```
#### Sample Output 0
`4`
#### Explanation 0:
Emma must avoid `c[2]` and `c[5]`. She can win the game with a minimum of 4 jumps:
![Explanation 0](https://s3.amazonaws.com/hr-challenge-images/20832/1461134731-c258160d15-jump2.png)

#### Sample Input 1
```
6
0 0 0 0 1 0
```
#### Sample Output 1
`3`
#### Explanation 1:
The only cloud to avoid is `c[4]`. Emma can win the game in 3 jumps:
![Explanation 1](https://s3.amazonaws.com/hr-challenge-images/20832/1461136358-764298d363-jump5.png)

#### SOLUTION
```js
function jumpingOnClouds(c) {
  let jumps = 0
  for (let i = 1; i < c.length; i++) {
    if (c[i] === 0) {
      if (c[i+1] === 0 && c[i-1] !== 1) i++
      jumps++
    }
  }
  return jumps
}
```

---

### [Left Rotation](https://www.hackerrank.com/challenges/ctci-array-left-rotation/problem)
A left rotation operation on an array shifts each of the array's elements **1** unit to the left. For example, if **2** left rotations are performed on array **[1, 2, 3, 4, 5]**, then the array would become **[3, 4, 5, 1, 2]**.

Given an array **a** of **n** integers and a number, **d**, perform **d** left rotations on the array. Return the updated array to be printed as a single line of space-separated integers.

#### Function Description
Complete the function rotLeft in the editor below. It should return the resulting array of integers.
rotLeft has the following parameter(s):
- An array of integers **a**.
- An integer **d**, the number of rotations.

#### Input Format
The first line contains two space-separated integers **n** and **d**, the size of **a** and the number of left rotations you must perform.
The second line contains **n** space-separated integers **a[i]**.

#### Constraints
- **1 <= n <= 10^5**
- **1 <= d <= n**
- **1 <= a[i] <= 10^6**

#### Output Format
Print a single line of **n** space-separated integers denoting the final state of the array after performing **d** left rotations.

#### Sample Input
```
5 4
1 2 3 4 5
```

#### Sample Output
`5 1 2 3 4`

#### Explanation
When we perform **d = 4** left rotations, the array undergoes the following sequence of changes:
**[1, 2, 3, 4, 5] -> [2, 3, 4, 5, 1] -> [3, 4, 5, 1, 2] -> [4, 5, 1, 2, 3] -> [5, 1, 2, 3, 4]**

#### SOLUTION
```js
function rotLeft(a, d) {
  const result = [...a]
  for (let i = 0; i < d; i++) {
    const first = result.shift()
    result.push(first)
  }
  return result
}
```

---
### [2D Array - Maximum Hourglass](https://www.hackerrank.com/challenges/2d-array/problem)
Given a **6 x 6** 2D Array, **arr**:
```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
```
An hourglass in **A** is a subset of values with indices falling in this pattern in **arr**'s graphical representation:
```
a b c
  d
e f g
```
There are **16** hourglasses in **arr**. An hourglass sum is the sum of an hourglass' values. Calculate the hourglass sum for every hourglass in **arr**, then print the maximum hourglass sum. The array will always be **6 x 6**.

#### Example
arr =
```
-9 -9 -9  1 1 1 
 0 -9  0  4 3 2
-9 -9 -9  1 2 3
 0  0  8  6 6 0
 0  0  0 -2 0 0
 0  0  1  2 4 0
```
The **16** hourglass sums are:
```
-63, -34, -9, 12, 
-10,   0, 28, 23, 
-27, -11, -2, 10, 
  9,  17, 25, 18
```
The highest hourglass sum is **28** from the hourglass beginning at row **1**, column **2**:
```
0 4 3
  1
8 6 6
```
**Note:** If you have already solved the Java domain's Java 2D Array challenge, you may wish to skip this challenge.

#### Function Description
Complete the function hourglassSum in the editor below.
hourglassSum has the following parameter(s):

- int arr[6][6]: an array of integers

#### Returns
- int: the maximum hourglass sum

#### Input Format
Each of the **6** lines of inputs **arr[i]** contains **6** space-separated integers **arr[i][j]**.

#### Constraints
- **-9 <= arr[i][j] <= 9**
- **0 <= i, j <= 5**

#### Output Format
Print the largest (maximum) hourglass sum found in **arr**.

#### Sample Input
```
1 1 1 0 0 0
0 1 0 0 0 0
1 1 1 0 0 0
0 0 2 4 4 0
0 0 0 2 0 0
0 0 1 2 4 0
```

#### Sample Output
`19`

#### Explanation
**arr** contains the following hourglasses:
![hourglasses](https://s3.amazonaws.com/hr-assets/0/1534256743-35b846ad4a-hourglasssum.png)

The hourglass with the maximum sum **(19)** is:
```
2 4 4
  2
1 2 4
```
#### SOLUTION
```js
function hourglassSum(arr) {
  const values = []
  const maxRowCol = arr.length - 2
  for (let i = 0; i < maxRowCol; i++) {
    for (let j = 0; j < maxRowCol; j++) {
        values.push(
            arr[i][j] + arr[i][j+1] + arr[i][j+2] +
            arr[i+1][j+1] +
            arr[i+2][j] + arr[i+2][j+1] + arr[i+2][j+2]
        )
    }
  }
  return Math.max(...values)
}
```
---

### [Queue Position Swapping](https://www.hackerrank.com/challenges/new-year-chaos/problem)
There are people waiting in line for a rollercoaster ride, and each person wears a sticker indicating their *initial* position in the queue. Initial positions increment by **1** from **1** at the front of the line to **n** at the back.
Any person in the queue can ask the person *directly in front* of them to swap positions. If two people swap positions, they still wear the same sticker denoting their original places in line. One person can swap with *at most two others*. For example, if **n = 8** and **Person 5** swaps with **Person 4**, the queue will look like this: 1, 2, 3, 5, 4, 6, 7, 8.
Fascinated by this chaotic queue, you decide you must know the minimum number of swaps that took place to get the queue into its current state!

#### Function Description
Complete the function *minimumSwaps* in the editor below. It must print an integer representing the minimum number of swaps necessary, or `Too chaotic` if the line configuration is not possible.
minimumSwaps has the following parameter(s):
- *q_count*: the length of the array
- *q*: an array of integers

#### Input Format
The first line contains an integer *t*, the number of test cases.
Each of the next *t* pairs of lines are as follows:
- The first line contains an integer *t*, the number of people in the queue
- The second line has *n* space-separated integers describing the final state of the queue.

#### Constraints
- 1 <= t <= 10
- 1 <= n <= 10^5

#### Output Format
Print an integer denoting the minimum number of swaps needed to get the queue into its final state. Print `Too chaotic` if the state is invalid, i.e. it requires a person to have swapped with more than **2** people.

#### Sample Input
```
2
5
2 1 5 3 4
5
2 5 1 3 4
```

#### Sample Output
```
3
Too chaotic
```

#### Explanation
**Test Case 1**
The initial state:
![the initial state](https://s3.amazonaws.com/hr-challenge-images/494/1451665589-31d436ba19-pic11.png)
After person **5** moves one position ahead by asking person **4**:
![moves one position ahead](https://s3.amazonaws.com/hr-challenge-images/494/1451665679-6504422ed9-pic2.png)
Now person **5** moves another position ahead by asking person **3**:
![moves another position ahead](https://s3.amazonaws.com/hr-challenge-images/494/1451665818-27bd62bb0d-pic3.png)
And person **2** moves one position ahead by asking person **1**:
![moves one position ahead](https://s3.amazonaws.com/hr-challenge-images/494/1451666025-02a2395a00-pic5.png)
So the final state is **2, 1, 5, 3, 4** after three swapping operations.

**Test Case 2**
No person can swap with more than two people, so it's not possible to achieve the input state.

#### SOLUTION
```js
// Complete the minimumSwaps function below.
function minimumSwaps(q) {
  var result = 0
  let expectedFirst = 1
  let expectedSecond = 2
  let expectedThird = 3
  
  for (let i = 0; i < q.length; i++) {
    const currentValue = q[i]
    if (currentValue === expectedFirst) {
      expectedFirst = expectedSecond
      expectedSecond = expectedThird
      ++expectedThird
    } else if (currentValue === expectedSecond) {
      ++result
      expectedSecond = expectedThird
      ++expectedThird
    } else if (currentValue === expectedThird) {
      result += 2
      ++expectedThird
    } else {
      result = "Too chaotic"
      break
    }
  }
  console.log(result)
  return result
}
```
---

### [Minimum Swaps to Sort Array](https://www.hackerrank.com/challenges/minimum-swaps-2/problem)
You are given an unordered array consisting of consecutive integers **[1, 2, 3, ..., n]** without any duplicates. You are allowed to swap any two elements. You need to find the minimum number of swaps required to sort the array in ascending order.

For example, given the array **arr = [7, 1, 3, 2, 4, 5, 6]** we perform the following steps:
```
i   arr                         swap (indices)
0   [7, 1, 3, 2, 4, 5, 6]   swap (0,3)
1   [2, 1, 3, 7, 4, 5, 6]   swap (0,1)
2   [1, 2, 3, 7, 4, 5, 6]   swap (3,4)
3   [1, 2, 3, 4, 7, 5, 6]   swap (4,5)
4   [1, 2, 3, 4, 5, 7, 6]   swap (5,6)
5   [1, 2, 3, 4, 5, 6, 7]
```
It took **5** swaps to sort the array.

#### Function Description
Complete the function minimumSwaps in the editor below. It must return an integer representing the minimum number of swaps to sort the array.
minimumSwaps has the following parameter(s):

- arr: an unordered array of integers

#### Input Format
The first line contains an integer, **n**, the size of **arr**.
The second line contains **n** space-separated integers **arr[i]**.

#### Constraints
- **1 <= n <= 10^5**
- **1 <= arr[i] <= n**

#### Output Format
Return the minimum number of swaps to sort the given array.

#### Sample Input 0
```
4
4 3 1 2
```
#### Sample Output 0
`3`
#### Explanation 0
Given array **arr : [4, 3, 1, 2]**
After swapping **(0, 2)** we get **arr: [1, 3, 4, 2]**
After swapping **(1, 2)** we get **arr: [1, 4, 3, 2]**
After swapping **(1, 3)** we get **arr: [1, 2, 3, 4]**
So, we need a minimum of **3** swaps to sort the array in ascending order.

#### Sample Input 1
```
5
2 3 4 1 5
```
#### Sample Output 1
`3`
#### Explanation 1
Given array **arr : [2, 3, 4, 1, 5]**
After swapping **(2, 3)** we get **arr: [2, 3, 1, 4, 5]**
After swapping **(0, 1)** we get **arr: [3, 2, 1, 4, 5]**
After swapping **(0, 2)** we get **arr: [1, 2, 3, 4, 5]**
So, we need a minimum of **3** swaps to sort the array in ascending order.

#### Sample Input 2
```
7
1 3 5 2 4 6 7
```
#### Sample Output 2
`3`
#### Explanation 2
Given array **arr : [1, 3, 5, 2, 4, 6, 7]**
After swapping **(1, 3)** we get **arr: [1, 2, 5, 3, 4, 6, 7]**
After swapping **(2, 3)** we get **arr: [1, 2, 3, 5, 4, 6, 7]**
After swapping **(3, 4)** we get **arr: [1, 2, 3, 4, 5, 6, 7]**
So, we need a minimum of **3** swaps to sort the array in ascending order.

#### SOLUTION
```js
// Complete the minimumSwaps function below.
function minimumSwaps(arr) {
  let swaps = 0;
  for(let i = 0; i < arr.length - 1; i++){
    if(arr[i] !== i+1) {
      arr[arr.lastIndexOf(i+1)] = arr[i];
      swaps++;
    }
  }
  return swaps;
}
```

---

### [Searching for difference Pairs](https://www.hackerrank.com/challenges/pairs/problem)
You will be given an array of integers and a target value. Determine the number of pairs of array elements that have a difference equal to a target value.
For example, given an array of [1, 2, 3, 4] and a target value of 1, we have three values meeting the condition: **2 - 1 = 1**,** 3 - 2 = 1** and **4 - 3 = 1**.

#### Function Description
Complete the pairs function below. It must return an integer representing the number of element pairs having the required difference.
pairs has the following parameter(s):
- k: an integer, the target difference
- arr: an array of integers

#### Input Format
The first line contains two space-separated integers **n** and **k**, the size of **arr** and the target value.
The second line contains **n** space-separated integers of the array **arr**.

#### Constraints
- **2 <= n <= 10^5**
- **0 < k < 10^9**
- **0 < arr[i] < 2^31 - 1**
- each integer **arr[i]** will be unique

#### Output Format
An integer representing the number of pairs of integers whose difference is **k**.

#### Sample Input
```
5 2
1 5 3 4 2 
```

#### Sample Output
`3`

#### Explanation
There are 3 pairs of integers in the set with a difference of 2: [5,3], [4,2] and [3,1] .

#### SOLUTION
```js
// Complete the pairs function below.
function pairs(k, arr) {
  let pairs = 0
  const memo = {}
  const sortDesc = arr.sort((a, b) => b-a)
  for(let i = 0; i < sortDesc.length; i++) {
      if (sortDesc[i] > k) {
          if (memo[sortDesc[i]]) {
              pairs++
              continue
          }
          const diff = sortDesc[i] - k
          for (let j = i + 1; j < sortDesc.length; j++) {
              if (sortDesc[j] === diff) {
                  memo[sortDesc[i]] = 1
                  pairs++
                  break
              }
          }
      } else {
          break
      }
  }
  return pairs
}
```

---

### [Add Values to Array Ranges](https://www.hackerrank.com/challenges/crush/problem)
Starting with a 1-indexed array of zeros and a list of operations, for each operation add a value to each of the array element between two given indices, inclusive. Once all operations have been performed, return the maximum value in your array.
For example, the length of your array of zeros *n* = 10. Your list of queries is as follows:
```
a b k
1 5 3
4 8 7
6 9 1
```
Add the values of *k* between the indices *a* and *b* inclusive:
```
index →  1 2 3  4  5 6 7 8 9  10
        [0,0,0, 0, 0,0,0,0,0, 0]
        [3,3,3, 3, 3,0,0,0,0, 0]
        [3,3,3,10,10,7,7,7,0, 0]
        [3,3,3,10,10,8,8,8,1, 0]
```
The largest value is 10 after all operations are performed.
#### Function Description
Complete the function *arrayManipulation*  in the editor below. It must return an integer, the maximum value in the resulting array..
arrayManipulation has the following parameters:
- *n* - the number of elements in your array.
- *queries* - a two dimensional array of queries where each *queries[i]* contains three integers, *a*, *b* and *k*.
#### INPUT FORMAT
The first line contains two space-separated integers *n* and *m*, the size of the array and the number of operations.
Each of the next *m* lines contains three space-separated integers ***a***, ***b*** and ***k***, the left index, right index and summand.
#### CONSTRAINTS
- 3 <= *n* <= 10^7
- 1 <= *m* <= 2*10^5
- 1 <= *a* <= *b* <= *n* 
- 0 <= *k* <= 10^9
#### OUTPUT FORMAT
Return the integer maximum value in the finished array.
#### SAMPLE INPUT
```
5 3
1 2 100
2 5 100
3 4 100
```
#### SAMPLE OUTPUT
```
200
```
#### EXPLANATION
After the first update list will be 100 100 0 0 0.

After the second update list will be 100 200 100 100 100.

After the third update list will be 100 200 200 200 100.

The required answer will be 200.
#### SOLUTION
- Brute force 1 - O(n*k)
```js
function arrayManipulation(n, queries) {
    const operations = new Array(n).fill(0)
    let maxValue = 0
    for (let i = 0; i < queries.length; i++) {
        const a = queries[i][0]
        const b = queries[i][1]
        const k = queries[i][2]
        for (let j = a - 1; j < b; j++) {
            operations[j] += k
            if (operations[j] > maxValue) maxValue = operations[j]
        }
    }
    return maxValue 
}
```
- Brute force 2 - O(n*k)
```js
function arrayManipulation(n, queries) {
    let maxValue = 0
    for (let i = 1; i <= n; i++) {
        let value = 0
        for (let j = 0; j < queries.length; j++) {
            const a = queries[j][0]
            const b = queries[j][1]
            const k = queries[j][2]
            if (a <= i && i <= b) value += k
        }
        if (value > maxValue) maxValue = value
    }
    return maxValue
}
```
- Optimal solution - O(k+n)
```js
function arrayManipulation(n, queries) {
    const operations = new Array(n).fill(0)
    let maxValue = 0
    for (let i = 0; i < queries.length; i++) {
        const a = queries[i][0]
        const b = queries[i][1]
        const k = queries[i][2]
        operations[a-1] += k
        operations[b] -= k
    }
    let sum = 0
    for (let i = 0; i < n; i++) {
        sum += operations[i]
        maxValue = Math.max(sum, maxValue)
    }
    return maxValue
}
```

---
