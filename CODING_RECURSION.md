## Coding Interview Prep
---
### Fibonacci Numbers
*The Fibonacci Sequence*
The Fibonacci sequence appears in nature all around us, in the arrangement of seeds in a sunflower and the spiral of a seashell for example.
The Fibonacci sequence begins with *fibonacci(0) = 0* and *fibonacci(1) = 1* as its first and second terms. After these first two elements, each subsequent element is equal to the sum of the previous two elements.
Programmatically:
- *fibonacci(0) = 0*
- *fibonacci(1) = 1*
- *fibonacci(n) = fibonacci(n-1) + fibonacci(n-2)*
Given *n*, return the *n*^th number in the sequence.
As an example, *n* = 5. The Fibonacci sequence to 6 is ***fs*** = [**0, 1, 1, 2, 3, 5, 8**]. With zero-based indexing, ***fs[5]*** = **5**.
#### FUNCTION DESCRIPTION
Complete the recursive function *fibonacci* in the editor below. It must return the *n*^th element in the Fibonacci sequence.
fibonacci has the following parameter(s):
- *n*: the integer index of the sequence to return
#### INPUT FORMAT
The input line contains a single integer, *n*.
#### CONSTRAINTS
- 0 <= *n* <= 30
#### OUTPUT FORMAT
Existing stub code in the editor prints the integer value returned by the *fibonacci* function.
#### SAMPLE INPUT
```
3
```
#### SAMPLE OUTPUT
```
2
```
#### EXPLANATION
The Fibonacci sequence begins as follows:
*fibonacci(0)* = 0
*fibonacci(1)* = 1
*fibonacci(2)* = (0 + 1) = 1
*fibonacci(3)* = (1 + 1) = 2
*fibonacci(4)* = (1 + 2) = 3
*fibonacci(5)* = (2 + 3) = 5
*fibonacci(6)* = (3 + 5) = 8
...
We want to know the value of *fibonacci(3)*. In the sequence above, *fibonacci(3)* evaluates to 2.
#### SOLUTION
```python
def fibonacci(n):
    if (n == 0 or n == 1): return n
    return fibonacci(n-1) + fibonacci(n-2)
```

---

### Recursive Digit Sum
 We define the super digit of an integer *x* using the following rules:
 Given an integer, we need to find the *super digit* of the integer
 . If *x* has only 1 digit, then its super digit is *x*
 - Otherwise, the super digit of *x* is equal to the super digit of the sum of the digits of *x*
 For example, the super digit of 9875 will be calculated as:
 ```
 super_digit(9875)   9+8+7+5 = 29
 super_digit(29)     2+9 = 11
 super_digit(11)     1+1 = 2
 super_digit(2)      = 2
 ```
 You are given two numbers *n*and *k*. The number *p* is created by concatenating the string *n k* times. Continuing the above example where *n = 9875*, assume your value *k = 4*. Your initial *p = 9875 9875 9875 9875 (spaces added for clarity).
 ```
 superDigit(p) = superDigit(9875987598759875) 
                 5+7+8+9+5+7+8+9+5+7+8+9+5+7+8+9 = 116
 superDigit(p) = superDigit(116)
                 1+1+6 = 8
 superDigit(p) = superDigit(8)
 ```
 All of the digits of *p* sum to 116. The digits of 116 sum to 8, 8 is only one digit, so it's the super digit.
 #### FUNCTION DESCRIPTION
 Complete the function *superDigit*  in the editor below. It must return the calculated super digit as an integer.
 superDigit has the following parameter(s):
 - *n*: a string representation of an integer
 - *k*: an integer, the times to concatenate *n* to make *p*
 #### INPUT FORMAT
 The first line contains two space separated integers, *n* and *k*
 #### CONSTRAINTS
- 1 <= *n* <= 10^100000
- 1 <= *K* <= 10^5
#### OUTPUT FORMAT
Return the super digit of *p*, where *p* is created as described above.
#### SAMPLE INPUT 0
```
148 3
```
#### SAMPLE OUTPUT 0
```
3
```
#### EXPLANATION 0
Here *n* = 148 and *k* = 3, so *P* = 148148148
```
super_digit(P) = super_digit(148148148) 
               = super_digit(1+4+8+1+4+8+1+4+8)
               = super_digit(39)
               = super_digit(3+9)
               = super_digit(12)
               = super_digit(1+2)
               = super_digit(3)
               = 3
```
#### SAMPLE INPUT 1
```
123 3
```
#### SAMPLE OUTPUT 1
```
9
```
#### EXPLANATION 1
Here *n* = 123 and *k* = 3, so *P* = 123123123
```
super_digit(P) = super_digit(123123123) 
               = super_digit(1+2+3+1+2+3+1+2+3)
               = super_digit(18)
               = super_digit(1+8)
               = super_digit(9)
               = 9
```
#### SOLUTION
```js
// Complete the digitSum function below.
function superDigit(n, k) {
    if (n.length < 2) return n
    const digit = (n.split('').reduce((res, d) => res + Number(d), 0) * k) + ''
    return superDigit(digit, 1)
}
```

---

### Crossword Puzzle
A 10x10 Crossword grid is provided to you, along with a set of names of places which need to be filled into the grid. Cells are marked either + or -. Cells marked with a - are to be filled with the word list.
The following shows an example crossword from the input *crossword* grid and the list of words to fit, *words* = [*POLAND, LHASA, SPAIN, INDIA*]:
```
Input           Output

++++++++++      ++++++++++
+------+++      +POLAND+++
+++-++++++      +++H++++++
+++-++++++      +++A++++++
+++-----++      +++SPAIN++
+++-++-+++      +++A++N+++
++++++-+++      ++++++D+++
++++++-+++      ++++++I+++
++++++-+++      ++++++A+++
++++++++++      ++++++++++

POLAND; LHASA; SPAIN; INDIA
```
#### FUNCTION DESCRIPTION
Complete the *crosswordPuzzle* function in the editor below. It should return an array of strings, each representing a row of the finished puzzle.
crosswordPuzzle has the following parameter(s):
- *crossword*: an array of 10 strings of length 10 representing the empty grid
- *words* a string consisting of semicolon delimited strings to fit into *crossword*
#### INPUT FORMAT
Each of the first 10 lines represents *crossword[i]*, each of which has 10 characters, *crossword[i][j]*.
The last line contains a string consisting of semicolon delimited *words[i]* to fit.
#### CONSTRAINTS
- 1 <= |*words*| <= 10
*crossword[i][j]* ϵ {+,-}
*words[i][j]* ϵ *ascii[A-Z]*
#### OUTPUT FORMAT
Position the words appropriately in the 10x10 grid, then return your array of strings for printing.
#### SAMPLE INPUT 0
```
+-++++++++
+-++++++++
+-++++++++
+-----++++
+-+++-++++
+-+++-++++
+++++-++++
++------++
+++++-++++
+++++-++++

LONDON; DEHLI; ICELAND; ANKARA
```
#### SAMPLE OUTPUT 0
```
+L++++++++
+O++++++++
+N++++++++
+DHELI++++
+O+++C++++
+N+++E++++
+++++L++++
++ANKARA++
+++++N++++
+++++D++++
```
#### SAMPLE INPUT 0
```
+-++++++++
+-++++++++
+-------++
+-++++++++
+-++++++++
+------+++
+-+++-++++
+++++-++++
+++++-++++
++++++++++

AGRA; NORWAY; ENGLAND; GWALIOR
```
#### SAMPLE OUTPUT 0
```
+E++++++++
+N++++++++
+GWALIOR++
+L++++++++
+A++++++++
+NORWAY+++
+D+++G++++
+++++R++++
+++++A++++
++++++++++
```
#### SOLUTION
```js
function crosswordPuzzle(crossword, hints) {
    const blankWords = findBlankWords(crossword)
    const combinations = getArrayMutations(hints.split(';'))

    for (let i = 0; i < combinations.length; i++) {
        const combination = combinations[i]
        const result = solvePuzzle(crossword, blankWords, combination)
        if (result) return result
    }
    return []
}

const getKey = (i, j) => `${i}_${j}`

function findBlankWords (crossword) {
    const words = []
    const visited = {}
    for (let i = 0; i < crossword.length; i++) {
        const row = crossword[i]
        for (let j = 0; j < row.length; j++) {
            const char = row[j]
            const key = getKey(i, j)
            if (char !== '-') continue
            // DOWN
            if (crossword[i+1] && crossword[i+1][j] === '-' && !visited['DOWN_' + key]) {
                const word = []
                for (let c = i; c < crossword.length; c++) {
                    if (crossword[c][j] !== '-') break
                    const cKey = getKey(c, j)
                    visited['DOWN_' + cKey] = true
                    word.push(cKey)
                }
                words.push(word)
            }
            // RIGHT
            if (row[j+1] === '-' && !visited['RIGHT_' + key]) {
                const word = []
                for (let c = j; c < row.length; c++) {
                    if (row[c] !== '-') break
                    const cKey = getKey(i, c)
                    visited['RIGHT_' + cKey] = true
                    word.push(cKey)
                }
                words.push(word)
            }
        }
    }
    return words
}

function solvePuzzle (crossword, blankWords, words) {
    const mapLetters = {}
    for (let i = 0; i < words.length; i++) {
        const letters = words[i].split('')
        const blankWord = blankWords[i]
        if (letters.length !== blankWord.length) return null
        for (let j = 0; j < letters.length; j++) {
            const letter = letters[j]
            const key = blankWord[j]
            if (!mapLetters[key]) {
                mapLetters[key] = letter
                continue
            }
            if (mapLetters[key] !== letter) return null
        }
    }
    const solved = []
    for (let i = 0; i < crossword.length; i++) {
        solved[i] = crossword[i].split('')
        for (let j = 0; j < crossword[i].length; j++) {
            const key = getKey(i, j)
            if (mapLetters[key]) {
                solved[i][j] = mapLetters[key]
            }
        }
        solved[i] = solved[i].join('')
    }
    return solved
}
// https://stackoverflow.com/a/60136724/1532821
function getArrayMutations(arr, perms = [], len = arr.length) {
  if (len === 1) perms.push(arr.slice(0))

  for (let i = 0; i < len; i++) {
    getArrayMutations(arr, perms, len - 1)

    len % 2 // parity dependent adjacent elements swap
      ? [arr[0], arr[len - 1]] = [arr[len - 1], arr[0]]
      : [arr[i], arr[len - 1]] = [arr[len - 1], arr[i]]
  }

  return perms
}
```

---

### Ways to Climb a Staircase
https://www.hackerrank.com/challenges/ctci-recursive-staircase/problem

### [Minimum Steps To One](https://leetcode.com/discuss/interview-question/538568/google-onsite-min-operations-to-reduce-number-to-1)
Given an integer as an input, *num*, return the *fewest* operations, or steps, needed to arrive at **1**, when you can only perform **3** operations:

- **Divide by 3**, if *num* is divisible by 3
- **Divide by 2**, if *num* is divisible by 2
- **Subtract 1**

**For example:** given an input of **5**, there are many paths to arrive at **1**. You can **subtract 1 five times** to arrive at **1**. But that isn't the shortest path. The largest step you can take first is to **subtract 1**, which gets you to **4**. Then you can **divide by 2**, which gets you to **2**. Finally, you **subtract 1**, which gets you to **1**. So in total, we performed **3** operations: **5 => 4 => 2 => 1**

Your goal is to return the minimum number of operations from the input integer to 1.

If *num* is 1, then return 0, since you don't need to perform any operations to arrive at 1.
