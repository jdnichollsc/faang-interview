# Facebook Coding Interview Prep

## Arrays

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
