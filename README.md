# JavaScript Interview Questions

> [For DSA related questions checkout this doc](https://github.com/mehedihasan2810/JavaScript-Data-Structures-and-Algorithms)

## Table Of Contents

- [Coding Questions](#coding-questions)

## Coding Questions

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
