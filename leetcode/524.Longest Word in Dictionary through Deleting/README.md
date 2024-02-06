# 524. Longest Word in Dictionary through Deleting [Link](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/)

`Medium`

## Desciption

Given a string s and a string array dictionary, return the longest string in the dictionary that can be formed by deleting some of the given string characters. If there is more than one possible result, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

---

Example 1:

Input: s = "abpcplea", dictionary = ["ale","apple","monkey","plea"]
Output: "apple"

---

Example 2:

Input: s = "abpcplea", dictionary = ["a","b","c"]
Output: "a"

## Solution

```js
/**
 * @param {string} s
 * @param {string[]} dictionary
 * @return {string}
 */
var findLongestWord = function (s, dictionary) {
  dictionary.sort();

  let maxString = "";

  for (let word of dictionary) {
    if (parrernMatcher(word, s)) {
      maxString = word.length > maxString.length ? word : maxString;
    }
  }

  return maxString;
};

function parrernMatcher(word, pattern) {
  // check the word is match subsequent
  let i = 0;
  let j = 0;
  while (i < word.length && j < pattern.length) {
    if (word[i] === pattern[j]) {
      i++;
      j++;
    } else {
      j++;
    }
  }

  return word.length === i;
}
```
