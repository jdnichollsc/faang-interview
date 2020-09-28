
### Reverse a Doubly Linked List
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

### Find Merge Point of Two List
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

