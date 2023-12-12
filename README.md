# JavaScript Interview Questions

## Table Of Contents

- [Coding Questions](#coding-questions)

## Coding Questions

- ### Given a string, reverse each word in the sentence

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

- ## How to empty an array in javascript?

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
