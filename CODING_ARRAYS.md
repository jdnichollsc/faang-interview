## Facebook Coding Interview Prep
---

### Count Matching Pairs of Numbers
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

### Jumping on the Clouds
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
