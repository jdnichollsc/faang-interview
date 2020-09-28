
### Fibonacci Numbers
```python
def fibonacci(n):
    if (n == 0 or n == 1): return n
    return fibonacci(n-1) + fibonacci(n-2)
```

---

### Recursive Digit Sum
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

