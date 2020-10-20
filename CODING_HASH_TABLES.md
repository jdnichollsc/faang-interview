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
