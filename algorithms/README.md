# Sorting algorithm

## Buble sort
```js
for(let i = 0; i < s.length; i++) {
  res += s[i]
}
```

## Selection sort

```js

```

## Merge Sort

```js

```

## Quick Sort

```js

```

## Radix Sort

```ts
// Helper function

function getDigit(num: number, i: number) {
  return Math.floor(Math.abs(num) / Math.pow(10, i) % 10);
}

function digitCount(num: number) {
  if(num === 0) return 1;
  return Math.floor(Math.log10(Math.abs(num))) + 1;
}

function mostDigits(nums: number[]) {
  let maxDigits = 0;
  for(let i = 0; i < nums.length; i++) {
    maxDigits = Math.max(maxDigits, digitCount(nums[i]));
  }
  return maxDigits
}
```

```ts
function radixSort(nums: number[]) {
  let maxDigitCount = mostDigits(nums);
  for(let k = 0; k < maxDigitCount; k++) {
    let digitBuckets = Array.from({length: 10}, () => [])
    for(let i = 0; i < nums.length; i++) {
      let digit = getDigit(nums[i], k)
      digitBuckets[digit].push(nums[i])
    }
    nums = [].concat(...digitBuckets)
  }
  return nums
}

radixSort([122,9,32,57,98,4993,2001,1989,444,256,469,50231])
// [2001, 50231, 122, 32, 4993, 444, 256, 57, 98, 9, 1989, 469]
// [2001, 9, 122, 50231, 32, 444, 256, 57, 469, 1989, 4993, 98]
// [2001, 9, 32, 57, 98, 122, 50231, 256, 444, 469, 1989, 4993]
// [9, 32, 57, 98, 122, 50231, 256, 444, 469, 1989, 2001, 4993]
// [9, 32, 57, 98, 122, 256, 444, 469, 1989, 2001, 4993, 50231]
```

**Big O**

+ Time Complexity(Best): O(nk)

+ Time Complexity(Average): O(nk)

+ Time Complexity(Worst): O(nk)

+ Space Complexity: O(n+ k)

  + n - length of array
  + k - number of digits(average)

