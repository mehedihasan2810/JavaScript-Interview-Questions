# JavaScript Interview Questions

[Want to get a good grasp on **_DSA_** in JavaScript? Check out this doc.](https://github.com/mehedihasan2810/JavaScript-Data-Structures-and-Algorithms)

## Table Of Contents

- [NeetCode 150 Questions & Solutions](#neetcode-150-questions--solutions)
  - [Arrays & Hashing](#arrays--hashing)
- [General JS Coding Questions & Solutions](#general-js-coding-questions--solutions)

<!--------------------------------------
NeetCode 150 Questions & Solutions start
---------------------------------------->

## NeetCode 150 Questions & Solutions

### **Arrays & Hashing:-**

1. ### ❓ **_Contains Duplicate:-_** Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

   <details>
   <summary>Examples 👉</summary>

   ```smart
   Example 1:
   Input: nums = [1,2,3,1]
   Output: true

   Example 2:
   Input: nums = [1,2,3,4]
   Output: false
   ```

   </details>

   <details>
   <summary>Solutions 👉</summary>

   ```js
   function containsDuplicate(nums) {
     // Create a set to store unique elements
     const uniqueSet = new Set();

     // Iterate through the array
     for (const num of nums) {
       // If the set already contains the current element, it's a duplicate
       if (uniqueSet.has(num)) {
         return true;
       }

       // Add the current element to the set
       uniqueSet.add(num);
     }

     // No duplicates found
     return false;
   }

   // Example usage:
   const array1 = [1, 2, 3, 4, 5];
   console.log(containsDuplicate(array1)); // Output: false

   const array2 = [1, 2, 3, 4, 1];
   console.log(containsDuplicate(array2)); // Output: true
   ```

   > This function uses a set to efficiently check for duplicates as it has constant time complexity for insertions and lookups. If the set already contains an element, it means that the element is a duplicate, and the function returns true. Otherwise, it continues iterating through the array. If the loop completes without finding any duplicates, the function returns false.

   </details>

   [Original Problem in LeetCode](https://leetcode.com/problems/contains-duplicate/)

2. ### ❓ **_Valid Anagram:-_** Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

   <details>
   <summary>Examples 👉</summary>

   ```smart
   Example 1:

   Input: s = "anagram", t = "nagaram"
   Output: true
   Example 2:

   Input: s = "rat", t = "car"
   Output: false
   ```

   </details>

   <details>
   <summary>Solutions 👉</summary>

   ```js
   function isAnagram(s, t) {
     // Check if the lengths are different, if yes, they can't be anagrams
     if (s.length !== t.length) {
       return false;
     }

     // Sort the characters of each string and compare the sorted strings
     const sortedS = s.split("").sort().join("");
     const sortedT = t.split("").sort().join("");

     return sortedS === sortedT;
   }

   // Example usage:
   const string1 = "listen";
   const string2 = "silent";

   console.log(isAnagram(string1, string2)); // Output: true
   ```

   > In this example, the isAnagram function first checks if the lengths of the two strings are different. If they are, the function returns false because strings of different lengths cannot be anagrams. Then, it sorts the characters of each string and compares the sorted strings. If the sorted strings are equal, the function returns true; otherwise, it returns false.

   </details>

   [Original Problem in LeetCode](https://leetcode.com/problems/valid-anagram/)

3. ### ❓ **_Two Sum:-_** Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

   <details>
   <summary>Examples 👉</summary>

   ```smart
   Example 1:
   Input: nums = [2,7,11,15], target = 9
   Output: [0,1]
   Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

   Example 2:
   Input: nums = [3,2,4], target = 6
   Output: [1,2]

   Example 3:
   Input: nums = [3,3], target = 6
   Output: [0,1]
   ```

   </details>

   <details>
   <summary>Solutions 👉</summary>

   ```js
   function twoSum(nums, target) {
     const numIndicesMap = new Map();

     for (let i = 0; i < nums.length; i++) {
       const complement = target - nums[i];

       // Check if the complement is in the map
       if (numIndicesMap.has(complement)) {
         // Return the indices of the two numbers
         return [numIndicesMap.get(complement), i];
       }

       // Add the current number and its index to the map
       numIndicesMap.set(nums[i], i);
     }

     // No solution found
     return [];
   }

   // Example usage:
   const nums = [2, 7, 11, 15];
   const target = 9;

   console.log(twoSum(nums, target)); // Output: [0, 1] (indices of numbers 2 and 7)
   ```

   > In this function, we iterate through the array of numbers (nums). For each number, we calculate its complement (the difference between the target and the current number). We then check if the complement is already in the numIndicesMap. If it is, we have found the pair, and we return the indices of the two numbers. If not, we add the current number and its index to the map. If no solution is found during the loop, we return an empty array.

   > This solution has a time complexity of O(n), where n is the length of the input array.

   </details>

   [Original Problem in LeetCode](https://leetcode.com/problems/two-sum/)

4. ### ❓ **_Group Anagrams:-_** Given an array of strings strs, group the anagrams together. You can return the answer in any order.

   <details>
   <summary>Examples 👉</summary>

   ```smart
   Example 1:
   Input: strs = ["eat","tea","tan","ate","nat","bat"]
   Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

   Example 2:
   Input: strs = [""]
   Output: [[""]]

   Example 3:
   Input: strs = ["a"]
   Output: [["a"]]
   ```

   </details>

   <details>
   <summary>Solutions 👉</summary>

   ```js
   function groupAnagrams(strs) {
     const anagramGroups = new Map();

     for (const str of strs) {
       // Sort the characters of the string
       const sortedStr = str.split("").sort().join("");

       // If the sorted string is not in the map, add it with an empty array
       if (!anagramGroups.has(sortedStr)) {
         anagramGroups.set(sortedStr, []);
       }

       // Add the original string to the group of anagrams
       anagramGroups.get(sortedStr).push(str);
     }

     // Convert the values (groups of anagrams) to an array and return
     return Array.from(anagramGroups.values());
   }

   // Example usage:
   const strs = ["eat", "tea", "tan", "ate", "nat", "bat"];
   console.log(groupAnagrams(strs));
   // Output: [["eat","tea","ate"],["tan","nat"],["bat"]]
   ```

   > In this function, we iterate through the array of strings (strs). For each string, we sort its characters and use the sorted string as a key in the hash map. If the key doesn't exist, we add it with an empty array as the value. We then push the original string to the array associated with that key. Finally, we convert the values (groups of anagrams) to an array and return it.

   > This solution has a time complexity of O(n _ k _ log(k)), where n is the number of strings and k is the maximum length of any string in the array. The dominant factor is the sorting of characters in each string.

    </details>

   [Original Problem in LeetCode](https://leetcode.com/problems/group-anagrams/)

<br>

<!--------------------------------------
NeetCode 150 Questions & Solutions end
---------------------------------------->

## General JS Coding Questions & Solutions

1. ### ❓ Given a string, reverse each word in the sentence

> For example `Welcome to javascript interview questions` should be become `emocleW ot tpircsavaj weivretni snoitseuq`

   <details>
   <summary>Answer 👉</summary>

```js
function reverseBySeparator(str, separator) {
  return str.split(separator).reverse().join(separator);
}

const str = "Welcome to javascript interview questions";

const reverseBySentence = reverseBySeparator(str, "");

const reverseEachWord = reverseBySeparator(reverseBySentence, " ");

console.log(reverseEachWord); // emocleW ot tpircsavaj weivretni snoitseuq
```

</details>

<br>

2. ### ❓ How to empty an array in javascript?

<details>
   <summary>
   Answer 👉
   </summary>

```js
const arr = [1, 3, 4];

// Method 1
arr.length = 0; // it will empty all the reference variable which pointing to the original `arr`

// Method 2
arr = []; // it will not change all the reference variable but only the `arr`

// Method 3
arr.splice(0, arr.length); // it will empty all the reference variable which pointing to the original `arr`

// Method 4
while (arr.length) {
  arr.pop();
}
```

</details>

<br>

3. ### ❓ FizzBuzz Challenge

> Create a loop which iterates up to 100 while outputting `fizz` at multiples of `3`, `buzz` at multiples of `5` and `fizzbuzz` at multiples of `3` and `5`

<details>
<summary>Answer 👉</summary>

```js
function fizzBuzz(num) {
  for (let i = 1; i <= num; i++) {
    let fizz = i % 3 === 0,
      buzz = i % 5 === 0;

    const result = fizz ? (buzz ? "Fizz Buzz" : "Fizz") : buzz ? "Buzz" : i;

    console.log(result);
  }
}

fizzBuzz(100);
```

</details>

<br>

4. ### ❓ Check if two strings are anagrams of one another

> **_Anagrams_** - A word, phrase, or name formed by rearranging the letters of another, such as `spar`, formed from `rasp`.

<details>
<summary>Answer 👉</summary>

```js
function checkAnagrams(str1, str2) {
  const a = str1.toLowerCase().split("").sort().join("");
  const b = str2.toLowerCase().split("").sort().join("");
  return a === b;
}

console.log(checkAnagrams("Mary", "Army")); // true
console.log(checkAnagrams("Mary", "Arma")); // false
```

</details>

<br>

5. ### ❓ Check if a string is palindrome or not

> **_Palindrome_** - a word, phrase, or sequence that reads the same backwards as forwards, e.g. madam or nurses run.

<details>
<summary>Answer 👉</summary>

```js
function checkPalindrome(str) {
  const str2 = str.replace(/\W/gi, "").toLowerCase();
  return str2.split("").reverse().join("") === str2;
}

console.log(checkPalindrome("level")); // true
console.log(checkPalindrome("level!")); // true
console.log(checkPalindrome("mehedi")); // false
```

</details>

[🔝 Back to top](#coding-questions)

<br>

6. ### ❓ What will be the out of the following output?

```js
let a = 1;

if (function f() {}) {
  a += typeof f;
}

console.log(a);
```

<details>
<summary>Answer & Explanation 👉</summary>

`'1undefined'`

> The function `f` is indeed defined within the if statement, but it's not invoked, and its reference is not accessible outside the if block. As a result, when you try to access the `typeof f` outside the block, it will be `'undefined'` because the function declaration doesn't affect the scope outside the block.

</details>

<br>

7. ### ❓ Guess the outputs of the following codes

```js
function func1() {
  setTimeout(() => {
    console.log(x);
    console.log(y);
  }, 3000);

  var x = 2;
  let y = 12;
}
func1();
```

<details>
<summary>Answer & Explanation 👉</summary>

`2`
`12`

> Outputs `2` and `12`. Since, even though let variables are not hoisted, due to the async nature of javascript, the complete function code runs before the setTimeout function. Therefore, it has access to both x and y.

</details>
