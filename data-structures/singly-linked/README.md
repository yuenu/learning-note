# Singly Link

## Setting up the start up

```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class SignlyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
}
```

## Pushing pseudocode

- This function should accept a value
- Create a new node using the value passed to the function
- If there is no head property on the list, set the head and tail to be the newly created node
- Otherwise set the next property on tail to be the new node and set the tail property on the list to be the newly created node
- Increament the length by one

```js
push(val) {
  // 1 ->  2  -> 3
  let newNode = new Node(val);
  if (!this.head) {
    this.head = newNode;
    this.tail = this.head;
  } else {
    //   1 ->  2  -> 3
    // head         tail
    this.tail.next = newNode;
    //   1 ->  2  -> 3    -> val
    // head         tail    newNode
    this.tail = newNode;
    //   1 ->  2  -> 3    -> val
    // head                  tail
  }
  this.length++;
  return this;
}
```

## Popping pseudocode

- If there are no nodes in the list, return undefined
- Loop through the list until you reach the tail

```js
pop() {
  // 1 ->  2  -> 3
  if (!this.head) return undefined;
  let current = this.head;
  let newTail = current;
  while (current.next) {
    newTail = current;
    current = current.next;
  }
  //   1 ->     2    ->   3
  // head                tail
  //         newTail     curr

  this.tail = newTail;
  //   1 ->     2    ->   3
  // head     tail
  //         newTail     curr

  this.tail.next = null;
  //   1 ->     2      |    3
  // head     tail     |
  //         newTail   |   curr

  this.length--;
  if (this.length === 0) {
    this.head = null;
    this.tail = null;
  }
  return current;
}
```

## Shifting pseudocode

- If there are no nodes, return undefined
- Store the current head property in a variable
- Set the head peoperty to be the current head's next property
- Decrement the length by 1
- Return the value of the node removed

```js
shift() {
  //   1   ->     2    ->   3
  if (!this.head) return undefined;
  let currentHead = this.head;
  //   1   ->     2    ->   3
  //  head               tail
  // currHead

  this.head = currentHead.next;
  //   1   ->     2    ->   3
  //            head      tail
  // currHead
  this.length--;
  if(this.length === 0) this.tail = null
  return currentHead;
}
```

## Unshifting pseudocode

- This function shold accept a value
- Create a new node using the value passed to function
- If there is no head property on the list, set the head and tail to be the newly created node
- Otherwise set the newly created node's next property to be the current head property on the list
- Set the head property on the list to be that newly created node
- Increment the length of the list by 1
- Return the linked list

```js
unshift(val) {
  //   1   ->    2   ->   3
  let newNode = new Node(val);
  if (!this.head) {
    this.head = newNode;
    this.tail = this.head;
  } else {
    
    newNode.next = this.head;
    //   val   ->  1   ->   2  ->   3
    // newNode    head             tail
    this.head = newNode;
    //   val   ->   1   ->   2  ->   3
    //  head                        tail
    // newNode
  }
  this.length++;
  return this;
}
```

## Get pseudocode

- This function should accept an index
- If the index is less than zero or greater than or equal to the length of the list,return null
- Loop throught the list until you reach the index and return the node at that specific index

```js
get(index) {
  if (index < 0 || index >= this.length) return null;
  let counter = 0;
  let current = this.head;
  while (counter !== index) {
    current = current.next;
    counter++;
  }
  return current;
}
```

## Set pseudocode

- This function should accept a value and an index
- Use your **get** function to find the specific node.
- If the node is not found, return false
- If the node is found, set the value of that node to be the value passed to the function and return false

```js
set(index, val) {
  let foundNode = this.get(index);
  if (foundNode) {
    foundNode.val = val;
    return true;
  } else {
    return false;
  }
}
```

## Inset pseudocode

- If the index is less than zero or greater than the length, return false
- If the index is the same as the length, push a new node to the end of the list
- If the index is 0, unshift a new node to the start of the list
- Otherwise, using the **get** method, access the node at the index - 1
- Set the next property on that node to be the new node
- Set the next property on the new node to be the previous next

```js
  insert(index, val) {
    // 1  ->  2  ->  3
    if (index < 0 || index > this.length) return false;
    if (index === this.length) return this.push(val);
    if (index === 0) return this.unshift(val);
    let newNode = new Node(val);
    let prev = this.get(index - 1);
    let temp = prev.next;
    prev.next = newNode;
    newNode.next = temp;
    this.length++;
    return true;
  }
```

## Remove pseudocode

- If the index is less than zero or greater than the length, return undefined
- If the index is the same as the length - 1, pop
- If the index is 0, shift
- Otherwise, using the **get** method, access the node at the index - 1
- Set the next property on that node to be the next of the next node
- Decrement the length
- Return the value of the node removed

```js
remove(index) {
  if (index < 0 || index >= this.length) return undefined;
  if (index === this.length - 1) return this.pop();
  if (index === 0) return this.shift();
  let previousNode = this.get(index - 1);
  let removed = previousNode.next;
  previousNode.next = removed.next;
  this.length--;
  return removed;
}
```

## Reverse pseudocode

- Swap the head and tail
- Create a variable called next
- Create a variable called prev
- Create a variable called node and initialize it to the head property
- Loop through the list
- Set next to be the next property on whatever node is
- Set the next property on the node to be whatever prev is
- Set prev to be the value of the node variable
- Set the node variable to be the value of the next variable

```js
reverse() {
  // 1  ->  2  ->  3  -> 4 
  let node = this.head;
  //  1  ->  2  ->  3  ->  4 
  // head                 tail
  // node

  this.head = this.tail;
  this.tail = node;
  //  1      2  ->  3      4 
  // tail                 head
  // node

  let next;
  let prev = null;
  for (let i = 0; i < this.length; i++) {
    next = node.next;
    node.next = prev;
    prev = node;
    node = next;
  }

  return this;
}
```
