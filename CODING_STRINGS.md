## Coding Interview Prep
---
### Counting Valleys on a Hike
A hiker tracks their walk through hills. During the hike, the hiker took exactly n steps. Every step is either *uphill*, U, or a *downhill*, D step. The hike starts and ends at altitude 0, and each step up or down represents a 1 unit change in altitude. We define the following terms:
- A *mountain* is a sequence of consecutive steps *above* altitude 0, starting with a step *up* from altitude 0 and ending with a step *down* to altitude 0.
- A *valley* is a sequence of consecutive steps *below* altitude 0, starting with a step *down* from altitude 0 and ending with a step *up* to altitude 0.

Given a sequence of *up* and *down* steps during the hike, **find and print the number of *valleys*** the hiker walked through.
For example, if the hiker's path is s = 'DDUUUUDD', the hiker first enters a valley 2 units deep. Then they climb out and up onto a mountain 2 units high. Finally, they return to altitude 0 and end the hike.
#### Function Description
Complete the *countingValleys* function in the editor below. It must return an integer that denotes the number of valleys the hiker walked through.
countingValleys has the following parameter(s):
- n: the number of steps taken
- s: a string describing the path
#### Input Format
The first line contains an integer n, the number of steps in the hike. The second line contains a single string s, of n characters that describe his path.
#### Constraints
- 2 <= n <= 10000000
- s contains only U's and D's
#### Output Format
Print a single integer that denotes the number of valleys the hiker walked through during their hike.
#### Sample Input
```
8
UDDDUDUU
```
#### Sample Output
`1`
#### Explanation
If we represent `_` as altitude 0, a step up as `/`, and a step down as `\`, the hike can be drawn as:
```
_/\      _
   \    /
    \/\/
```
> The hiker enters and leaves one valley.
#### SOLUTION
```js
function countingValleys(n, s) {
    const ar = s.split('')
    let altitude = 0
    return ar.reduce(function (result, step) {
        if (step === 'U' & altitude === -1) {
            result++
        }
        altitude += step === 'U' ? 1 : -1
        return result
    }, 0)
}
```

---

### Count the a's in an Infinitely Repeating String
There is a string, `s`, of lowercase English letters that is repeated infinitely many times.
Given an integer, `n`, find and print the number of letter a's in the first *n* letters of this infinite string.
For example, if the string `s = 'abcac'` and *n* = 10, the substring we consider is `'abcacabcac'`, the first 10 characters of the infinite string. There are 4 occurrences of `a` in this substring.
#### Function Description
Complete the `repeatedString` function in the editor below. It should return an integer representing the number of occurrences of `a` in the first *n* characters in the infinitely repeating string.
`repeatedString` has the following parameters:
- s: a string to repeat
- n: the number of characters to consider
#### Input Format
The first line contains a single string, *s*. 
The second line contains an integer, *n*.
#### Constraints
- The length of *s* is between 1 and 100
- *n* is a positive integer
#### Output Format
Print the number of letter a's in the first *n* letters of the infinite string created by repeating *s* infinitely many times.
#### Sample Input 0
```
aba
10
```
#### Sample Output 0
`7`
#### Explanation 0
The first *n* = 10 letters of the infinite string are `abaabaabaa`. Because there are 7 a's, we print 7 on a new line.
#### Sample Input 1
```
a
1000000000000
```
#### Sample Output 1
`1000000000000`
#### Explanation 1
Because all of the first *n* = 1000000000000 letters of the infinite string are a, we print 1000000000000 on a new line.

#### SOLUTION
```js
function repeatedString(s, n) {
    const occurrences = getOccurrences(s, 'a')
    const numberOfRepetitions = parseInt(n / s.length)
    const totalMissingLetters = n % s.length
    const restOccurrences = getOccurrences(s.substring(0, totalMissingLetters), 'a')
    return numberOfRepetitions * occurrences + restOccurrences
}

function getOccurrences(word, letter) {
    return word.split('').filter(c => c === letter).length
}
```

---

### Making Anagrams
We consider two strings to be anagrams of each other if the first string's letters can be rearranged to form the second string. In other words, both strings must contain the same exact letters in the same exact frequency For example, `bacdc` and `dcbac` are anagrams, but `bacdc` and `dcbad` are not.

Given two strings, `a` and `b`, that may or may not be of the same length, determine the minimum number of character deletions required to make `a` and `b` anagrams. Any characters can be deleted from either of the strings.
For example, if `a = cde` and `b = dcf`, we can delete `e` from string *a* and `f` from string *b* so that both remaining strings are `cd` and `dc` which are anagrams.
#### Function Description
Complete the `makeAnagram` function in the editor below. It must return an integer representing the minimum total characters that must be deleted to make the strings anagrams.
`makeAnagram` has the following parameter(s):
- *a*: a string
- *b*: a string
#### Input Format
The first line contains a single string, *a*.
The second line contains a single string, *b*.
#### Constraints
- The lengths of *a* and *b* are at least 1
- The strings *a* and *b* consist of lowercase English alphabetic letters, in other words ASCII characters from the range [a-z].
#### Output Format
Print the number of characters you must delete to make the two strings anagrams of each other.
#### Sample Input
```
cde
abc
```
#### Sample Output
`4`
#### Explanation
We delete the following characters from our two strings to turn them into anagrams of each other:
- Remove `d` and `e` from `cde` to get `c`.
- Remove `a` and `b` from `abc` to get `c`.
We must delete 4 characters to make both strings anagrams, so we print 4 on a new line.
#### SOLUTION
```js
function makeAnagram(a, b) {
    const aArray = a.split('')
    const bArray = b.split('')
    const arrays = aArray.length < bArray.length ? {
      min: aArray,
      max: bArray
    } : {
      min: bArray,
      max: aArray
    }
    let i = 0
    while (i < arrays.min.length) {
        const letter = arrays.min[i]
        const indexMax = arrays.max.indexOf(letter)
        if (indexMax >= 0) {
           arrays.min.splice(i, 1)
           arrays.max.splice(indexMax, 1)
        } else {
           i++
        }
    }
    return arrays.min.length + arrays.max.length
}
```

---

### Alternating Characters
You are given a string containing characters `A` and `B` only. Your task is to change it into a string such that there are no matching adjacent characters. To do this, you are allowed to delete zero or more characters in the string.
Your task is to find the minimum number of required deletions.
For example, given the string `s = AABAAB`, remove an `A` at positions 0 and 3 to make `s = ABAB` in 2 deletions.
#### Function Description
Complete the `alternatingCharacters` function in the editor below. It must return an integer representing the minimum number of deletions to make the alternating string.
`alternatingCharacters` has the following parameter:
- *s*: a string
#### Input Format
The first line contains an integer *q*, the number of input strings.
The next *q* lines each contain a string *s*.
#### Constraints
- *q*, the number of strings, will be between 1 and 10
- The length of each string *s* is less than 10^5
- Each string *s* will consist only of characters `A` and `B`
#### Output Format
For each string, print the minimum number of deletions required on a new line.
#### Sample Input
```
5
AAAA
BBBBB
ABABABAB
BABABA
AAABBB
```
#### Sample Output
```
3
4
0
0
4
```
#### Explanation
The characters marked red are the ones that can be deleted so that the string doesn't have matching consecutive characters.
![Explanation](https://s3.amazonaws.com/hr-assets/0/1502450721-a0a2e9b5bd-alternatingCharacter2.png)
#### SOLUTION
```js
function alternatingCharacters(s) {
  let deletions = 0
  const characters = s.split('')
  for (let i = 0; i < characters.length; i++) {
      const letter = characters[i]
      let numToDelete = 0
      for (let j = i + 1; j < characters.length; j++) {
          if (letter === characters[j]) {
              numToDelete++
          } else {
              break
          }
      }
      deletions += numToDelete
      i += numToDelete
  }
  return  deletions
}
```
---

### Character Frequencies
A string is considered to be *valid*  if all characters of the string appear the same number of times. It is also *valid*  if you can remove just 1 character anywhere in the string, and the remaining characters will occur the same number of times. Given a string ***s***, determine if it is *valid*. If so, return YES, otherwise return NO.
- if ***s*** = *abc*, it is a valid string because frequencies are {*a* : 1, *b* : 1, *c* : 1}.
- if ***s*** = *abcc*, it is also a valid string, because we can remove one *c* and have 1 of each character in the remaining string.
- if ***s*** = *abccc* however, the string is *not* valid as we can only remove one occurrence of *c*. That would leave character frequencies of {*a* : 1, *b* : 1, *c* : 1}.
#### FUNCTION DESCRIPTION
Complete the *isValid* function in the editor below. It should return either the string YES or the string NO.
isValid has the following parameter(s):
- ***s***: a string
#### INPUT FORMAT
A single string ***s***.
#### CONSTRAINTS
- 1 ≤ |***s***| ≤ 10^5
- All characters are lowercase alphabetic characters
#### OUTPUT FORMAT
Print YES if string ***s*** is *valid*, otherwise, print NO.
#### SAMPLE INPUT 0 
```
aabbcd
```
#### SAMPLE OUTPUT 0
```
NO
```
#### EXPLANATION 0
Given ***s*** = **"aabbcd"**, we would need to remove two characters, both c and d → aabb or a and b → abcd, to make it valid. We are limited to removing only one character, so ***s*** is *invalid*.
#### SAMPLE INPUT 1 
```
aabbccddeefghi
```
#### SAMPLE OUTPUT 1
```
NO
```
#### EXPLANATION 1
Frequency counts for the letters are as follows:
{'a': 2, 'b': 2, 'c': 2, 'd': 2, 'e': 2, 'f': 1, 'g': 1, 'h': 1, 'i': 1}
There are two ways to make the valid string.
- Remove 4 characters with a frequency of 1: {fghi}
- Remove 5 characters with a frequency of 2: {abcde}
Neither of these is an option.
#### SAMPLE INPUT 2 
```
abcdefghhgfedecba
```
#### SAMPLE OUTPUT 2
```
YES
```
#### EXPLANATION 2
All characters occur twice except for *e* which occurs **3** times. We can delete one instance of *e*  to have a valiid string.
#### SOLUTION
```js
// Complete the isValid function below.
function isValid(s) {
    const characters = s.split('')
    const map = new Map()
    for (let i = 0; i < characters.length; i++) {
        const character = characters[i]
        if (map.has(character)) {
            map.set(character, map.get(character) + 1)
        } else {
            map.set(character, 1)
        }
    }
    const groups = Array.from(map)
    let charSize = groups[0][1]
    let mismatch = 0
    let result = 'YES'
    for (let i = 1; i < groups.length; i++) {
        const size = groups[i][1]
        if (size !== charSize) {
            if (mismatch > 0) {
                result = 'NO'
                break
            }
            mismatch++
            if (size === 1) continue
            if (Math.abs(size - charSize) > 1) {
                result = 'NO'
                break
            }
        }
    }
    return result
}
```
---

### Special Substrings
A string is said to be a *special string* if either of two conditions is met:
- All of the characters are the same, e.g. aaa.
- All characters except the middle one are the same, e.g. aadaa.
A special substring is any substring of a string which meets one of those criteria. Given a string, determine how many special substrings can be formed from it.
For example, given the string ***s*** = **mnonopoo**, we have the following special substrings: **{m, n, o, n, o, p, o, o, non, ono, opo, oo}**.
#### FUNCTION DESCRIPTION
Complete the *substrCount* function in the editor below. It should return an integer representing the number of special substrings that can be formed from the given string.
substrCount has the following parameter(s):
- *n*: an integer, the length of string 
- *s*: a string.
#### INPUT FORMAT
The first line contains an integer, ***n*** , the length of ***s***.
The second line contains the string ***s***.
#### CONSTRAINTS
- 1 ≤ ***n*** ≤ 10^6
- Each character of the string is a lowercase alphabet.
#### OUTPUT FORMAT
Print a single line containing the count of total special substrings.
#### SAMPLE INPUT 0
```
5
asasd
```
#### SAMPLE OUTPUT 0
```
7
```
#### EXPLANATION 0
The special palindromic substrings of ***s*** = **asasd** are {a, s, a, s, d, asa, sas}.
#### SAMPLE INPUT 1
```
7
abcbaba
```
#### SAMPLE OUTPUT 1
```
10
```
#### EXPLANATION 1
The special palindromic substrings of ***s*** = **abcbaba** are {a, b, c, b, a, b, a, bcb, bab, aba}.
#### SAMPLE INPUT 2
```
4
aaaa
```
#### SAMPLE OUTPUT 2
```
10
```
#### EXPLANATION 2
The special palindromic substrings of ***s*** = **aaaa** are {a, a, a, a, aa, aa, aa, aaa, aaa, aaaa}.
 #### SOLUTION
```js
// Complete the substrCount function below.
function substrCount(n, s) {
    let counter = 0
    for (let i = 0; i < n; i++) {
        const character = s[i]
        let middlePart = character
        counter++
        for (let j = i + 1; j < n; j++) {
            if (s[j] === character) {
                counter++
                middlePart += character
            } else {
                const secondPartIndex = j + 1
                if (s.substring(secondPartIndex, secondPartIndex + middlePart.length) === middlePart) {
                    counter++
                }
                break
            }
        }
    }
    return counter
}
```
---

### Common Child
A string A is said to be a child of another string B if they match exactly, or if any number of characters in B can be deleted to form A. Given two strings of equal length, what's the longest string that can be constructed such that it is a child of both?
For example, ABCD and ABDC  have two children with maximum length 3, ABC and ABD. They can be formed by eliminating either the D or C from both strings. Note that we will not consider ABCD as a common child because we can't rearrange characters and ABCD ≠ ABDC.
 #### FUNCTION DESCRIPTION
Complete the *commonChild* function in the editor below. It should return the longest string which is a common child of the input strings.
commonChild has the following parameter(s):
- *s*1, *s*2: two equal length strings.
#### INPUT FORMAT
There are two lines with one string each ***s*1** and ***s*2**.
#### CONSTRAINTS
- 1 ≤ |***s*1**|, |***s*2**| ≤ 5000
- All character are upper case alphabets.
#### OUTPUT FORMAT
Print the length of the longest string ***s*** such that ***s*** is a child of both ***s*1** and ***s*2**.
#### SAMPLE INPUT 
```
HARRY
SALLY
```
#### SAMPLE OUTPUT 
```
2
```
#### EXPLANATION 
The longest string that can be formed by deleting zero or more characters from HARRY and SALLY is AY, whose length is 2.
#### SAMPLE INPUT 1
```
AA
BB
```
#### SAMPLE OUTPUT 1
```
0
```
#### EXPLANATION 1
AA and BB have no characters in common and hence the output is 0.
#### SAMPLE INPUT 2
```
SHINCHAN
NOHARAAA
```
#### SAMPLE OUTPUT 2
```
3
```
#### EXPLANATION 2
The longest string that can be formed between SHINCAHN and NOHARAA while maintaining the order is NHA.
#### SAMPLE INPUT 3
```
ABCDEF
FBDAMN
```
#### SAMPLE OUTPUT 3
```
2
```
#### EXPLANATION 3
BD is the longest child of the given strings.
 #### SOLUTION
```js
// Complete the commonChild function below.
function commonChild(s1, s2) {
    const firstString = s1.split('')
    const secondString = s2.split('')
    const memo = [...secondString, 0].fill(0)
    // const subsequences = [...secondString, ''].fill('')
    for (let i = 1; i <= firstString.length; i++) {
        let prev = 0
        // let prevSubsequences = ''
        for (let j = 1; j <= secondString.length; j++) {
            const temp = memo[j]
            // const tempSubsequence = subsequences[j]
            if (firstString[i-1] === secondString[j-1]) {
                memo[j] = prev + 1
                // subsequences[j] = prevSubsequences + firstString[i-1]
            } else if (memo[j-1] > memo[j]) {
                memo[j] = memo[j-1]
                // subsequences[j] = subsequences[j-1]
            }
            prev = temp
            // prevSubsequences = tempSubsequence
        }
    }
    // console.log(subsequences[secondString.length])
    return memo[secondString.length]
}
```
---

### Abbreviation

```js
// Complete the abbreviation function below.
function abbreviation(a, b) {
  /*let lettersA = a.toUpperCase()
  let lettersB = b.toUpperCase()
  let index = 0
  let indexA = 0
  let indexB = 0
  let isAbbreviation = true
  // TODO: Fix missing test cases
  while (index < a.length || index < b.length) {
    const letterA = a.charAt(index)
    if (letterA && letterA === letterA.toUpperCase()) {
        indexB = lettersB.indexOf(letterA)
        if (indexB > -1) {
            lettersB = lettersB.slice(indexB+1)
        } else {
            isAbbreviation = false
            break
        }
    }

    const letterB = b.charAt(index)
    if (letterB) {
        indexA = lettersA.indexOf(letterB)
        if (indexA > -1) {
            lettersA = lettersA.slice(indexA+1)
        } else {
            isAbbreviation = false
            break
        }
    }

    index++
  }
  return isAbbreviation ? 'YES' : 'NO'*/

    const firstString = a.split('')
    const secondString = b.split('')
    
    let memo = new Array(firstString.length + 1)
    memo[0] = new Array(secondString.length + 1)
    memo[0][0] = true;
    for (let i = 1; i <= a.length; i++) {
        memo[i] = new Array(secondString.length + 1)
        memo[i][0] = a[i-1] !== a[i-1].toUpperCase()
    }
    for (let i = 1; i <= a.length; i++) {
        const rowPrev = i - 1
        for (let j = 1; j <= b.length; j++) {
            const colPrev = j - 1
            if (a[rowPrev] === b[colPrev]) {
                memo[i][j] = memo[rowPrev][colPrev]
            } else if (a[rowPrev].toUpperCase() === b[colPrev]) {
                memo[i][j] = memo[rowPrev][colPrev] || memo[rowPrev][j]
            } else if (a[rowPrev] === a[rowPrev].toUpperCase()) {
                memo[i][j] = false
            } else {
                memo[i][j] = memo[rowPrev][j]
            }
        }
    }
    return memo[firstString.length][secondString.length] ? 'YES' : 'NO'
}

```
