# Binary Search Tree (BST)

## Setting up the startup

```js
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class BinarySearchTree {
  constructor() {
    this.root = null;
  }
}
```

## INSERTING A NODE

Steps - Iteratively or Recursively

- Create a new node
- Starting ar the root
  - Check if there is a root, if not - the root now becomes that new node!
  - If there is a root, check if the values of the new node is greater than or
  - If it is greater
    - Check to see if there is a node to the right
      - If there is, move to that node and repeat these steps
      - If there is not, add that node as the right property
  - If it is less
    - Check to see if there is a node to the left
      - If there is, move to that node and repeat there steps
      - If there is not, add that node as the left property

```js
insert(value) {
  let newNode = new Node(value);
  if (this.root === null) {
    this.root = newNode;
    return this;
  }

  let current = this.root;

  while (true) {
    if (value === current.value) return undefined;

    if (value < current.value) {
      if (current.left === null) {
        current.left = newNode;
        return this;
      }
      current = current.left;
    } else {
      if (current.right === null) {
        current.right = newNode;
        return this;
      }
      current = current.right;
    }
  }
}
```

### Finding a Node in a BST

Steps - Iteratively or Recursively

- Starting at the root
  - Check if there is a root, if not, we're done searching!
  - If there is a root, check if the value of the new node is the value we are looking for.
  - If not , check to see if the value is fgreater than or less than the value of the root
  - If it is greater
    - Check to see if there is a node to the right
      - If there is, move to that node and repeat there steps
      - If there is not, we're done searching!
  - If it is less
    - Check to see if there is a node to the left
      - If there is, move to that node and repeat there steps
      - If there is not, we're done searching!

```js
find(value) {
  if (this.root === null) return false;
  let current = this.root,
    found = false;
  while (current && !found) {
    if (value < current.value) {
      current = current.left;
    } else if (value > current.value) {
      current = current.right;
    } else {
      found = true;
    }
  }
  if (!found) return undefined;
  return current;
}
```

### Big O of BST

- Insertion - O(log n)
- Searching - O(log n)

## Breadth-First Search (BFS)

![BFS](https://img-blog.csdnimg.cn/20190317005509279.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lpZmVuNDIzNA==,size_16,color_FFFFFF,t_70)

### Setting up our tree

```js
var tree = new BinarySearchTree();
tree.insert(10);
tree.insert(5);
tree.insert(13);
tree.insert(11);
tree.insert(2);
tree.insert(16);
tree.insert(7);

//       10
//   5        13
// 2   7    11   16
```

### Steps - iteratively

- Create a queue (this can be an array) and a variable to store the values of nodes visited
- Place the root node in the queue
- Loop as long as there is anything in the queue
  - Dequeue a node from the queue and push the value of the node into the variable that stores the nodes
  - If there is a left property on the node dequeue - add it to the queue
  - If there is a right property on the node dequeue - add it to the queue
- Return the variable that stores the values

```js
BFS() {
  let node = this.root;
  let data = [];
  let queue = [];
  queue.push(node);
  while (queue.length) {
    node = queue.shift();
    data.push(node.value);
    if (node.left) queue.push(node.left);
    if (node.right) queue.push(node.right);
  }

  return data;
}
// [10, 5, 13, 2, 7, 11, 16]
```

## Depth-First Search (DFS) - PreOrder

### setps - Recursively

- Create a variable to store the values of nodes visited
- Store the root of the BST in a variable called current
- Write a helper function which accepts a node
  - Push the value of the node to the variable that stores the values
  - If the node has a left property, call the helper function with the left peoperty on the node
  - If the node has a right property, call the helper function with the right property on the node
- Invoke the helper function with the current variable
- Return ther array of values

```js
DFSPreOrder() {
  let data = [];
  function traverse(node) {
    data.push(node);
    if (node.left) traverse(node.left);
    if (node.right) traverse(node.right);
  }
  traverse(this.root);
  return data;
}
// [10, 5, 2, 7, 13, 11, 16]
```

## Depth-First Search (DFS) - PostOrder

### steps - Recursivly

- Create a variable to store the values of nodes visited
- Store the root of the BST in a variable called current
- Write a helper function which accepts a node
  - If the node has a left property, call the helper function
    with the left property on the node
  - If the node has a right property, call the helper function with the right property on the node
  - Push the value of the node to the variable that stores the values
- Invoke the helper function with the current variable
- Return the array of values

```js
DFSPostOrder() {
  const data = [];
  function traverse(node) {
    if (node.left) traverse(node.left);
    if (node.right) traverse(node.right);
    data.push(node.value);
  }
  traverse(this.root);
  return data;
}
// [2, 7, 5, 11, 16, 13, 10]
```

## Depth-First Search (DFS) - InOrder

### Steps - Recursively

- Create a variable to store the values of nodes visited
- Store the root of the BST in a variable called current
- Write a helper function which accepts a node
  - If the node has a left property, call the helper function with the left property on the node
  - Push the value of the node to the variable that stores the values
  - If the node has a right property, call the helpwe function with the right property on the node
- Invoke the helper function with the current variable

```js
DFSInOrder() {
  const data = [];
  if(!this.root) return data
  function traverse(node) {
    if (node.left) traverse(node.left);
    data.push(node.value);
    if (node.right) traverse(node.right);
  }
  traverse(this.root);
  return data;
}
// [2, 5, 7, 10, 11, 13, 16]
```

## Recap

- Trees are non-linear data structures that contain a root and child nodes
- Binary Trees can have values of any type, but at most two children for each parent
- Binary Search Trees are a more specific version of binary trees where every node to the left of a parent is lessthan it's value and every node to the right is greater
- We can search through Trees using BFS and DFS
