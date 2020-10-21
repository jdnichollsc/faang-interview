## Coding Interview Prep
---
### Encode Secret Message
You have a note to send to your friend, but you don't want anyone to recognize your handwriting. You want to know if you can cut out whole words from a magazine and use them to create a secret message. The words in your note are *case-sensitive* and you *must* use only whole words available in the magazine. You *cannot* use substrings or concatenation to create the words you need.
Given the words in the magazine and the words in the note, print Yes if you can replicate your note *exactly* using whole words from the magazine; otherwise, print No.
For example, the note is "Coding is fun". The magazine contains only "coding is fun". The magazine has all the right words, but there's a case mismatch. The answer is No.
#### Function Description
Complete the *checkMagazine* function in the editor below. It must print Yes if the note can be formed using the magazine, or No.
checkMagazine has the following parameters:
- *magazine*: an array of strings. Each a word in the magazine.
- *note*: an array of strings. Each a word in the note.
#### Input Format
The first line contains two space-separated integers, *m* and *n*, the numbers of words in the *magazine* and the *note*.
The second line contains *m* space-separated strings, each *magazine[i]*.
The second line contains *n* space-separated strings, each *note[i]*.
#### Constraints
- 1 <= *m*, *n* <= 30000
- The length of each word is between 1 and 5 characters
- Each word consists of English alphabetic letters (i.e., *a* to *z* and *A* to *Z*).
#### Output Format
Print Yes if you can use the magazine to create a copy of your note. Otherwise, print No.
#### Sample Input 0
```
6 4
give me one hamburger today night
give one hamburger today
```
#### Sample Output 0
`Yes`
#### Sample Input 1
```
6 5
two times three is not four
two times two is four
```
#### Sample Output 1
`No`
#### Explanation 1
'two' only occurs once in the magazine.
#### Sample Input 2
```
7 4
ive got a lovely bunch of coconuts
ive got some coconuts
```
#### Sample Output 2
`No`
#### Explanation 2
The magazine is missing the word *some*.
#### SOLUTION
```js
// Complete the checkMagazine function below.
function checkMagazine(magazine, note) {
  const magazineWords = [...magazine]
  let result = 'Yes'
  for (let i = 0; i < note.length; i++) {
      const indexMagazineWord = magazineWords.indexOf(note[i])
      if (indexMagazineWord < 0) {
          result = 'No'
          break
      } else {
          magazineWords.splice(indexMagazineWord, 1)
      }
  }
  return console.log(result)
}
```

---


### Common Substring Between Two Strings
Given two strings, determine if they share a common substring. A substring may be as small as one character.
For example, the words "a", "and", "art" share the common substring *a*. The words "be" and "cat" do not share a substring.

#### Function Description
Complete the function *twoStrings* in the editor below. It should return a string, either Yes or No based on whether the strings share a common substring.
twoStrings has the following parameter(s):
- *s1*, *s2*: two strings to analyze.
#### Input Format
The first line contains a single integer *p*, the number of test cases.
The following *p* pairs of lines are as follows:
- The first line contains string ***s1***.
- The second line contains string ***s2***.
#### Constraints
*s1* and *s2* consist of characters in the range ascii[a-z].
- 1 <= ***p*** <= 10
- 1 <= |***s1***|,|***s2***| <= 10^5
#### Output Format
For each pair of strings, return Yes or No.
#### Sample Input 0
```
2
hello
world
hi
world
```
#### Sample Output 0
```
YES
NO
```
#### Explanation 0
We have ***p*** = **2** pairs to check:
1. ***s*1** = **"hello"**, ***s*2** = **"world"**. The substrings **"o"** and **"l"** are common to both strings.
2. ***a*** = **"hi"**, ***b*** = **"world"**. ***s*1** and ***s*2** share no common substrings.
#### SOLUTION
```js
// Complete the twoStrings function below.
function twoStrings(s1, s2) {
    const comparision = s1.length > s2.length ? {
        string: s1,
        characters: s2.split('')
    } : {
        string: s2,
        characters: s1.split('')
    }
    
    const hasCommon = comparision.characters.some((character) => comparision.string.includes(character))
    return hasCommon ? 'YES' : 'NO'
}
```

---

### Frequency Queries
You are given *q* queries. The first integer in each query represents one of the following three operations:
- **1 *x***: Insert x in your data structure.
- **2 *y***: Delete one occurence of y from your data structure, if present.
- **3 *z***: Check if any integer is present whose frequency is exactly *z*. If yes, print 1 else 0.
The second integer in the query represents x, y, or z, depending on the operation in the query.
The queries are given in the form of a 2-D array *queries* of size *q* where *queries[i]*[0] contains the operation, and *queries[i]*[1] contains the data element. For example, you are given array 
*queries* = [(1,1). (2,2), (3,2), (1,1), (1,1), (2,1), (3,2)]. The results of each operation are:
```
Operation  Array   Output
)1,1)      [1]
(2,2)      [1]
(3,2)              0
(1,1)      [1,1]
(1,1)      [1,1,1]
(2,1)      [1,1]
(3,2)              1
```
Return an array with the output: [0,1].
#### Function Description
Complete the *freqQuery* function in the editor below. It must return an array of integers, where each element is a 1 if there is at least one element value with the queried number of occurrences in the current array, or 0 if there is not.
freqQuery has the following parameter(s):
- *queries*: a 2-d array of integers.
#### Input Format
The first line contains of an integer *q*, the number of queries.
Each of the next *q* lines containes two integers denoting the 2-d array *queries*.
#### Constraints
- 1 <= *q*
- 1 <= *x,y,z*
- All *queries[i]*[0] are either 1, 2, or 3
- 1 <= *queries[i]*[1]
#### Output Format
Return an integer array consisting of all the outputs of queries of type 3
#### Sample Input 0
```
8
1 5 
1 6
3 2
1 10
1 10
1 6
2 5
3 2
```
#### Sample Output 0
```
0
1
```
#### Explanation 0
For the first query of type 3, there is no integer whose frequency is 2 (*array* = [5, 6]). So answer is 0.
For the second query of type 3, there are two integers in *array* = [6, 10, 10, 6] whose frequency is 2 (*integers* = 6 and 10). So, the answer is 1.
#### Sample Input 1
```
4
3 4
2 1003
1 16
3 1
```
#### Sample Output 1
```
0
1
```
#### Explanation 1
For the first query of type 3, there is no integer of frequency 4. The answer is 0.
For the second query of type 3, there is one integer, 16 of frequency 1 so the answer is 1.
#### Sample Input 2
```
10
1 3
2 3
3 2
1 4
1 5
1 5
1 4
3 2
2 4
3 2
```
#### Sample Output 2
```
0
1
1
```
#### Explanation 2
When the first output query is run, the array is empty. We insert two 4's and two 5's before the second output query, *arr* = [4, 5, 5, 4] so there are two instances of elements occurring twice. We delete a 4 and run the same query. Now only the instances of 5 satisfy the query.
#### SOLUTION
```js
// Complete the freqQuery function below.
function freqQuery(queries) {
  const frequencies = {}
  const quantities = {}
  return queries.reduce(function (output, query) {
    const [operation, value] = query
    if (operation === 1) {
        if (frequencies[value])
            quantities[frequencies[value]]--
        const newQuantity = (frequencies[value] || 0) + 1
        frequencies[value] = newQuantity
        quantities[newQuantity] = (quantities[newQuantity] || 0) + 1
    } else if (operation === 2) {
        if (frequencies[value]) {
            quantities[frequencies[value]]--
            const newQuantity = (frequencies[value] || 0) - 1
            if (newQuantity > 0) {
                frequencies[value] = newQuantity
                quantities[newQuantity] = (quantities[newQuantity] || 0) + 1
            } else {
                delete frequencies[value]
            }
        }
    } else {
        output.push(quantities[value] ? 1 : 0)
    }
    return output
  }, [])
}
```

--- 

### Ice Cream Shop
The Ice Cream Shop offers many flavors. Each flavor has a cost associated with it.
Given the value of *money* and the *cost* of each flavor for *t* trips to the Ice Cream Shop, choose two *distinct* flavors such that you spend your entire pool of money during each visit. ID numbers are the *1-based* index number associated with a *cost*. For each trip to the parlor, print the ID numbers for the two types of ice cream that you purchase as two space-separated integers on a new line. You must print the smaller ID first and the larger ID second.
For example, there are ***n*** = **5** flavors having ***cost*** = [**2, 1, 3, 5, 6**]. You have *money* = 5 to spend. You would purchase flavor ID's 1 and 3 for a cost of 2 + 3 = 5. Use 1 based indexing for your response.
**Note:**
- Two ice creams having unique IDs *i* and *j* have the same cost (i.e., cost[i] == cost[j])
- There will always be a unique solution.
#### Function Description
Complete the function *whatFlavors*  in the editor below. It must determine the two flavors you will purchase and print them as two space-separated integers on a line.
whatFlavors has the following parameter(s):
- *cost*: an array of integers representing price for a flavor.
- *money*: an integer representing the amount of money you have to spend.
#### Input Format
The first line contains an integer, *t*, the number of trips to the ice cream shop.
Each of the next *t* sets of 3 lines is as follows:
- The first line contains *money*.
- The second line contains an integer, *n*, the size of the array *cost*.
- The third line contains *n* space-separated integers denoting the *cost[i]*.
#### Constraints
- 1 <= *t* <= 50
- 2 <= *money* <= 10^9
- 2 <= *n* <= 5*10^4
- 1 <= *cost[i]* <= 10^9
#### OUTPUT FORMAT
Print two space-separated integers denoting the respective indices for the two distinct flavors you choose to purchase in ascending order. Recall that each ice cream flavor has a unique ID number in the inclusive range from 1 to |*cost*|.
#### SAMPLE INPUT
```
2
4
5
1 4 5 3 2
4
4
2 2 4 3
```
#### SAMPLE OUTPUT
```
1 4
1 2
```
#### EXPLANATION
You make the following two trips to the ice cream shop:
1. The first time, *money* = 4 dollars. There are five flavors available that day and flavor 1 and 4 have a total cost of 1 + 3 = 4.
2. The second time, *money* = 4 dollars. There are four flavors available that day and flavor 1 and 2 have a total cost of 2 + 2 = 4.
#### SOLUTION
```js
// Complete the whatFlavors function below.
function whatFlavors(cost, money) {
  const possibleFlavors = {}
  let response = []
  for (let i = 0; i < cost.length; i++) {
      if (money > cost[i]) {
        const diff = possibleFlavors[money - cost[i]]
        if (diff) {
            response = [diff, i + 1]
            break
        }
        possibleFlavors[cost[i]] = i + 1
      }
  }
  console.log(response[0], response[1])
  return response
}
```

---

### Count Triplets
You are given an array and you need to find number of tripets of indices (***i, j, k***) such that the elements at those indices are in geometric progression https://en.wikipedia.org/wiki/Geometric_progression for a given common ratio *r* and  *i* < *j* < *k*.
For example, ***arr** = [**1, 4, 16, 64**]. If *r* = 4 we have [1, 4, 16] and [4, 16, 64] at indices (0, 1, 2) and [1, 2, 3].
#### Function Description
Complete the *countTriplets* function in the editor below. It should return the number of triplets forming a geometric progression for a given *r* as an integer.
countTriplets has the following parameter(s):
- *arr*: an array of integers.
- *r*: an integer, the common ratio.
#### Input Format
The first line contains two space-separated integers *n* and *r*, the size of *arr* and the common ratio.
The next line contains *n* space-separated integers *arr[i]*
- The first line contains *money*.
- The second line contains an integer, *n*, the size of the array *cost*.
- The third line contains *n* space separated integers denoting the *cost[i]*.
#### Constraints
- 1 <= *n* <= 10^5
- 1 <= *r* <= 10^9
- 1 <= *arr[i]* <= 10^9
#### OUTPUT FORMAT
Return the count of triplets that form a geometric progression.
#### SAMPLE INPUT 0
```
4 2
1 2 2 4
```
#### SAMPLE OUTPUT 0
```
2
```
#### EXPLANATION 0
There are 2 triplets in satisfying our criteria, whose indices are (0, 1, 3) and (0, 2, 3).
#### SAMPLE INPUT 1
```
6 3
1 3 9 9 27 81
```
#### SAMPLE OUTPUT 1
```
6
```
#### EXPLANATION 1
The triplets satisfying are index (0, 1, 2), (0, 1, 3), (1, 2, 4), (1, 3, 4), (2, 4, 5) and (3, 4, 5)
#### SAMPLE INPUT 2
```
5 5
1 5 5 25 125
```
#### SAMPLE OUTPUT 2
```
4
```
#### EXPLANATION 2
The triplets satisfying are index (0, 1, 3), (0, 2, 3), (1, 3, 4), (2, 3, 4).
#### SOLUTION
```js
// Complete the countTriplets function below.
function countTriplets(arr, r) {
  let count = 0
  const elements = {}
  const pairs = {}
  for (let i = 0; i < arr.length; i++) {
    const element = arr[i]
    if (pairs[element/r]) {
        count += pairs[element/r]
    }
    if (elements[element/r]) {
        pairs[element] = (pairs[element] || 0) + elements[element/r]
    }
    elements[element] = (elements[element] || 0) + 1
  }
  return count
}
```

---

### Count Substrings Anagrams
Two stringsare anagrams of each other if the letters of one string can be rearranged to form the other string. Given a string, find the number of pairs of substrings of the string that are anagrams of each other.
For example *s* = *mom*, the list of all anagrammatic pairs is [*m, m*], [*mo, om*] at positions [[0], [2], [0, 1], [1, 2]] respectively.
#### Function Description
Complete the function *anagramPairs* in the editor below. It must return an integer that represents the number of anagrammatic pairs of substrings in *s*.
anagramPairs has the following parameter(s):
- *s*: a string.
#### Input Format
The first line contains an integer *q*, the number of queries.
Each of the next *q* lines contains a string *s* to analyze.
#### Constraints
- 1 <= *q* <= 10
- 2 <= |*s*| <= 100
- String *s* contains only lowercase letters ϵ ascii[a-z].
#### OUTPUT FORMAT
For each query, return the number of unordered anagrammatic pairs.
#### SAMPLE INPUT 0
```
2
abba
abcd
```
#### SAMPLE OUTPUT 0
```
4
0
```
#### EXPLANATION 0
The list of all anagrammatic pairs is [*a, a*], [*ab, ba*], [*b, b*] and [*abb, bba*] at positions [[0], [3]], [[0, 1], [2, 3]], [[1], [2]] and [[0, 1, 2], [1, 2, 3]] respectively. 
No anagrammatic pairs exist in the second query as no character repeats.
#### SAMPLE INPUT 1
```
2
i f a i l u h k q q
k k k k
```
#### SAMPLE OUTPUT 1
```
3
10
```
#### EXPLANATION 1
For the first query we have anagram pairs [*i, i*], [*q, q*] and [*ifa, fai*] at positions [[0], [3]],  [[8], [9]] and [[0, 1, 2], [1, 2, 3]] respectively.
For the second query: 
There are 6 anagrams of the form [k, k] at positions [[0], [1]], [[0], [2]], [[0], [3]], [[1], [2]], [[1], [3]] and [[2], [3]].
There are 3 anagrams of the form [kk, kk] at positions [[0, 1], [1, 2]], [[0, 1], [2, 3]] and [[1, 2], [2, 3]].
There is 1 anagram of the form [kkk, kkk] at position [[0, 1, 2], [1, 2, 3]].
#### SAMPLE INPUT 2
```
1
cdcd
```
#### SAMPLE OUTPUT 2
```
5
```
#### EXPLANATION 2
There are two anagrammatic pairs of length 1: [c, c] and [d, d]
There are three anagrammatic pairs of length 2: [cd, dc], [cd, cd], [dc, cd] at positions [[0, 1], [1, 2]], [[0, 1], [2, 3]], [[1, 2], [2, 3]] respectively.
#### SOLUTION
```js
/*
 * Complete the 'anagramPairs' function below.
 *
 * The function is expected to return an INTEGER.
 * The function accepts STRING s as parameter.
 */

function anagramPairs(s) {
    // Write your code here
    const doubles = s.split('').filter((c, i) => s.indexOf(c) !== i).length
    if (!doubles) return 0

    const parts = []
    for (let i = 0; i < s.length; i++) {
        for (let j = i + 1; j <= s.length; j++) {
            const subString = s.substring(i, j).split('').sort().join('')
            parts.push(subString)
        }
    }
    let counter = 0
    for (let i = 0; i < parts.length; i++) {
        for (let j = i + 1; j <= parts.length; j++) {
            if (parts[j] === parts[i]) counter++
        }
    }
    return counter
}
```

---
