# JavaScript Interview Questions

[Want to get a good grasp on **_DSA_** in JavaScript? Check out this doc.](https://github.com/mehedihasan2810/JavaScript-Data-Structures-and-Algorithms)

## Table Of Contents

- [NeetCode 150 Questions & Solutions](#neetcode-150-questions--solutions)
- [General JS Coding Questions & Solutions](#general-js-coding-questions--solutions)

<!--------------------------------------
NeetCode 150 Questions & Solutions start
---------------------------------------->

## NeetCode 150 Questions & Solutions

1. ### ❓ Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

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

   [Original Problem in LeetCode](https://leetcode.com/problems/contains-duplicate/)

   </details>

2. ### ❓ Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

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

   [Original Problem in LeetCode](https://leetcode.com/problems/valid-anagram/)

   </details>

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
