# Stack & Queues

## Stack

### Seting up the node first (Both of us can use)

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

## Stack

```js
class Stack {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
  push(val) {
    let newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      let temp = this.first;
      this.first = newNode;
      this.first.next = temp;
    }
    return ++this.size;
  }
  pop() {
    if (!this.first) return null;
    let temp = this.first;
    if (this.first === this.last) {
      this.last = null;
    }
    this.first = this.first.next;
    this.size--;
    return temp.value;
  }
}
```

### Recap

- Stacks are a **LIFO** data structure where the last value in is always the first one out.
- Stacks are used to handle function invocations(the call stack), foroperations like undo/redo, and for routing (remember pages you have visited and go back/forward) amdmuch more!
- They are not a bulit in data structure in Javascript,but are relatively simply to implement

## Queue

### Setting up our quere class

```js
class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
}
```

### Enqueue Pseudocode

- This function accepts some value
- Create a new node using that value passed to the function
- If there are no nodes in the queue, set this node to be the first and last property of the queue
- Otherwise, set the next property on the current last to be that node, and then set the last property of the queue to be that node
- Increament the size of the queue by 1

```js
enqueue(val) {
  let newNode = new Node(val);
  if (!this.first) {
    this.first = newNode;
    this.last = newNode;
  } else {
    this.last.next = newNode;
    this.last = newNode;
  }
  return ++this.size;
}
```

#### Dequeue pseudocde

- If there is no first property, just return null
- Store the first property in a variable
- See if the first is the same as the last (check if there is only 1 node). If so, set the first and last to be null
- If there is more than 1 node,set the first property to be the next property of first
- Decreament the size by 1

```js
dequeue() {
  if (!this.first) return null;
  let temp = this.first;
  if (this.first === this.last) {
    this.last = null;
  }
  this.first = this.first.next;
  this.size--;
  return temp.value;
}
```

### Recap

- Queues are a **FIFO** data structure, all elements are first in first out.
- Queues are usefult for processing tasks and are foundational for more complex data structures.
- Insertion and Removal can be done in O(1)
