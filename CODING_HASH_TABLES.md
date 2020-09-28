
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

### 
```js

```

--- 

### Maximum Number of Toys to Buy
```js

```

---

### Maximum Number of Toys to Buy
```js

```

---

### Maximum Number of Toys to Buy
```js

```

---
