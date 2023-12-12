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
