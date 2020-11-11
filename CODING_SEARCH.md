## Search
---
### [Minimum Time Required](https://www.hackerrank.com/challenges/minimum-time-required/problem)

You are planning production for an order. You have a number of machines that each have a fixed number of days to produce an item. Given that all the machines operate simultaneously, determine the minimum number of days to produce the required order.
For example, you have to produce *goal* 10 items. You have three machines that take *machines* [2, 3, 2] days to produce an item. The following is a schedule of items produced:
```
Day Production  Count
2   2               2
3   1               3
4   2               5
6   3               8
8   2              10
```
It takes 8 days to produce 10 items using these machines.
#### Function Description
Complete the *minimumTime* function in the editor below. It should return an integer representing the minimum number of days required to complete the order.
minimumTime has the following parameter(s):
- *machines*: an array of integers representing days to produce one item per machine
- *goal*: an integer, the number of items required to complete the order
#### Input Format
The first line consist of two integers *n* and *goal*, the size of *machines* and the target production.
The next line contains *n* space-separated integers, *machines [i].
#### Constraints
- 1 <= *n* <= 10^5
- 1 <= *goal* <= 10^9
- 1 <= *machines[i]* <= 10^9
#### Output Format
Return the minimum time required to produce *goal*  items considering all machines work simultaneously.
#### Sample Input 0
```
2 5
2 3
```
#### Sample Output 0
`6`
#### Explanation 0
In 6 days *machine 0* can produce 3 items and *machine 1* can produce 2 items. This totals up to 5.
#### Sample Input 1
```
3 10
1 3 4
```
#### Sample Output 1
`7`
#### Explanation 1
In 7 minutes *machine 0* can produce 7 items, *machine 1* can produce 2 items and *machine 2* can produce 1 item. Which totals up to 10.
#### Sample Input 2
```
3 12
4 5 6
```
#### Sample Output 2
`20`
#### Explanation 2
In 20 daya *machine 0* can produce 5 items, *machine 1* can produce 4 and *machine 2* can produce 3. 
#### SOLUTION
- Brute force
```js
// Complete the minTime function below.
function minTime(machines, goal) {
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
    return currentDay
}
```
- Optimal solution
```js
// Complete the minTime function below.
function minTime(machines, goal) {
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

### [Making candies](https://www.hackerrank.com/challenges/making-candies/problem)

You're playing a game called *CandyMaker*, where the goal is to make candies.
You just started a level in which you must accumulate *n* candies starting with *m* machines and *w* workers. In a single *pass*, you can make *m x w* candies. After each pass, you can decide whether to spend some of your candies to buy more machines or hire more workers. Buying a machine or hiring a worker costs *p* units, and there is no limit to the number of machines you can own or workers you can employ.

You want to minimize the number of passes to obtain the required number of candies at the end of a day. Determine that number of passes.

For example, you start with *m* = 1 machine and *w* = 2 workers. The cost to purchase or hire, *p* = 1 and you need to accumulate 60 candies. You execute the following strategy:
1. Make *m x w* = 1 x 2 = 2 candies. Purchase two machines.
2. Make 3 x 2 = 6 candies. Purchase 3 machines and hire 3  workers
3. Make 6 x 5 = 30 candies. Retain all 30 candies.
4. Make 6 x 5 = 30 candies. With yesterday's production, you have 60 candies.
It took 4 passes to make enough candies.
#### Function Description
Complete the *minimumPasses* function in the editor below. The function must return a long integer representing the minimum number of passes required.
minimumTime has the followminimumPasses has the following parameter(s):ing parameter(s):
- *m*: long integer, the starting number of machines.
- *w*: long integer, the starting number of workers.
- *p*: long integer, the cost of a new hire or a new machine
- *n*: long integer, the number of candies to produce.
#### Input Format
A single line consisting of four space-separated integers describing the values of *m, w, p* and *n*, the starting number of machines and workers, the cost of a new machine or a new hire, and the the number of candies you must accumulate to complete the level.
#### Constraints
- 1 <= *m, w, p, n* <= 10^12
#### Output Format
Return a long integer denoting the minimum number of passes required to accumulate at least *n* candies.
#### Sample Input
```
3 1 2 12
```
#### Sample Output
`3`
#### Explanation
You make three passes:
1. In the first pass, you make *m x w* = 3 x 1 = 3 candies. You then spend *p = 2* of them hiring another worker, so *w = 2* and you have one candy left over.
2. In the second pass, you make 3 x 2 = 6 candies. You then spend *2 * p* = 4 of them on another machine and another worker, so *w = 3* and *m = 4* and you has 3 candies left over.
3. In the third pass, you make 4 x 3 = 12 candies. Because this satisfies your goal of making at least *n = 12* candies, we print the number of passes (i.e., 3) as our answer.
#### SOLUTION
---
```js
// Complete the minimumPasses function below.
const getStepsRequired = (total) => (quantity) => Math.ceil(total / quantity)

function minimumPasses(machines, workers, price, goal) {
    let accumulated = 0
    let invest = 0
    let spend = Infinity
    while (accumulated < goal) {
        const capability = machines * workers
        let steps = getStepsRequired(price - accumulated)(capability)
        if (steps < 1) {
            const upgrade = Math.floor(accumulated / price)
            if (machines > workers + upgrade) {
                workers += upgrade
            } else if (workers > machines + upgrade) {
                machines += upgrade
            } else {
                const total = machines + workers + upgrade
                machines = Math.floor(total/2)
                workers = total - machines
            }
            // Save the remaining money
            accumulated = accumulated % price
            steps = 1
        }
        const newCapability = machines * workers
        accumulated += steps * newCapability
        invest += steps
        const remaining = goal - accumulated
        const increment = getStepsRequired(remaining)(newCapability)
        spend = Math.min(spend, invest + increment)
    }
    return Math.min(invest, spend)
}
```
