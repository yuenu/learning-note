# Sorting algorithm

## Setting **SWAP** function

```js
function swap(arr, idx1, idx2) {
  let temp = arr[idx1];
  arr[idx1] = arr[idx2];
  arr[idx2] = temp;
}
```

## Buble sort

![bubble sort](https://upload.wikimedia.org/wikipedia/commons/0/06/Bubble-sort.gif)

- Strat looping from with a variable called i the end of the array towards the beginning
- Start an inner loop with a variable called j from teh beginning until **i - 1**
- if arr[j] is greater than arr[j + 1] ,swap those two values!

```js
function bubbleSort(arr) {
  let noSwap;
  for (let i = arr.length; i > 0; i--) {
    noSwap = true;
    for (let j = 0; j < i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
        noSwap = false;
      }
    }
    if (noSwap) break;
  }
  return arr;
}
```

## Selection sort

![selection sort](https://i0.wp.com/algorithms.tutorialhorizon.com/files/2019/01/Selection-Sort-Gif.gif?fit=300%2C214&ssl=1)

- Store the first element as the smallest value you're seen so far.
- Compare this item to the next item in the array until you find a smaller number
- If a smaller number is found, designate that smaller number to be the new **"minimum"** and continue until the end of the array.
- If the **"minimum"** is not the value(index) you initially began with, swap the two values.
- Repeat this with the next element until the array is sorted.

```js
function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let lowest = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[lowest]) {
        lowest = j;
      }
    }
    if (i !== lowest) {
      swap(arr, i, lowest);
    }
  }
  return arr;
}
```

## Insertion Sort

![insertion sort](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)

- Start by picling the second elemtn in the array
- Now compare the second element with the one before it and swap if necessary
- Continue to the next element and if it is the incorrect order, iterate through the sorted portion(i.e the left side) to place the element in the correct place.

```js
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let currentVal = arr[i];

    let j = i - 1;
    while (j > -1 && currentVal < arr[j]) {
      arr[j + 1] = arr[j];
      j--;
    }
    arr[j + 1] = currentVal;
  }
  return arr;
}
```

## Merge Sort
![merge sort](https://miro.medium.com/max/1400/1*61Mf0zjVfd1s3_SzUNGxPA.png)

### merge pseudocode

- Create an empty array, take a look at the smallest values in each input array
- While there are still values we haven't looked at...
  - If the value in the first array is smaller than the value in the second array, push the value in the first array into our results and move on to the next value in the first array
  - If the value in the first array is larger than the value in the second array, push the value in the second array into our results amd move on to the next value in the second array
  - Once we exhaust one array, push in all remaining values from the other array

```js
function merge(arr1, arr2) {
  let results = [];
  let i = 0;
  let j = 0;
  while (i < arr1.length && j < arr2.length) {
    if (arr2[j] > arr1[i]) {
      results.push(arr1[i]);
      i++;
    } else {
      results.push(arr2[j]);
      j++;
    }
  }

  while (i < arr1.length) {
    results.push(arr1[i]);
    i++;
  }

  while (j < arr2.length) {
    results.push(arr2[j]);
    j++;
  }
  return results;
}
```

### mergeSort Pseudocode

- Break up the array into halves until you have arrays that are empty or have one element
- Once you have smaller sorted arrays, merge those arrays with other sorted arrays until you are back at the full length of the array
- Once the array has been merged back together, return teh merged (and sorted!) array

```js
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  let mid = Math.floor(arr.length / 2);
  let left = mergeSort(arr.slice(0, mid));
  let right = mergeSort(arr.slice(mid));
  return merge(left, right);
}
```

## Quick Sort

![quick sort](https://1.bp.blogspot.com/-qkBgZvw19qA/XoAcJbwCs5I/AAAAAAAACvA/WYUwKTPcIU0ckhru_tPDestSc-u9d87XACLcBGAsYHQ/s1600/ba915e7cf4ace758143fe94df260c34a.jpg)

- Like merge sort, exploits the fact that arrays of 0 or 1 element are always sorted
- Works by selecting one element (call the "pivot") and finding the index where the pivot should end up in the sorted array
- Once the pivot is positioned appropriately, quick sort can be applied on either side of the pivot

### Pivot Helper

- In order to implement merge sort, it's useful to first implement a function responsible arranging elements in an array on either side of a pivot
- Given an array, this helper function should designate an element as the pivot
- It shold then rearrange elements in the array so that all values less than the pivot are moved to the left of the pivot, and all values greater than the pivot are moved to the right of the pivot
- The order of elements on either side of the pivot doesn't matter
- The helper should do this **in place**, that is, it should not create a new array
- When complete, the helper should return teh index of the pivot

### Pivot Pseudocode

- It will help to accept three arguments: an array, a start index, and an end index(these can default to 0 and the array length minus 1, respectively)
- Grab the pivot from the start of the array
- Store the current pivot index in a variable (this will kepp track of where the pivot should end up)
- Loop throught the array from the start until the end
  - If the pivot is greater than the current element, increment with the element at the pivot index
- Swap the starting element (i.e the pivot) with the pivot index
- Return the pivot index

```js
function pivot(arr, start = 0, end = arr.length + 1) {
  let pivot = arr[start];
  let swapIdx = start;
  for (let i = start + 1; i < arr.length; i++) {
    if (pivot > arr[i]) {
      swapIdx++;
      swap(arr, swapIdx, i);
    }
  }
  swap(arr, start, swapIdx);
  return swapIdx;
}
```

### Quicksort Pseudocode

- Call the pivot helper on the array
- When the helper returns to you the updated pivot index, recursively call the pivot helper on the subarray to the left of that index, and the subarray to the right of that index

```js
function quickSort(arr, left = 0, right = arr.length - 1) {
  if (left < right) {
    let pivotIndex = pivot(arr, left, right);
    // left
    quickSort(arr, left, pivotIndex - 1);
    // right
    quickSort(arr, pivotIndex + 1, right);
  }
  return arr;
}
```

## Radix Sort

![radix sort](https://www.codingeek.com/wp-content/uploads/2017/02/radix.png)

```ts
// Helper function

function getDigit(num: number, i: number) {
  return Math.floor((Math.abs(num) / Math.pow(10, i)) % 10);
}

function digitCount(num: number) {
  if (num === 0) return 1;
  return Math.floor(Math.log10(Math.abs(num))) + 1;
}

function mostDigits(nums: number[]) {
  let maxDigits = 0;
  for (let i = 0; i < nums.length; i++) {
    maxDigits = Math.max(maxDigits, digitCount(nums[i]));
  }
  return maxDigits;
}
```

```ts
function radixSort(nums: number[]) {
  let maxDigitCount = mostDigits(nums);
  for (let k = 0; k < maxDigitCount; k++) {
    let digitBuckets = Array.from({ length: 10 }, () => []);
    for (let i = 0; i < nums.length; i++) {
      let digit = getDigit(nums[i], k);
      digitBuckets[digit].push(nums[i]);
    }
    nums = [].concat(...digitBuckets);
  }
  return nums;
}

radixSort([122, 9, 32, 57, 98, 4993, 2001, 1989, 444, 256, 469, 50231]);
// [2001, 50231, 122, 32, 4993, 444, 256, 57, 98, 9, 1989, 469]
// [2001, 9, 122, 50231, 32, 444, 256, 57, 469, 1989, 4993, 98]
// [2001, 9, 32, 57, 98, 122, 50231, 256, 444, 469, 1989, 4993]
// [9, 32, 57, 98, 122, 50231, 256, 444, 469, 1989, 2001, 4993]
// [9, 32, 57, 98, 122, 256, 444, 469, 1989, 2001, 4993, 50231]
```

**Big O**

- Time Complexity(Best): O(nk)

- Time Complexity(Average): O(nk)

- Time Complexity(Worst): O(nk)

- Space Complexity: O(n+ k)

  - n - length of array
  - k - number of digits(average)
