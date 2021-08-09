# Hash Table

## Hash function

### Writing our hash function first
```js
class HashTable {
  constructor(size = 53) {
    this.keyMap = new Array(size);
  }

  _hash(key) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      let char = key[i];
      let value = char.charCodeAt(0) - 96;
      total = (total * WEIRD_PRIME + value) % this.keyMap;
    }
    return total;
  }
}
```

## Set / Get

### set

1. Accepts a key and a value
2. Hashes the key
3. Stores the key-value pair in the hash table array via separate chaining

```js
set(key,value){
  let index = this._hash(key);
  if(!this.keyMap[index]){
    this.keyMap[index] = [];
  }
  this.keyMap[index].push([key, value]);
}
```
### get

1. Accepts a key
2. Hashes the key
3. Retrieves the key-value pair in the hash table
4. If the key isn't found, returns **undefined**

```js
get(key){
  let index = this._hash(key);
  if(this.keyMap[index]){
    for(let i = 0; i < this.keyMap[index].length; i++){
      if(this.keyMap[index][i][0] === key) {
        return this.keyMap[index][i][1]
      }
    }
  }
  return undefined;
}
```

## Keys / Values

### keys
1. Loops through the hash table array and returns an array of keys in the table

```js
keys() {
  let keysArr = [];
  for (let i = 0; i < this.keyMap.length; i++) {
    if (this.keyMap[i]) {
      for (let j = 0; j < this.keyMap[i].length; j++) {
        if (!keysArr.includes(this.keyMap[i][j][0])) {
          keysArr.push(this.keyMap[i][j][0]);
        }
      }
    }
  }
  return keysArr;
}
```

### values
1. Loops through the hash table array and returns and array of values in the table

```js
values() {
  let valuesArr = [];
  for (let i = 0; i < this.keyMap.length; i++) {
    if (this.keyMap[i]) {
      for (let j = 0; j < this.keyMap[i].length; j++) {
        if (!valuesArr.includes(this.keyMap[i][j][1])) {
          valuesArr.push(this.keyMap[i][j][1]);
        }
      }
    }
  }
  return valuesArr;
}
```