## 77.Combinations [link](https://leetcode.com/problems/combinations/)
`Medium`

Given two integers n and k, return all possible combinations of k numbers out of the range [1, n].

You may return the answer in any order.




### Constraints:
* 1 <= n <= 20
* 1 <= k <= n
---

## Solution 1
```js
function combine(n: number, k: number): number[][] {
    
  const result = []
  function traverse(arr, depth) {
    //console.log(arr, depth)

    if (arr.length === k) {
      result.push(arr);
      return;
    }
    
    if (depth > n) {      
      return;
    }

    traverse(arr, depth + 1);  
    traverse(arr.concat(depth), depth + 1);
  }

  traverse([], 1);
        
  return result
};
```

log
```js
// [] 1
// [] 2
// [] 3
// [] 4
// [] 5
// [ 4 ] 5
// [ 3 ] 4
// [ 3 ] 5
// [ 3, 4 ] 5 -> push
// [ 2 ] 3
// [ 2 ] 4
// [ 2 ] 5
// [ 2, 4 ] 5 -> push
// [ 2, 3 ] 4 -> push
// [ 1 ] 2
// [ 1 ] 3
// [ 1 ] 4
// [ 1 ] 5
// [ 1, 4 ] 5 -> push
// [ 1, 3 ] 4 -> push
// [ 1, 2 ] 3 -> push
```

## Solution 2

```js
function combine(n: number, k: number, index=1, curr: number[] = [], paths: number[][] = []): number[][] {
    console.log('curr:', curr, 'path:', path, 'idx:', index)
  
    if (curr.length === k) {
        paths.push(curr)
        return paths
    }
    
    for (let i = index; i <= n; i++) {
        let temp = [...curr, i]
        combine(n, k, i+1, temp, paths)
    }
    
    return paths
};
```

log
```js
// curr: [] paths: [] idx: 1
// curr: [ 1 ] paths: [] idx: 2
// curr: [ 1, 2 ] paths: [] idx: 3
// curr: [ 1, 3 ] paths: [ [ 1, 2 ] ] idx: 4
// curr: [ 1, 4 ] paths: [ [ 1, 2 ], [ 1, 3 ] ] idx: 5
// curr: [ 2 ] paths: [ [ 1, 2 ], [ 1, 3 ], [ 1, 4 ] ] idx: 3
// curr: [ 2, 3 ] paths: [ [ 1, 2 ], [ 1, 3 ], [ 1, 4 ] ] idx: 4
// curr: [ 2, 4 ] paths: [ [ 1, 2 ], [ 1, 3 ], [ 1, 4 ], [ 2, 3 ] ] idx: 5
// curr: [ 3 ] paths: [ [ 1, 2 ], [ 1, 3 ], [ 1, 4 ], [ 2, 3 ], [ 2, 4 ] ] idx: 4
// curr: [ 3, 4 ] paths: [ [ 1, 2 ], [ 1, 3 ], [ 1, 4 ], [ 2, 3 ], [ 2, 4 ] ] idx: 5
// curr: [ 4 ] paths: [ [ 1, 2 ], [ 1, 3 ], [ 1, 4 ], [ 2, 3 ], [ 2, 4 ], [ 3, 4 ] ] idx: 5
```