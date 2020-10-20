## Coding Interview Prep
---
### Maximum Number of Toys to Buy
A parent goes to the store to buy toys for their child. The parent has only a certain amount to spend, and they want to maximize the number of toys they buy with their money.
Given a list of prices and an amount to spend, what is the maximum number of toys the parent can buy? For example, if **prices** = [**1,2,3,4**] and parent has ***k*** = **7**
to spend, they can buy items [**1,2,3**] for 6, or [**3,4**] for 7 units of currency. They would choose the first group of 3 items.
#### Function Description
Complete the function *maximumToys* in the editor below. It should return an integer representing the maximum number of toys the parent can purchase.
maximumToys has the following parameter(s):
- *prices*: an array of integers representing toy prices
-*k*: an integer, the parent's budget
#### Input Format
The first line contains two integers, *n* and *k*, the number of priced toys and the amount the parent has to spend.
The next line contains *n* space-separated integers *prices[i]*.
#### Constraints
- *n* >= 1 
- *k* >= 1 
- prices[i] >= 1 
A toy can't be bought multiple times.
#### Output Format
The maximum number of toys the parent can buy.
#### Sample Input
```
7 50
1 12 5 111 200 1000 10
```
#### Sample Output
`4`
#### Explanation
They can buy only 4 toys at most. These toys have the prices 1, 12, 5, 10.
#### SOLUTION
```js
// Complete the maximumToys function below.
function maximumToys(prices, k) {
    const sortedPrices = prices.sort((a, b) => a-b)
    let totalPrice = 0
    let i
    for (i = 0; i < sortedPrices.length; i++) {
        const price = sortedPrices[i]
        if (price + totalPrice < k) {
            totalPrice += price
        } else {
            break
        }
    }
    return i
}
```

---

### Fraudulent Activity Notifications
HackerLand National Bank has a simple policy for warning clients about possible fraudulent account activity. If the amount spent by a client on a particular day is *greater than or equal to* **2** x the client's median spending for a trailing number of days, they send the client a notification about potential fraud. The bank doesn't send the client any notifications until they have at least that trailing number of prior days' transaction data.
Given the number of trailing days ***d*** and a client's total daily expenditures for a period of ***n*** days, find and print the number of times the client will receive a notification over all  ***n*** days. 
For example, ***d*** = ***3***, and ***expenditures*** = ***[10, 20, 30, 40, 50]***. On the first three days, they just collect spending data. At day **4**, we have trailing expenditures of  **[10, 20, 30]**. The median is 20 and the day's expenditure is 40. Because **40** >= **2** x **20**, there will be a notice. The next day, our trailing expenditures are **[20, 30, 40]** and the expenditures are 50. This is less than **2** x **30** so no notice will be sent. Over the period, there was one notice sent..
**Note**: The median of a list of numbers can be found by arranging all the numbers from smallest to greatest. If there is an odd number of numbers, the middle one is picked. If there is an even number of numbers, median is then defined to be the average of the two middle values. 
#### Function Description
Complete the function *activityNotifications* in the editor below. It must return an integer representing the number of client notifications.
activityNotifications has the following parameter(s):
- *expenditure*: an array of integers representing daily expenditures
- *d*: an integer, the lookback days for median expending.
#### INPUT FORMAT
The first line contains two space-separated integers *n* and *d*, the number of days of transaction data, and the number of trailing days' data used to calculate median spending.
The second line contains *n* space-separated non-negative integers where each integer *i* denotes *expenditure[i]*.
#### Constraints
- 1 <= *n* <= 2x10^5
- 1 <= *d* <= *n*
- 0 <= *expenditure[i]* <= 200
#### Output Format
Print an integer denoting the total number of times the client receives a notification over a period of *n* days.
#### Sample Input 0
```
9 5
2 3 4 2 3 6 8 4 5
```
#### Sample Output 0
`2`
#### Explanation 0
We must determine the total number of *notifications* the client receives over a period of ***n*** = ***9*** days. For the first five days, the customer receives no notifications because the bank has insufficient transaction data:  *notifications* = *0*.
On the sixth day, the bank has ***d*** = ***5*** days of prior transaction data, **{2,3,4,2,3}** and ***median*** = **3** dollars. The client spends **6** dollars, which triggers a notification because **6** >= **2** x *median*: *notifications* = 0 + 1 = 1.
On the seventh day, the bank has *d* = **5** days of prior transaction data, **{4,2,3,6,8}** and *median* = **4** dollars. The client spends **4** dollars wich does not trigger 
anotification becouse **4** < **2** x *median*: *notifications* = 2.
On the ninth day, the bank has ***d*** = ***5*** days of prior transaction data, **{2,3,6,8,4}**, and a transaction median of  **4** dollars. The client spends  **5** dollars, which does not trigger a notification because **5** < **2** x *median*: *notifications* = 2.
#### Sample Input 1
```
5 4
1 2 3 4 4
```
#### Sample Output 1
`0`
#### Explanation 1
There are **4** days of data required so the first day a notice might go out is day **5**. Our trailing expenditures are **{1,2,3,4}** with a median of 2.5 The client spends  **4** which is less than **2** x **2.5** so no notification is sent.
#### SOLUTION 
```js
// Complete the activityNotifications function below.
function activityNotifications(expenditure, d) {
    // Number of notifications
    let n = 0

    // Set midpoints for median calculation
    let [ i1, i2 ] = [ Math.floor((d-1)/2), Math.ceil((d-1)/2) ]
    let m1, m2, m

    // Initialize count sorted subarray
    let cs = new Array(201).fill(0)
    for (let i = d-1; i >= 0; i--) cs[expenditure[i]]++

    // Iterate through expenditures
    for (let i = d, l = expenditure.length; i < l; i++) {

        // Find median
        for (let j = 0, k = 0; k <= i1; k += cs[j], j++) m1 = j
        for (let j = 0, k = 0; k <= i2; k += cs[j], j++) m2 = j
        let m = (m1 + m2) / 2

        // Check if notification is given
        if (expenditure[i] >= m * 2) n++

        // Replace subarray elements
        cs[expenditure[i-d]]--
        cs[expenditure[i]]++
    }

    return n
}

```

---

### Counting Inversions
https://www.hackerrank.com/challenges/ctci-merge-sort/problem

---
