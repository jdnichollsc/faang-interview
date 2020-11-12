## Greedy Algorithms
---
### [Greedy Florist](https://www.hackerrank.com/challenges/greedy-florist/problem)
A group of friends want to buy a bouquet of flowers. The florist wants to maximize his number of *new* customers and the money he makes. To do this, he decides he'll multiply the price of each flower by the number of that customer's previously purchased flowers plus 1. The first flower will be original price, (0 + 1) x **original price**, the next will be (1 + 1) x **original price** and so on.
Given the size of the group of friends, the number of flowers they want to purchase and the original prices of the flowers, determine the minimum cost to purchase all of the flowers.
For example, if there are *k = 3* friends that want to buy *n = 4* flowers that cost *v* = [1, 2, 3, 4]  each will buy one of the flowers priced [2, 3, 4] at the original price. Having each purchased *x = 1* flower, the first flower in the list, *c[0]*, will now cost *(current purchase + previous purchase) x c[0]* = (1 + 1) x 1 = 2. The total cost will be 2 + 3 + 4 + 2 = 11.
#### Function Description
Complete the *getMinimumCost* function in the editor below. It should return the minimum cost to purchase all of the flowers.
getMinimumCost has the following parameter(s):
- *c*: an array of integers representing the original price of each flower
- *k*: an integer, the number of friends.
#### Input Format
The first line contains two space-separated integers *n* and *k*, the number of flowers and the number of friends.
The second line contains *n* space-separated positive integers *c[i]*, the original price of each flower.
#### Constraints
- 1 <= *n, k* <= 100
- 1 <= *c[i]* <= 10^6
- answer < 2^31
- 1 <= *i* <= *n*
#### Output Format
Print the minimum cost to buy all *n* flowers
#### Sample Input 0
```
3 3
2 5 6
```
#### Sample Output 0
```
13
```
#### Explanation 0
There are *n = 3* flowers with costs *c = [2, 5, 6]* and *k = 3* people in the group. If each person buys one flower, the total cost of prices paid is 2 + 5 + 6 = 13 dollars. Thus, we print 13 as our answer.
#### Sample Input 1
```
3 2
2 5 6
```
#### Sample Output 1
```
15
```
#### Explanation 1
There are *n = 3* flowers with costs *c = [2, 5, 6]* and *k = 2* people in the group. We can minimize the total purchase cost like so: 
1. The first person purchases 2 flowers in order of decreasing price; this means they buy the more expensive flower (*c1* = 5) first at price *p1* = (0 + 1) x 5 = 5 dollars and the less expensive flower (*c0 = 2*) second at price *p0* = (1 + 1) x 2 = 4 dollars.
2. The second person buys the most expensive flower at price *p2* = (0 + 1) x 6  = 6 dollars
We then print the sum of these purchases, which is 5 + 4 + 6, as our answer.
#### Sample Input 2
```
5 3
1 3 5 7 9
```
#### Sample Input 2
```
29
```
#### Explanation 2
The friends buy flowers for 9, 7 and 3, 5 and 1 for a cost of 9 + 7 + 3 * (1 + 1) + 5 + 1 * (1 + 1) = 29.
#### SOLUTION
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
You will be given a list of integers, *arr*, and a single integer *k*. You must create an array of length *k* from elements of *arr* such that its *unfairness* is minimized. Call that array ***subarr***. Unfairness of an array is calculated as
    ***max(subarr) - min(subarr)***
Where:
- *max* denotes the largest integer in ***subarr***
- *min* denotes the smallest integer in ***subarr***
As an example, consider the array [1, 4, 7, 2] with a *k* of 2. Pick any two elements, test ***subarr*** = [4, 7] ***unfairness*** = ***max(4, 7) - min(4, 7)*** = 7 - 4 = 3
Testing for all pairs, the solution [1, 2] provides the minimum unfairness.
**Note**:: Integers in **arr** may not be unique.
#### Function Description
Complete the *maxMin* function in the editor below. It must return an integer that denotes the minimum possible value of *unfairness*
maxMin has the following parameter(s):
- *k*: an integer, the number of elements in the array to create
- *arr*: an array of integers
#### Input Format
The first line contains an integer *n*, the number of elements in array **arr**
The second line contains an integer *k*.
Each of the next *n* lines contains an integer *arr[i]* where 1 <= *i* < *n*
#### Constraints
- 2 <= *n* <= 10^5
- 2 <= *k* <= *n*
- 0 <= *arr[i]* <= 10^9
#### Output Format
An integer that denotes the minimum possible value of *unfairness*
#### Sample Input 0
```
7
3
10
100
300
200
1000
20
30
```
#### Sample Output 0
```
20
```
#### Explanation 0
Here *k* = 3; selecting the 3 integers 10, 20, 30, unfairness equals
```
max(10,20,30) - min(10,20,30) = 30 - 10 = 20
```
#### Sample Input 1
```
10
4
1
2
3
4
10
20
30
40
100
200
```
#### Sample Output 1
```
3
```
#### Explanation 1
Here *k* = 4; selecting the 4 integers 1, 2, 3, 4, unfairness equals
```
max(1,2,3,4) - min(1,2,3,4) = 4 - 1 = 3
```
#### Sample Input 2
```
5
2
1
2
1
2
1
```
#### Sample Output 2
```
0
```
#### Explanation 2
Here *k* = 2. *subarr* = [2, 2] or *subarr* = [1, 1] give the minimum unfairness of 0
#### SOLUTION
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
