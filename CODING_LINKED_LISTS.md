## Linked Lists
---
### [Reverse a Doubly Linked List](https://www.hackerrank.com/challenges/reverse-a-doubly-linked-list/problem)
You’re given the pointer to the head node of a doubly linked list. Reverse the order of the nodes in the list. The head node might be NULL to indicate that the list is empty. Change the *next* and *prev* pointers of all the nodes so that the direction of the list is reversed. Return a reference to the head node of the reversed list.
#### Function Description
Complete the *reverse* function in the editor below. It should return a reference to the head of your reversed list.
reverse has the following parameter(s):
- *head*: : a reference to the head of a DoublyLinkedList
#### INPUT FORMAT
The first line contains an integer *t*, the number of test cases.
Each test case is of the following format:
- The first line contains an integer *n*, the number of elements in the linked list.
- The next *n* lines contain an integer each denoting an element of the linked list.
#### CONSTRAINTS
- 1 <= *t* <= 10
- 0 <= *n* <= 1000
- 0 <= *doublyLinkedListNode.data* <= 1000
#### OUTPUT FORMAT
Return a reference to the head of your reversed list. The provided code will print the reverse array as a one line of space-separated integers for each test case.
#### SAMPLE INPUT
```

1
4
1
2
3
4
```
#### SAMPLE OUTPUT
```
4 3 2 1
```
#### EXPLANATION
The initial doubly linked list is: 
1 ↔ 2 ↔ 3 ↔ 4 → *NULL*
The reversed doubly linked list is: 
4 ↔ 3 ↔ 2 ↔ 1 → *NULL*
#### SOLUTION
```js
// Complete the reverse function below.

/*
 * For your reference:
 *
 * DoublyLinkedListNode {
 *     int data;
 *     DoublyLinkedListNode next;
 *     DoublyLinkedListNode prev;
 * }
 *
 */
function reverse(head) {
    if (!head) return null
    let node = head
    let prev = null
    do {
        const next = node.next
        node.next = prev
        node.prev = next

        prev = node
        node = next
    } while (node != null)
    head = prev
    return head
}
```

---

### [Find Merge Point of Two List](https://www.hackerrank.com/challenges/find-the-merge-point-of-two-joined-linked-lists/problem)
Given pointers to the head nodes of 2 linked lists that merge together at some point, find the Node where the two lists merge. It is guaranteed that the two head Nodes will be different, and neither will be NULL.
In the diagram below, the two lists converge at Node *x*
```
[List #1] a--->b--->c
                     \
                      x--->y--->z--->NULL
                     /
     [List #2] p--->q
```
Complete the int findMergeNode(SinglyLinkedListNode* head1, SinglyLinkedListNode* head2) method so that it finds and returns the data value of the Node where the two lists merge.
#### INPUT FORMAT
Does not read any input from stdin/console. The findMergeNode(SinglyLinkedListNode,SinglyLinkedListNode) method has two parameters, ***head*1** and ***head*2**, which are the non-null head Nodes of two separate linked lists that are guaranteed to converge.
#### CONSTRAINTS
The lists will merge.
*head*1 and *head*2 ≠ *null* 
*head*1 ≠ *head*2
#### OUTPUT FORMAT
Does not write any output to stdout/console.
Each Node has a data field containing an integer. Return the integer data for the Node where the two lists merge.
#### SAMPLE INPUT
The diagrams below are graphical representations of the lists that input Nodes *headA*and *headB* are connected to.
#### TEST CASE 0
```
 1
  \
   2--->3--->NULL
  /
 1
```
#### TEST CASE 1
```
1--->2
      \
       3--->Null
      /
     1
```
#### SAMPLE OUTPUT
```
2
3
```
#### EXPLANATION
*Test Case 0*: As demonstrated in the diagram above, the merge Node's data field contains the integer 2.

*Test Case 1*: As demonstrated in the diagram above, the merge Node's data field contains the integer 3.

#### SOLUTION
```js
/*
    Find merge point of two linked lists
    Note that the head may be 'null' for the empty list.
    Node is defined as
    var Node = function(data) {
        this.data = data;
        this.next = null;
    }
*/

// This is a "method-only" submission.
// You only need to complete this method.

function findMergeNode(headA, headB) {
    let nodeA = headA
    let mergeNode = null
    while (nodeA && !mergeNode) {
        let nodeB = headB
        while (nodeA && nodeB) {
            if (nodeA == nodeB) {
                mergeNode = nodeA
                break
            }
            nodeB = nodeB.next
        }
        nodeA = nodeA.next
    }
    return mergeNode && mergeNode.data
}
```

---

### Inserting a Node Into a Sorted Doubly Linked List
Given a reference to the head of a doubly-linked list and an integer, *data*, create a new *DoublyLinkedListNode* object having data value *data* and insert it into a sorted linked list while maintaining the sort.
#### FUNCTION DESCRIPTION
Complete the sortedInsert function in the editor below. It must return a reference to the head of your modified DoublyLinkedList.
sortedInsert has two parameters:
1. *head*: A reference to the head of a doubly-linked list of *DoublyLinkedListNode* onjets
2. *data*: An integer denoting the value of the *data* field for the *DoublyLinkedListNode* you must insert into the list.
**Note**: Recall that an empty list (i.e., where ***head = null***) and a list with one element *are sorted lists*.
#### INPUT FORMAT
The first line contains an integer *t*, the number of test cases. 
Each of the test case is in the following format:
- The first line contains an integer *n*, the number of elements in the linked list.
- Each of the next *n* lines contains an integer, the *data* for each node of the linked list.
- The last line contains an integer *data* which needs to be inserted into the sorted doubly-linked list.
#### CONSTRAINTS
- 1 <= *t* <= 10
- 1 <= *n* <= 1000
- 1 <= *doublyLinkedListNode.data* <= 1000
#### OUTPUT FORMAT
**Do not print anything to stdout.** Your method must return a reference to the ***head*** of the same list that was passed to it as a parameter.
The ouput is handled by the code already written in the editor and is as follows:
For each test case, print the elements of the sorted doubly-linked list separated by spaces on a new line.
#### SAMPLE INPUT
```
1
4
1
3
4
10
5
```
#### SAMPLE OUTPUT
```
1
3
4
5
10
```
#### EXPLANATION
The initial doubly linked list is: 
1 ↔ 3 ↔ 4 ↔ |0 → *NULL*
The doubly linked list after insertion is: 
1 ↔ 3 ↔ 4 ↔ 5 ↔ 10 → *NULL*
#### SOLUTION
```js
// Complete the sortedInsert function below.

/*
 * For your reference:
 *
 * DoublyLinkedListNode {
 *     int data;
 *     DoublyLinkedListNode next;
 *     DoublyLinkedListNode prev;
 * }
 *
 */
function sortedInsert(head, data) {
    let node = head
    while (node) {
        if (data < node.data && (!node.prev || data >= node.prev.data)) {
            const currentNode = new DoublyLinkedListNode(data)
            currentNode.prev = node.prev
            currentNode.next = node

            if (node.prev) node.prev.next = currentNode
            node.prev = currentNode
            if (head.data == node.data) head = currentNode
            break
        }
        if (data > node.data && (!node.next || data <= node.next.data)) {
            const currentNode = new DoublyLinkedListNode(data)
            currentNode.prev = node
            currentNode.next = node.next
            if (node.next) node.next.prev = currentNode
            node.next = currentNode
            break
        }
        node = node.next
    }
    return head
}
```

---

### Insert at a Specific Position
This question is part of a tutorial track by MyCodeSchool https://www.youtube.com/user/mycodeschool  and is accompanied by a video lesson found here https://www.youtube.com/watch?v=Y0n86K43GO4 
You’re given the pointer to the head node of a linked list, an integer to add to the list and the position at which the integer must be inserted. Create a new node with the given integer, insert this node at the desired position and return the head node.
A position of 0 indicates head, a position of 1 indicates one node away from the head and so on. The head pointer given may be null meaning that the initial list is empty.
As an example, if your list starts as 1 → 2 → 3 and you want to insert a node at position 2with *data* = 4, your new list should be 1 → 2 → 4 → 3
#### FUNCTION DESCRIPTION
Complete the function *insertNodeAtPosition* in the editor below. It must return a reference to the head node of your finished list.
insertNodeAtPosition has the following parameters:
- *head*:: a SinglyLinkedListNode pointer to the head of the list
- *data*:: an integer value to insert as data in your new node
- *position*:: an integer position to insert the new node, zero based indexing
#### INPUT FORMAT
The first line contains an integer *n*, the number of elements in the linked list.
Each of the next *n* lines contains an integer SinglyLinkedListNode[i].data representing each node in the list.
The next line contains an integer *data* denoting the data of the node that is to be inserted.
The last line contains an integer *position*
#### CONSTRAINTS
- 1 <= *n* <= 1000
- 1 <= *SinglyLinkedListNode[i].data* <= 1000, where SinglyLinkedListNode[i] is the *i*^th element of the linked list.
- 1 <= *position* <= *n*
#### OUTPUT FORMAT
Return a reference to the list head. Existing code prints the list for you.
#### SAMPLE INPUT
```
3
16
13
7
1
2
```
#### SAMPLE OUTPUT
```
16 13 1 7
```
#### EXPLANATION
The initial linked list is  16 13 7. We have to insert 1 at the position 2 which currently has 7 in it. The updated linked list will be 16 13 1 7.
#### SOLUTION
```js
// Complete the insertNodeAtPosition function below.

/*
 * For your reference:
 *
 * SinglyLinkedListNode {
 *     int data;
 *     SinglyLinkedListNode next;
 * }
 *
 */
function insertNodeAtPosition(head, data, position) {
    const newNode = new SinglyLinkedListNode(data)
    if (!head) return newNode
    let node = head
    let prevNode = null
    let counter = 0
    while (node) {
        if (counter == position || !node.next) {
            newNode.next = node
            if (prevNode) prevNode.next = newNode
            if (head == node) head = currentNode
            break
        }
        prevNode = node
        node = node.next
        counter++
    }
    return head
}
```

