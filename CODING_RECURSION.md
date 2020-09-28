
### Fibonacci Numbers
```
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
```
