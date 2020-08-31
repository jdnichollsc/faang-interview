## Facebook Coding Interview Prep
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
