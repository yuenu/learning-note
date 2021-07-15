# Doubly Link

![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Doubly-linked-list.svg/610px-Doubly-linked-list.svg.png)

## setting up node class

```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
    this.prev = null;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
}
```

## pushing pseudocde

- Create a new node with the value passed to the function
- If the head property is null set the head and tail to be the newly created node
- If not, set the next property on the tail to be that node
- Set the previous property on the newly created node to be the tail
- Set the tail to be the newly created node

```js
push(val) {
  let newNode = new Node(val); // val
  if(this.length === 0) {
    this.head = newNode
    this.tail = newNode
  } else {
    this.tail.next = newNode;
    // 1 ⇔ 3 -> val
    //    tail
    newNode.prev = this.tail;
    // 1 ⇔ 3 ⇔ val
    //    tail
    this.tail = newNode
    // 1 ⇔ 3 ⇔ val
    //          tail
  }
  this.length++;
  return this;
}
```

## popping pseudocode

- If thee is no head, return undefined
- Store the current tail in a variable to return later
- If the length is 1, set the head and tail to be null
- Update the tail to be the previous Node.
- Set the newTail's next to null

```js
pop() {
  // 1 ⇔ 3 ⇔ 7
  if(!this.head) return undefined
  let poppedNode = this.tail; // 7
  if(this.length === 1) {
    this.head = null;
    this.tail = null;
  } else {
    // 1 ⇔ 3 ⇔ 7
    //         tail
    //          pop
    this.tail = poppedNode.prev ;
    // 1 ⇔ 3 ⇔ 7
    //    tail  pop
    this.tail.next = null;
    // 1 ⇔ 3 <- 7
    //    tail  pop
    poppedNode.prev = null;
  }
  this.length--;
  return poppedNode;
}
```

## Shifting pseudocode

- If length is 0, return undefined
- Store the current head property in a variable(we'll call it old head)
- If the length is one
  - set the head to be null
  - set the tail to be null
- Update the head to be the next of the old head
- Set the head's prev property to null

```js
shift() {
  if (this.length === 0) return undefined;
  // 99 ⇔ 100
  let oldHead = this.head;
  if(this.length === 1) {
    this.head = null;
    this.tail = null;
  } else {
    this.head = oldHead.next;
    this.head.prev = null;
    oldHead.next = null;
  }
  this.length--
  return oldHead
}
```

## Unshifting pseudocode

- Create a new node with the value passed to the function
- If the length is 0
  - Set the head to be the new node
  - Set the tail to be the new node
- Others
  - Set the prev property on the head of the list to be the new node
  - Set the next property on the new node to be the head property
  - Update the head to be the new node
- Increment the length
- Return the list

```js
unshift(val) {
  let newNode = new Node(val);
  if (this.length === 0) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    //  1  ⇔  2  ⇔  3
    // head         tail
    this.head.prev = newNode;
    // new  <- 1  ⇔  2  ⇔  3
    //       head          tail
    newNode.next = this.head;
    // new  ⇔  1  ⇔  2  ⇔  3
    //        head          tail
    this.head = newNode;
    // new  ⇔  1  ⇔  2  ⇔  3
    // head                 tail
  }
  this.length++
  return this
}
```

## Get pseudocode

- If the index is less than 0 or greater or equal to the length, return null
- If the index is less than or equal to half the length of the list
  - Loop through the list starting from the head and loop towards the middle
  - Return the node once it is found
- If the index is greater than half the length of the list
  - Loop through the list starting from the tail and loop towards the middle
  - Return the node once it is found

### Linear searching of signly linked

```js
get(index) {
  if(index < 0 || index >= this.length) return null;
  let count = 0;
  let current = this.head;
  while(count != index) {
    current = current.next
    count++
  }
  return current
}
```

### Find the middle one, and determine search from head or tail

```js
get(index) {
  if (index < 0 || index >= this.length) return null;
  let count, current
  if (index <= this.length / 2) {
    count = 0;
    current = this.head;
    while (count != index) {
      current = current.next;
      count++;
    }
    return current;
  } else {
    count = this.length - 1;
    current = this.tail;
    while (count !== index) {
      current = current.prev;
      count--;
    }
    return current;
  }
}
```

## Set pseudocode

- Create a variable which is the result of the **get** method at the index passed to the function
  - If the **get** method return s a valid node, set the value of that node to be the value passed to the function
  - Return true
- Otherwise, return false

```js
set(index, val) {
  let foundNode = this.get(index);
  if (foundNode !== null) {
    foundNode.val = val;
    return true;
  }
  return false;
}
```

## Insert pseudocode

- If the index is less than zero or greater than or equal to the length return false
- If the index is 0, unshift
- If the index is same as the length, push
- Use the **get** method to access the index - 1
- Set the next and prev properties on the correct nodes to link everything together

```js
insert(index, val) {
  if (index < 0 || index > this.length) return false;
  if (index === 0) return this.unshift(val);
  if (index === this.length) return this.push(val);
  let newNode = new Node(val);
  let beforeNode = this.get(index - 1);
  let afterNode = beforeNode.next;
  beforeNode.next = newNode;
  newNode.prev = beforeNode;
  newNode.next = afterNode;
  afterNode.prev = newNode;
  this.length++
  return true
}
```

## Remove pseudocode

- If the index is less than zreo or greater than or equal to the length return undefined
- If the index is 0, **shift**
- If the index is the same as the length - 1 , **pop**
- Use the **get** method to retrieve the item to bre removed
- Update the next and prec properties to remove the found node from the list
- Set next and prev to null on the found node
- Decreament the length
- Return the removed node

```js
remove(index) {
  if (index < 0 || index >= this.length) return undefined;
  if (index === 0) return this.shift();
  if (index === this.length - 1) return this.pop();
  let removedNode = this.get(index);
  let beforeNode = removedNode.prev
  let afterNode = removedNode.next
  beforeNode.next = afterNode;
  afterNode.prev = beforeNode;
  removedNode.next = null;
  removedNode.prev = null;
  this.length--;
  return removedNode;
}
```

---

## Conclusion

Big O

- insertion - O(1)
- Removal - O(1)
- Searching - O(N)
- Access - O(N)

Recap

- Doubly Linked Lists are almost identical to Singly Linked Lists except there is an additional pointer to previous nodes
- Better then Singly Linked Lists for finding nodes and can be done in half the time!
- However, they do take up more memory considering the extra pointer
