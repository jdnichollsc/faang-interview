
### Minimum Time Required
```js
// Complete the minTime function below.
function minTime(machines, goal) {
    /* BRUTE FORCE
    const dayMachines = {}
    for (let i = 0; i < machines.length; i++) {
        const day = dayMachines[machines[i]]
        if (day) {
            day.push(i)
        } else {
            dayMachines[machines[i]] = [i]
        }
    }
    const daysToRun = Object.keys(dayMachines).sort((a, b) => Number(a)-Number(b))
    const minDay = daysToRun[0]
    let currentDay = minDay - 1
    let items = 0
    while (items < goal) {
        currentDay++
        for (let i = 0; i < daysToRun.length; i++) {
            if (daysToRun[i] > currentDay) break
            if (currentDay % daysToRun[i] === 0) {
                items += dayMachines[daysToRun[i]].length
                if (items >= goal) break
            }
        }
    }
    return currentDay*/

    const sorted = machines.sort((a, b) => a-b)
    let low = 1
    let high = goal * sorted[sorted.length - 1]
    // Binary search
    while (low < high) {
        const mid = Math.floor(low + (high-low)/2)
        if (findItems(sorted, goal, mid)) {
            high = mid
        } else {
            low = mid + 1
        }
    }
    return high
}

function findItems(machines, goal, time) {
    let items = 0
    for (let i = 0; i < machines.length; i++) {
        items += Math.floor(time/machines[i])
        if (items >= goal) break
    }
    return items >= goal
}
```

---

### Making candies
https://www.hackerrank.com/challenges/making-candies/problem

---
