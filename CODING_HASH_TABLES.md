
### Encode Secret Message
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
