# JavaScript Interview Questions

[Want to get a good grasp on **_DSA_** in JavaScript? Check out this doc.](https://github.com/mehedihasan2810/JavaScript-Data-Structures-and-Algorithms)

## Table Of Contents

- [NeetCode 150 Questions & Solutions](#neetcode-150-questions--solutions)
  - [Arrays & Hashing](#arrays--hashing)
  - [Two Pointers](#two-pointers)
  - [Stack](#stack)
  - [Binary Search](#binary-search)
  - [Linked List](#linkedlist)
  - [Trees](#trees)
  - [Design System](#design-system)
  - [Misc](#misc)
- [General JS Coding Questions & Solutions](#general-js-coding-questions--solutions)

<!--------------------------------------
NeetCode 150 Questions & Solutions start
---------------------------------------->

## NeetCode 150 Questions & Solutions

## Arrays & Hashing

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

5. ### ❓ **_Top K Frequent Elements:-_** Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

   <details>
   <summary>Examples 👉</summary>

   ```smart
   Example 1:
   Input: nums = [1,1,1,2,2,3], k = 2
   Output: [1,2]

   Example 2:
   Input: nums = [1], k = 1
   Output: [1]
   ```

   </details>

    <details>
    <summary>Solutions 👉</summary>

   ```js
   function topKFrequent(nums, k) {
     // Create a frequency map to store the count of each number
     const frequencyMap = new Map();

     // Populate the frequency map
     for (const num of nums) {
       frequencyMap.set(num, (frequencyMap.get(num) || 0) + 1);
     }

     // Create an array of buckets to store numbers with the same frequency
     const buckets = new Array(nums.length + 1).fill(null).map(() => []);

     // Distribute numbers into buckets based on their frequency
     for (const [num, frequency] of frequencyMap) {
       buckets[frequency].push(num);
     }

     // Iterate through buckets in reverse order to get the top k frequent elements
     const result = [];
     for (let i = buckets.length - 1; i >= 0 && result.length < k; i--) {
       if (buckets[i].length > 0) {
         result.push(...buckets[i]);
       }
     }

     return result;
   }

   // Example usage:
   const nums = [1, 1, 1, 2, 2, 3];
   const k = 2;

   console.log(topKFrequent(nums, k)); // Output: [1, 2]
   ```

   > In this function, we first create a frequency map to count the occurrences of each number in the input array. Then, we use buckets to group numbers with the same frequency together. Finally, we iterate through the buckets in reverse order to get the top k frequent elements.

   > This solution has a time complexity of O(n), where n is the size of the input array. The bucket sort step takes O(n) time, and iterating through the buckets in reverse order ensures that we get the top k frequent elements efficiently.

    </details>

   [Original Problem in LeetCode](https://leetcode.com/problems/top-k-frequent-elements/)

6. ### ❓ **_Product of Array Except Self:-_** Given an integer array nums, return an array answer such that `answer[i]` is equal to the product of all the elements of nums except `nums[i]`.

   <details>
   <summary>Examples 👉</summary>

   ```smart
   Example 1:
   Input: nums = [1,2,3,4]
   Output: [24,12,8,6]

   Example 2:
   Input: nums = [-1,1,0,-3,3]
   Output: [0,0,9,0,0]
   ```

   </details>

    <details>
    <summary>Solutions 👉</summary>

   ```js
   function productExceptSelf(nums) {
     const n = nums.length;

     // Initialize the result array
     const result = new Array(n).fill(1);

     // Calculate the product to the left of each element and update the result array
     let leftProduct = 1;
     for (let i = 0; i < n; i++) {
       result[i] *= leftProduct;
       leftProduct *= nums[i];
     }

     // Calculate the product to the right of each element and update the result array
     let rightProduct = 1;
     for (let i = n - 1; i >= 0; i--) {
       result[i] *= rightProduct;
       rightProduct *= nums[i];
     }

     return result;
   }

   // Example usage:
   const nums = [1, 2, 3, 4];
   console.log(productExceptSelf(nums));
   // Output: [24, 12, 8, 6]
   ```

   > This approach has a time complexity of O(n) as required. we use the result array to store the products to the left and right of each element as we iterate through the array. This eliminates the need for separate left and right product arrays, resulting in O(1) extra space complexity.

    </details>

   [Original Problem in LeetCode](https://leetcode.com/problems/product-of-array-except-self/)

7. ### ❓ **_Encode and Decode Strings:-_** Design an algorithm to encode a lists of strings to string and the encoded string is then sent over the network and is decoded back to original list of strings.

     <details>
     <summary>Solutions 👉</summary>

   ```js
   class StringEncoderDecoder {
     constructor() {
       this.delimiter = ";";
     }

     // Encode a list of strings to a single string
     encode(strList) {
       return strList.join(this.delimiter);
     }

     // Decode a string to a list of strings
     decode(encodedStr) {
       return encodedStr.split(this.delimiter);
     }
   }

   // Example usage:
   const stringEncoderDecoder = new StringEncoderDecoder();

   const originalStrings = ["apple", "banana", "orange"];
   const encodedString = stringEncoderDecoder.encode(originalStrings);
   console.log("Encoded String:", encodedString); // Encoded String: apple;banana;orange

   const decodedStrings = stringEncoderDecoder.decode(encodedString);
   console.log("Decoded Strings:", decodedStrings); // Decoded Strings: [ 'apple', 'banana', 'orange' ]
   ```

   > In this example, the StringEncoderDecoder class has encode and decode methods. The encode method takes an array of strings, joins them using a delimiter (in this case, ';'), and returns the encoded string. The decode method takes an encoded string, splits it using the same delimiter, and returns an array of strings.

   > This is a simple representation, and you might want to consider additional techniques or encoding formats based on your specific requirements and constraints (e.g., dealing with special characters, handling empty strings, etc.). If security is a concern, you might also want to explore more robust encoding/decoding methods.

    </details>

   [Original Problem in LeetCode](https://leetcode.com/problems/encode-and-decode-strings/)

8. ### ❓ **_Longest Consecutive Sequence:-_** Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.

    <details>
   <summary>Examples 👉</summary>

   ```smart
   Example 1:
   Input: nums = [100,4,200,1,3,2]
   Output: 4
   Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

   Example 2:
   Input: nums = [0,3,7,2,5,8,4,6,0,1]
   Output: 9
   ```

   </details>

    <details>
    <summary>Solutions 👉</summary>

   ```js
   function longestConsecutive(nums) {
     if (nums.length === 0) {
       return 0;
     }

     const numSet = new Set(nums);
     let longestStreak = 1;

     for (const num of numSet) {
       if (!numSet.has(num - 1)) {
         let currentNum = num;
         let currentStreak = 1;

         while (numSet.has(currentNum + 1)) {
           currentNum += 1;
           currentStreak += 1;
         }

         longestStreak = Math.max(longestStreak, currentStreak);
       }
     }

     return longestStreak;
   }

   // Example usage:
   const nums = [100, 4, 200, 1, 3, 2];
   console.log(longestConsecutive(nums)); // Output: 4 (the sequence is 1, 2, 3, 4)
   ```

   > In this implementation, we use a set (numSet) to store the unique elements in the array. We iterate through the array and, for each element, check if it is the start of a sequence by verifying that there is no previous consecutive element in the set. If it is the start, we iterate forward to find the consecutive elements and update the longest streak accordingly.

   > This algorithm has O(n) time complexity because each element is processed at most twice (once when identified as a possible start, and once when part of a sequence), and set operations are generally O(1) on average.

    </details>

   [Original Problem in LeetCode](https://leetcode.com/problems/longest-consecutive-sequence/)

<br>

[🔼 Back to top](#table-of-contents)

## Two Pointers

9. ### ❓ **_Valid Palindrome:-_** A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers. Given a string s, return true if it is a palindrome, or false otherwise.

    <details>
   <summary>Examples 👉</summary>

   ```smart
   Example 1:

   Input: s = "A man, a plan, a canal: Panama"
   Output: true
   Explanation: "amanaplanacanalpanama" is a palindrome.
   Example 2:

   Input: s = "race a car"
   Output: false
   Explanation: "raceacar" is not a palindrome.
   Example 3:

   Input: s = " "
   Output: true
   Explanation: s is an empty string "" after removing non-alphanumeric characters.
   Since an empty string reads the same forward and backward, it is a palindrome.
   ```

   </details>

    <details>
    <summary>Solutions 👉</summary>

   ```js
   // Array - Filter && Clone && Reverse
   // Time O(N) | Space O(N)
   function isPalindrome(str) {
     const alphaNumericChars = str.toLowerCase().replace(/[^a-z-9]/gi, "");
     return (
       alphaNumericChars === alphaNumericChars.split("").reverse().join("")
     );
   }

   console.log(isPalindrome("A man, a plan, a canal: Panama")); // true
   console.log(isPalindrome("race a car")); // false
   console.log(isPalindrome(" ")); // true

   // -----------------------------------------------------------------------

   // 2 Pointer | Midde Convergence
   // Time O(N) | Space O(1)
   function isPalindrome(s) {
     if (s.length <= 1) return true;

     let [left, right] = [0, s.length - 1];
     let leftChar, rightChar;
     while (left < right) {
       leftChar = s[left];
       rightChar = s[right];

       // skip char if non-alphanumeric
       if (!/[a-zA-Z0-9]/.test(leftChar)) {
         left++;
       } else if (!/[a-zA-Z0-9]/.test(rightChar)) {
         right--;
       } else {
         // compare letters
         if (leftChar.toLowerCase() != rightChar.toLowerCase()) {
           return false;
         }
         left++;
         right--;
       }
     }
     return true;
   }

   console.log(isPalindrome("A man, a plan, a canal: Panama")); // true
   console.log(isPalindrome("race a car")); // false
   console.log(isPalindrome(" ")); // true
   ```

   > The two-pointer approach involves initializing two pointers (left and right) at the beginning and end of the cleaned string, respectively. We then iterate towards the center while comparing characters. If there is a mismatch at any point, the string is not a palindrome.

   > This solution has a time complexity of O(n), where n is the length of the cleaned string.

   </details>

   [Original Problem in LeetCode](https://leetcode.com/problems/valid-palindrome/)

10. ### ❓ **_3Sum:-_** Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`. Notice that the solution set must not contain duplicate triplets.

     <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: nums = [-1,0,1,2,-1,-4]
    Output: [[-1,-1,2],[-1,0,1]]
    Explanation:
    nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
    nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
    nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
    The distinct triplets are [-1,0,1] and [-1,-1,2].
    Notice that the order of the output and the order of the triplets does not matter.

    Example 2:
    Input: nums = [0,1,1]
    Output: []
    Explanation: The only possible triplet does not sum up to 0.

    Example 3:
    Input: nums = [0,0,0]
    Output: [[0,0,0]]
    Explanation: The only possible triplet sums up to 0.
    ```

    </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    function threeSum(nums) {
      const res = [];
      nums.sort((a, b) => a - b);

      for (let i = 0; i < nums.length; i++) {
        const a = nums[i];
        if (a > 0) break;
        if (i > 0 && a === nums[i - 1]) continue;

        let l = i + 1;
        let r = nums.length - 1;
        while (l < r) {
          const threeSum = a + nums[l] + nums[r];
          if (threeSum > 0) {
            r--;
          } else if (threeSum < 0) {
            l++;
          } else {
            res.push([a, nums[l], nums[r]]);
            l++;
            r--;
            while (nums[l] === nums[l - 1] && l < r) {
              l++;
            }
          }
        }
      }
      return res;
    }

    console.log(threeSum([-1, 0, 1, 2, -1, -4])); // [ [ -1, -1, 2 ], [ -1, 0, 1 ] ]
    ```

    - We sort the array to simplify the two-pointer approach.
    - We iterate through the array and use two pointers to find triplets whose sum is zero.
    - We skip duplicates to ensure that the solution set doesn't contain duplicate triplets.
    - The time complexity of this solution is O(n^2), where n is the length of the input array.

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/3sum/)

11. ### ❓ **_Two Sum II - Input Array Is Sorted:-_** Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 < numbers.length`. Return the indices of the two numbers, index1 and index2, added by one as an integer array `[index1, index2]` of length 2.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: numbers = [2,7,11,15], target = 9
    Output: [1,2]
    Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

    Example 2:
    Input: numbers = [2,3,4], target = 6
    Output: [1,3]
    Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].

    Example 3:
    Input: numbers = [-1,0], target = -1
    Output: [1,2]
    Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    function twoSum(numbers, target) {
      let left = 0;
      let right = numbers.length - 1;

      while (left < right) {
        const sum = numbers[left] + numbers[right];

        if (sum === target) {
          return [left + 1, right + 1]; // Adding 1 to convert from 0-based to 1-based indices
        } else if (sum < target) {
          left++;
        } else {
          right--;
        }
      }

      // No solution found, but the problem statement guarantees exactly one solution
      return [];
    }

    // Example usage:
    const numbers = [2, 7, 11, 15];
    const target = 9;
    console.log(twoSum(numbers, target)); // Output: [1, 2]
    ```

    **Explanation:**

    - Initialize two pointers (left and right) at the beginning and end of the array.

    - Calculate the sum of the elements at the current pointers.

    - If the sum is equal to the target, return the indices of the two numbers.

    - If the sum is less than the target, increment the left pointer to explore larger values.

    - If the sum is greater than the target, decrement the right pointer to explore smaller values.

    - Repeat steps 2-5 until the pointers meet or the solution is found.

    > The time complexity of this solution is O(n), where n is the length of the input array, because each pointer moves at most n times. The space complexity is O(1) since only a constant amount of extra space is used.

     </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

12. ### ❓ **_Container With Most Water:-_** You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are `(i, 0)` and `(i, height[i])`. Find two lines that together with the x-axis form a container, such that the container contains the most water. Return the maximum amount of water a container can store. Notice that you may not slant the container.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: height = [1,8,6,2,5,4,8,3,7]
    Output: 49
    Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

    Example 2:
    Input: height = [1,1]
    Output: 1
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    function maxArea(height) {
      let maxWater = 0;
      let left = 0;
      let right = height.length - 1;

      while (left < right) {
        const hLeft = height[left];
        const hRight = height[right];
        const h = Math.min(hLeft, hRight);
        const w = right - left;
        const area = h * w;

        maxWater = Math.max(maxWater, area);

        if (hLeft < hRight) {
          left++;
        } else {
          right--;
        }
      }

      return maxWater;
    }

    // Example usage:
    const height = [1, 8, 6, 2, 5, 4, 8, 3, 7];
    console.log(maxArea(height)); // Output: 49
    ```

    **In this implementation:**

    - left and right are the two pointers initialized at the beginning and end of the array.
    - The while loop continues until left is less than right.
    - Calculate the area using the minimum height of the two lines (h) and the width (w).
    - Update maxWater if the current area is greater.
    - Move the pointers toward each other based on the shorter line, as moving the pointer of the longer line won't possibly result in a larger area.
    - This algorithm has a time complexity of O(n), where n is the length of the input array. The two-pointer approach ensures that we explore all possible combinations of lines.

     </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/container-with-most-water/)

13. ### ❓ **_Longest Substring Without Repeating Characters:-_** Given a string s, find the length of the longest substring without repeating characters.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: s = "abcabcbb"
    Output: 3
    Explanation: The answer is "abc", with the length of 3.

    Example 2:
    Input: s = "bbbbb"
    Output: 1
    Explanation: The answer is "b", with the length of 1.

    Example 3:
    Input: s = "pwwkew"
    Output: 3
    Explanation: The answer is "wke", with the length of 3.
    Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    function lengthOfLongestSubstring(s) {
      let maxLength = 0;
      let windowStart = 0;
      const charIndexMap = new Map();

      for (let windowEnd = 0; windowEnd < s.length; windowEnd++) {
        const currentChar = s[windowEnd];

        if (charIndexMap.has(currentChar)) {
          // If the current character is already in the substring, update the windowStart
          windowStart = Math.max(
            windowStart,
            charIndexMap.get(currentChar) + 1
          );
        }

        // Update the character's index in the map
        charIndexMap.set(currentChar, windowEnd);

        // Update the maximum length of the substring
        maxLength = Math.max(maxLength, windowEnd - windowStart + 1);
      }

      return maxLength;
    }

    // Example usage:
    const s = "abcabcbb";
    console.log(lengthOfLongestSubstring(s)); // Output: 3
    ```

    **In this implementation:**

    - windowStart represents the start index of the current substring.
    - windowEnd represents the end index of the current substring.
    - charIndexMap is a Map that stores the most recent index of each character in the substring.
    - As the window slides to the right, the function updates windowStart whenever a repeating character is encountered and updates the charIndexMap accordingly.
    - The maximum length of the substring is calculated and updated in each iteration.
      > This algorithm has a time complexity of O(n), where n is the length of the input string, as each character is visited at most twice (once by the windowEnd and once by the windowStart). The space complexity is O(min(m, n)), where m is the size of the character set. In most cases, the character set is constant, so the space complexity is O(1).
      </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

14. ### ❓ **_Longest Repeating Character Replacement:-_** You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times. Return the length of the longest substring containing the same letter you can get after performing the above operations.

      <details>
      <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: s = "ABAB", k = 2
    Output: 4
    Explanation: Replace the two 'A's with two 'B's or vice versa.

    Example 2:
    Input: s = "AABABBA", k = 1
    Output: 4
    Explanation: Replace the one 'A' in the middle with 'B' and form "AABBBBA".
    The substring "BBBB" has the longest repeating letters, which is 4.
    There may exists other ways to achieve this answer too.
    ```

      </details>

      <details>
      <summary>Solutions 👉</summary>

    ```js
    function characterReplacement(s, k) {
      let maxLength = 0;
      let maxCount = 0;
      let windowStart = 0;
      const charCount = new Array(26).fill(0); // Assuming only uppercase English characters

      for (let windowEnd = 0; windowEnd < s.length; windowEnd++) {
        const charIndex = s.charCodeAt(windowEnd) - "A".charCodeAt(0);
        charCount[charIndex]++;

        maxCount = Math.max(maxCount, charCount[charIndex]);

        // If the number of characters to change (window size - maxCount) exceeds the allowed operations (k), shrink the window
        if (windowEnd - windowStart + 1 - maxCount > k) {
          charCount[s.charCodeAt(windowStart) - "A".charCodeAt(0)]--;
          windowStart++;
        }

        // Update the maxLength
        maxLength = Math.max(maxLength, windowEnd - windowStart + 1);
      }

      return maxLength;
    }

    // Example usage:
    const s = "ABAB";
    const k = 2;
    console.log(characterReplacement(s, k)); // Output: 4
    ```

    **In this implementation:**

    - windowStart and windowEnd represent the sliding window indices.
    - charCount is an array to store the count of characters within the current window.
    - maxCount keeps track of the maximum count of a single character within the window.
    - If the number of characters to change (window size - maxCount) exceeds the allowed operations (k), shrink the window from the left.
    - Update maxLength in each iteration.
    - This algorithm has a time complexity of O(n), where n is the length of the input string, as it iterates through the string only once. The space complexity is O(1) since the size of the character set is constant.
    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/longest-repeating-character-replacement/)

    [Video Explanation](https://youtu.be/gqXU1UyA8pk?si=2LShGEILILSJm94a)

<br>

[🔼 Back to top](#table-of-contents)

## Stack

15. ### ❓ **_Valid Parentheses:-_** Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:

    Input: s = "()"
    Output: true
    Example 2:

    Input: s = "()[]{}"
    Output: true
    Example 3:

    Input: s = "(]"
    Output: false
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    function isValid(s) {
      const stack = [];
      const bracketMap = {
        "(": ")",
        "{": "}",
        "[": "]",
      };

      for (let i = 0; i < s.length; i++) {
        const currentBracket = s[i];

        if (bracketMap[currentBracket]) {
          // If it's an opening bracket, push it onto the stack
          stack.push(currentBracket);
        } else {
          // If it's a closing bracket, check if it matches the top of the stack
          const lastOpeningBracket = stack.pop();

          if (currentBracket !== bracketMap[lastOpeningBracket]) {
            // If not, the string is invalid
            return false;
          }
        }
      }

      // After iterating through the string, the string is valid if the stack is empty
      return stack.length === 0;
    }

    // Example usage:
    console.log(isValid("()")); // Output: true
    console.log(isValid("()[]{}")); // Output: true
    console.log(isValid("(]")); // Output: false
    console.log(isValid("([)]")); // Output: false
    console.log(isValid("{[]}")); // Output: true

    // ----------------------------------------------

    //-------------
    // With Regexp
    //-------------
    function isValid(s) {
      const bracketRegex = /(\(\)|\{\}|\[\])+/g;

      // Replace valid bracket pairs with an empty string until no more valid pairs can be found
      while (bracketRegex.test(s)) {
        s = s.replace(bracketRegex, "");
      }

      // If the resulting string is empty, the original string was valid
      return s.length === 0;
    }

    // Example usage:
    console.log(isValid("()")); // Output: true
    console.log(isValid("()[]{}")); // Output: true
    console.log(isValid("(]")); // Output: false
    console.log(isValid("([)]")); // Output: false
    console.log(isValid("{[]}")); // Output: true
    ```

    **In this implementation:**

    - The stack is used to keep track of the opening brackets.
    - The bracketMap is a mapping of opening brackets to their corresponding closing brackets.
    - When iterating through the string, if an opening bracket is encountered, it is pushed onto the stack.
    - If a closing bracket is encountered, it is checked against the top of the stack to ensure that the brackets match.
    - After iterating through the string, the string is considered valid if the stack is empty.
      > This algorithm has a time complexity of O(n), where n is the length of the input string, as it iterates through the string once. The space complexity is also O(n) in the worst case when all opening brackets are at the beginning of the string.
        </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/valid-parentheses/)

16. ### ❓ **_Min Stack:-_** Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input
    ["MinStack","push","push","push","getMin","pop","top","getMin"]
    [[],[-2],[0],[-3],[],[],[],[]]

    Output
    [null,null,null,null,-3,null,0,-2]

    Explanation
    MinStack minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    minStack.getMin(); // return -3
    minStack.pop();
    minStack.top();    // return 0
    minStack.getMin(); // return -2
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    // LinkedList Approach
    // Time O(1) | Space O(1)
    class MinStack {
      constructor() {
        this.head = null;
      }

      push(val) {
        this.head = !this.head /* Space O(1) */
          ? new Node(val, val, null)
          : new Node(val, Math.min(val, this.head.min), this.head);
      }

      pop() {
        this.head = this.head.next; /* Time O(1) */
      }

      top() {
        return this.head.val; /* Time O(1) */
      }

      getMin() {
        return this.head.min; /* Time O(1) */
      }
    }

    class Node {
      constructor(val, min, next) {
        this.val = val;
        this.min = min;
        this.next = next;
      }
    }

    const minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    console.log(minStack.getMin()); // return -3
    minStack.pop();
    console.log(minStack.top()); // return 0
    console.log(minStack.getMin()); // return -2

    // --------------------------------------------

    // Array Approach
    // Time O(1) | Space O(n)
    class MinStack {
      constructor() {
        this.stack = [];
        this.minStack = [];
      }

      push(val, { minStack } = this) {
        this.stack.push(val); /* Space O(N) */

        const isMinEmpty = !minStack.length;
        const hasNewMin = val <= this.top(minStack);
        const canAddMin = isMinEmpty || hasNewMin;
        if (canAddMin) minStack.push(val); /* Space O(N) */
      }

      pop({ stack, minStack } = this) {
        const top = stack.pop(); /* Time O(1) */

        const canPopMin = top === this.getMin();
        if (canPopMin) minStack.pop(); /* Time O(1) */
      }

      top(stack = this.stack) {
        return stack.length ? stack[stack.length - 1] /* Time O(1) */ : null;
      }

      getMin(minStack = this.minStack) {
        return this.top(minStack); /* Time O(1) */
      }
    }

    const minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    console.log(minStack.getMin()); // return -3
    minStack.pop();
    console.log(minStack.top()); // return 0
    console.log(minStack.getMin()); // return -2
    ```

    In this implementation:

    - The Node class represents each node in the linked list, storing the value, minimum, and a reference to the next node.
    - The MinStack class uses the head pointer to represent the top of the stack.
    - When pushing a new element, a new node is created with the current value, the minimum of the current value and the minimum of the previous node, and a reference to the previous node.
    - The pop, top, and getMin functions then operate based on the current head node.
      > This implementation maintains the minimum value at each node, allowing constant time retrieval of the minimum element.
          </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/min-stack/)

17. ### ❓ **_Evaluate Reverse Polish Notation:-_** You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation. Evaluate the expression. Return an integer that represents the value of the expression.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: tokens = ["2","1","+","3","*"]
    Output: 9
    Explanation: ((2 + 1) * 3) = 9

    Example 2:
    Input: tokens = ["4","13","5","/","+"]
    Output: 6
    Explanation: (4 + (13 / 5)) = 6

    Example 3:
    Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
    Output: 22
    Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
    = ((10 * (6 / (12 * -11))) + 17) + 5
    = ((10 * (6 / -132)) + 17) + 5
    = ((10 * 0) + 17) + 5
    = (0 + 17) + 5
    = 17 + 5
    = 22
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    // Time O(N) | Space(N)
    function evalRPN(tokens, stack = []) {
      for (const char of tokens) {
        /* Time O(N) */
        const isOperation = char in OPERATORS;
        if (isOperation) {
          const value = performOperation(char, stack);

          stack.push(value); /* Space O(N) */

          continue;
        }

        stack.push(Number(char)); /* Space O(N) */
      }

      return stack.pop();
    }

    const OPERATORS = {
      "+": (a, b) => a + b,
      "-": (a, b) => a - b,
      "*": (a, b) => a * b,
      "/": (a, b) => Math.trunc(a / b),
    };

    const performOperation = (char, stack) => {
      const [rightNum, leftNum] = [stack.pop(), stack.pop()];
      const operation = OPERATORS[char];

      return operation(leftNum, rightNum);
    };

    console.log(evalRPN(["2", "1", "+", "3", "*"])); // Output: 9
    console.log(evalRPN(["4", "13", "5", "/", "+"])); // Output: 6
    console.log(
      evalRPN([
        "10",
        "6",
        "9",
        "3",
        "+",
        "-11",
        "*",
        "/",
        "*",
        "17",
        "+",
        "5",
        "+",
      ])
    ); // Output: 22
    ```

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

18. ### ❓ **_Generate Parentheses:-_** Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

    ![image graph of how generate parentheses algorithm works](/assets/validP.webp)
    <br>
    Image Credit: [Dev Genius](https://blog.devgenius.io/10-daily-practice-problems-day-18-f7293b55224d)

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: n = 3
    Output: ["((()))","(()())","(())()","()(())","()()()"]

    Example 2:
    Input: n = 1
    Output: ["()"]
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    // Time O(2^N) Space O(n)
    function generateParenthesis(n) {
      const result = [];

      function backtrack(current, openCount, closeCount) {
        if (current.length === 2 * n) {
          result.push(current);
          return;
        }

        if (openCount < n) {
          backtrack(current + "(", openCount + 1, closeCount);
        }

        if (closeCount < openCount) {
          backtrack(current + ")", openCount, closeCount + 1);
        }
      }

      backtrack("", 0, 0);
      return result;
    }

    // Example usage:
    const n = 3;
    const result = generateParenthesis(n);
    console.log(result); // [ '((()))', '(()())', '(())()', '()(())', '()()()' ]

    // --------------------------------------------------------

    // Stack Approach
    // Time O(2^N) Space O(n)
    var generateParenthesis = function (n) {
      const stack = [];
      const res = [];

      function backtrack(openN, closedN) {
        if (openN === closedN && openN === n) {
          res.push(stack.join(""));
          return;
        }

        if (openN < n) {
          stack.push("(");
          backtrack(openN + 1, closedN);
          stack.pop();
        }

        if (closedN < openN) {
          stack.push(")");
          backtrack(openN, closedN + 1);
          stack.pop();
        }
      }

      backtrack(0, 0);
      return res;
    };

    // Example usage:
    const result = generateParenthesis(3);
    console.log(result); // [ '((()))', '(()())', '(())()', '()(())', '()()()' ]
    ```

    **In this code:**

    - The generateParenthesis function initializes an empty array result to store the generated combinations.
    - The backtrack function is a recursive function that explores all possible combinations.
    - The base case checks if the length of the current combination is equal to 2 \* n. If so, it adds the combination to the result.
    - The recursive cases handle adding an open parenthesis '(' if the count of open parentheses is less than n, and adding a close parenthesis ')' if the count of close parentheses is less than the count of open parentheses.
    - The function is called initially with an empty string and counts for open and close parentheses set to 0.

      > This approach generates all possible combinations by exploring valid paths in the recursion tree. The resulting result array contains all well-formed parentheses combinations for the given value of n.

      </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/generate-parentheses/)

19. ### ❓ **_Daily Temperatures:-_** Given an array of integers temperatures represents the daily temperatures, return an array answer such that `answer[i]` is the number of days you have to wait after the ith day to get a warmer temperature. If there is no future day for which this is possible, keep answer`[i] == 0` instead.

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: temperatures = [73,74,75,71,69,72,76,73]
    Output: [1,1,4,2,1,1,0,0]

    Example 2:
    Input: temperatures = [30,40,50,60]
    Output: [1,1,1,0]

    Example 3:
    Input: temperatures = [30,60,90]
    Output: [1,1,0]
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    function dailyTemperatures(temperatures) {
      const n = temperatures.length;
      const result = new Array(n).fill(0);
      const stack = [];

      for (let i = 0; i < n; i++) {
        while (
          stack.length > 0 &&
          temperatures[i] > temperatures[stack[stack.length - 1]]
        ) {
          const prevIndex = stack.pop();
          result[prevIndex] = i - prevIndex;
        }
        stack.push(i);
      }

      return result;
    }

    // Example usage:
    const temperatures = [73, 74, 75, 71, 69, 72, 76, 73];
    const result = dailyTemperatures(temperatures);
    console.log(result); // [ 1, 1, 4, 2, 1, 1, 0, 0 ]
    ```

    **In this code:**

    - We use a stack (stack) to keep track of the indices of the temperatures.
    - We iterate through the temperatures array and pop the stack until the current temperature is greater than the temperature at the top of the stack.
    - For each popped index, we calculate the difference between the current index and the popped index, representing the number of days to wait for a warmer temperature.
    - We push the current index onto the stack.
    - The result array is updated with the number of days to wait for a warmer temperature for each day.

      > This solution has a time complexity of O(n), where n is the length of the temperatures array, and a space complexity of O(n).

      </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/daily-temperatures/)

20. ### ❓ **_Largest Rectangle in Histogram:-_** Given an array of integers heights representing the histogram's bar height where the width of each bar is 1, return the area of the largest rectangle in the histogram.

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: heights = [2,1,5,6,2,3]
    Output: 10
    Explanation: The above is a histogram where width of each bar is 1.
    The largest rectangle is shown in the red area, which has an area = 10 units.

    Example 2:
    Input: heights = [2,4]
    Output: 4
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    function largestRectangleArea(heights) {
      const stack = [];
      let maxArea = 0;

      for (let i = 0; i <= heights.length; i++) {
        while (
          stack.length > 0 &&
          (i === heights.length ||
            heights[i] < heights[stack[stack.length - 1]])
        ) {
          const height = heights[stack.pop()];
          const width =
            stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
          maxArea = Math.max(maxArea, height * width);
        }
        stack.push(i);
      }

      return maxArea;
    }

    // Example usage:
    const heights = [2, 1, 5, 6, 2, 3];
    const result = largestRectangleArea(heights);
    console.log(result); // 10
    ```

    **In this code:**

    - We use a stack (stack) to maintain the indices of the histogram bars.
    - We iterate through the histogram bars and pop the stack until the current bar is taller than the bar at the top of the stack. For each popped bar, we calculate the area of the rectangle formed with that bar as the smallest bar.
    - The width of the rectangle is determined by the difference between the current index and the index at the top of the stack. If the stack is empty, the width is the current index.
    - We update the maxArea with the maximum area encountered during the process.
    - We push the current index onto the stack.

      > The final result is the maximum area of the rectangle in the histogram.
      > This solution has a time complexity of O(n), where n is the length of the heights array, and a space complexity of O(n).

        </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/)

<br>

[🔼 Back to top](#table-of-contents)

## Binary Search

21. ### ❓ **_Search a 2D Matrix:-_** You are given an m x n integer matrix matrix with the following two properties: Each row is sorted in non-decreasing order. The first integer of each row is greater than the last integer of the previous row. Given an integer target, return true if target is in matrix or false otherwise. You must write a solution in O(log(m \* n)) time complexity.

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
    Output: true

    Example 2:
    Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
    Output: false
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    function searchMatrix(matrix, target) {
      if (!matrix || matrix.length === 0 || matrix[0].length === 0) {
        return false;
      }

      const m = matrix.length;
      const n = matrix[0].length;

      let left = 0;
      let right = m * n - 1;

      while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        const midElement = matrix[Math.floor(mid / n)][mid % n];

        if (midElement === target) {
          return true;
        } else if (midElement < target) {
          left = mid + 1;
        } else {
          right = mid - 1;
        }
      }

      return false;
    }

    // Example usage:
    const matrix = [
      [1, 3, 5, 7],
      [10, 11, 16, 20],
      [23, 30, 34, 60],
    ];
    const target = 3;
    const result = searchMatrix(matrix, target);
    console.log(result); // true
    ```

    **In this code:**

    - The binary search is performed on the flattened array of the matrix.
    - The midElement is calculated using the formula matrix[Math.floor(mid / n)][mid % n].
    - If midElement is equal to the target, we return true.
    - If midElement is less than the target, we update the left pointer.
    - If midElement is greater than the target, we update the right pointer.
    - The loop continues until the left pointer is greater than the right pointer.
      > This solution has a time complexity of O(log(m \* n)) as required.

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/search-a-2d-matrix/)

22. ### ❓ **_Koko Eating Bananas:-_** Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours. Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour. Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return. Return the minimum integer k such that she can eat all the bananas within h hours.

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: piles = [3,6,7,11], h = 8
    Output: 4

    Example 2:
    Input: piles = [30,11,23,4,20], h = 5
    Output: 30

    Example 3:
    Input: piles = [30,11,23,4,20], h = 6
    Output: 23
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    function minEatingSpeed(piles, h) {
      let left = 1;
      let right = Math.max(...piles);

      while (left <= right) {
        const mid = Math.floor((left + right) / 2);

        if (canEatAll(piles, h, mid)) {
          // If it's possible to eat all bananas at this speed, try a lower speed.
          right = mid - 1;
        } else {
          // If it's not possible to eat all bananas at this speed, try a higher speed.
          left = mid + 1;
        }
      }

      return left;
    }

    // Helper function to check if it's possible to eat all bananas at a given speed.
    function canEatAll(piles, h, speed) {
      let hoursNeeded = 0;

      for (const pile of piles) {
        hoursNeeded += Math.ceil(pile / speed);
      }

      return hoursNeeded <= h;
    }

    // Example usage:
    const piles = [3, 6, 7, 11];
    const h = 8;
    const result = minEatingSpeed(piles, h);
    console.log(result); // 4
    ```

    **In this code:**

    - The binary search is performed on the possible values of k (speed).
    - The canEatAll function checks if it's possible to eat all bananas at a given speed within h hours.
    - If it's possible, we try a lower speed; otherwise, we try a higher speed.
    - The final result is the minimum speed required to eat all bananas within h hours.
      > This solution has a time complexity of O(n log m), where n is the length of the piles array and m is the maximum number of bananas in any pile.

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/koko-eating-bananas/)

23. ### ❓ **_Find Minimum in Rotated Sorted Array:-_** Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array `nums = [0,1,2,4,5,6,7]` might become: `[4,5,6,7,0,1,2]` if it was rotated 4 times. `[0,1,2,4,5,6,7]` if it was rotated 7 times. Notice that rotating an array `[a[0], a[1], a[2], ..., a[n-1]]` 1 time results in the array `[a[n-1], a[0], a[1], a[2], ..., a[n-2]]`. Given the sorted rotated array nums of unique elements, return the minimum element of this array. You must write an algorithm that runs in O(log n) time.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: nums = [3,4,5,1,2]
    Output: 1
    Explanation: The original array was [1,2,3,4,5] rotated 3 times.

    Example 2:
    Input: nums = [4,5,6,7,0,1,2]
    Output: 0
    Explanation: The original array was [0,1,2,4,5,6,7] and it was rotated 4 times.

    Example 3:
    Input: nums = [11,13,15,17]
    Output: 11
    Explanation: The original array was [11,13,15,17] and it was rotated 4 times.
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    function findMin(nums) {
      let left = 0;
      let right = nums.length - 1;

      while (left < right) {
        const mid = Math.floor((left + right) / 2);

        if (nums[mid] > nums[right]) {
          // The pivot is on the right half, search in the right half.
          left = mid + 1;
        } else {
          // The pivot is on the left half or at the mid index itself, search in the left half.
          right = mid;
        }
      }

      return nums[left];
    }

    // Example usage:
    const rotatedArray1 = [4, 5, 6, 7, 0, 1, 2];
    const result1 = findMin(rotatedArray1);
    console.log(result1); // Output: 0

    const rotatedArray2 = [0, 1, 2, 4, 5, 6, 7];
    const result2 = findMin(rotatedArray2);
    console.log(result2); // Output: 0
    ```

    **In this code:**

    - The binary search is used to find the pivot point.
    - If nums[mid] > nums[right], it means the pivot is on the right half, so we search in the right half.
    - If nums[mid] <= nums[right], it means the pivot is on the left half or at the mid index itself, so we search in the left half.
    - The loop continues until left and right converge to the pivot point.
    - The minimum element is at the index left (or right).
      > This solution has a time complexity of O(log n), where n is the length of the array.

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

24. ### ❓ **_Search in Rotated Sorted Array:-_** There is an integer array nums sorted in ascending order (with distinct values). Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (0-indexed). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index 3 and become `[4,5,6,7,0,1,2]`. Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums. You must write an algorithm with `O(log n)` runtime complexity.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:

    Input: nums = [4,5,6,7,0,1,2], target = 0
    Output: 4
    Example 2:

    Input: nums = [4,5,6,7,0,1,2], target = 3
    Output: -1
    Example 3:

    Input: nums = [1], target = 0
    Output: -1
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    function search(nums, target) {
      let left = 0;
      let right = nums.length - 1;

      while (left <= right) {
        const mid = Math.floor((left + right) / 2);

        if (nums[mid] === target) {
          return mid;
        }

        if (nums[left] <= nums[mid]) {
          // Left half is sorted.
          if (target >= nums[left] && target < nums[mid]) {
            // Target is in the left sorted half.
            right = mid - 1;
          } else {
            // Target is in the rotated half.
            left = mid + 1;
          }
        } else {
          // Right half is sorted.
          if (target > nums[mid] && target <= nums[right]) {
            // Target is in the right sorted half.
            left = mid + 1;
          } else {
            // Target is in the rotated half.
            right = mid - 1;
          }
        }
      }

      return -1; // Target not found.
    }

    // Example usage:
    const rotatedArray1 = [4, 5, 6, 7, 0, 1, 2];
    const target1 = 0;
    const result1 = search(rotatedArray1, target1);
    console.log(result1); // Output: 4

    const rotatedArray2 = [4, 5, 6, 7, 0, 1, 2];
    const target2 = 3;
    const result2 = search(rotatedArray2, target2);
    console.log(result2); // Output: -1
    ```

    **In this code:**

    - We use binary search to find the target in the rotated sorted array.
    - We check whether the left or right half is sorted.
    - Depending on whether the target is in the sorted half or the rotated half, we adjust the search space accordingly.
    - The loop continues until left and right converge, or the target is found.
      > This solution has a time complexity of O(log n), where n is the length of the array.

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/search-in-rotated-sorted-array/)

25. ### ❓ **_Time Based Key-Value Store:-_** Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.

    **Implement the TimeMap class:**

    - TimeMap() Initializes the object of the data structure.
    - void set(String key, String value, int timestamp) Stores the key key with the value value at the given time timestamp.
    - String get(String key, int timestamp) Returns a value such that set was called previously, with timestamp_prev <= timestamp. If there are multiple such values, it returns the value associated with the largest timestamp_prev. If there are no values, it returns "".

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input
    ["TimeMap", "set", "get", "get", "set", "get", "get"]
    [[], ["foo", "bar", 1], ["foo", 1], ["foo", 3], ["foo", "bar2", 4], ["foo", 4], ["foo", 5]]
    Output
    [null, null, "bar", "bar", null, "bar2", "bar2"]

    Explanation:
    TimeMap timeMap = new TimeMap();
    timeMap.set("foo", "bar", 1);  // store the key "foo" and value "bar" along with timestamp = 1.
    timeMap.get("foo", 1);         // return "bar"
    timeMap.get("foo", 3);         // return "bar", since there is no value corresponding to foo at timestamp 3 and timestamp 2, then the only value is at timestamp 1 is "bar".
    timeMap.set("foo", "bar2", 4); // store the key "foo" and value "bar2" along with timestamp = 4.
    timeMap.get("foo", 4);         // return "bar2"
    timeMap.get("foo", 5);         // return "bar2"
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    class TimeMap {
      constructor() {
        // Initialize the data structure.
        this.data = new Map();
      }

      set(key, value, timestamp) {
        // Store the key with the value and timestamp.
        if (!this.data.has(key)) {
          this.data.set(key, []);
        }
        this.data.get(key).push({ timestamp, value });
      }

      get(key, timestamp) {
        let value = "";

        // Retrieve the value associated with the largest timestamp_prev.
        if (!this.data.has(key)) {
          return value;
        }

        const values = this.data.get(key);

        // Perform binary search to find the largest timestamp_prev.
        let left = 0;
        let right = values.length - 1;

        while (left <= right) {
          const mid = Math.floor((left + right) / 2);
          if (values[mid].timestamp <= timestamp) {
            value = values[mid].value;
            left = mid + 1;
          } else {
            right = mid - 1;
          }
        }

        return value;
      }
    }

    // Example usage:
    const timeMap = new TimeMap();
    timeMap.set("foo", "bar", 1);
    console.log(timeMap.get("foo", 1)); // Output: "bar"
    console.log(timeMap.get("foo", 3)); // Output: "bar"
    timeMap.set("foo", "bar2", 4);
    console.log(timeMap.get("foo", 4)); // Output: "bar2"
    console.log(timeMap.get("foo", 5)); // Output: "bar2"
    ```

    **In this implementation:**

    - The set method stores key-value pairs with timestamps in a list for each key.
    - The get method retrieves the value associated with the largest timestamp_prev using binary search.
      > This solution has a time complexity of O(log n) for both the set and get methods, where n is the number of timestamps for a given key. The space complexity is O(n).

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/time-based-key-value-store/)

26. ### ❓ **_Median of Two Sorted Arrays:-_** Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: nums1 = [1,3], nums2 = [2]
    Output: 2.00000
    Explanation: merged array = [1,2,3] and median is 2.

    Example 2:
    Input: nums1 = [1,2], nums2 = [3,4]
    Output: 2.50000
    Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    function findMedianSortedArrays(nums1, nums2) {
      if (nums1.length > nums2.length) {
        [nums1, nums2] = [nums2, nums1]; // Ensure nums1 is the shorter array.
      }

      const x = nums1.length;
      const y = nums2.length;
      let low = 0;
      let high = x;

      while (low <= high) {
        const partitionX = Math.floor((low + high) / 2);
        const partitionY = Math.floor((x + y + 1) / 2) - partitionX;

        const maxX =
          partitionX === 0 ? Number.NEGATIVE_INFINITY : nums1[partitionX - 1];
        const minX =
          partitionX === x ? Number.POSITIVE_INFINITY : nums1[partitionX];
        const maxY =
          partitionY === 0 ? Number.NEGATIVE_INFINITY : nums2[partitionY - 1];
        const minY =
          partitionY === y ? Number.POSITIVE_INFINITY : nums2[partitionY];

        if (maxX <= minY && maxY <= minX) {
          if ((x + y) % 2 === 0) {
            return (Math.max(maxX, maxY) + Math.min(minX, minY)) / 2;
          } else {
            return Math.max(maxX, maxY);
          }
        } else if (maxX > minY) {
          high = partitionX - 1;
        } else {
          low = partitionX + 1;
        }
      }

      throw new Error("Input arrays are not sorted.");
    }

    // Example usage:
    const nums1 = [1, 3];
    const nums2 = [2];
    console.log(findMedianSortedArrays(nums1, nums2)); // Output: 2.0
    ```

    **In this implementation:**

    - We ensure nums1 is the shorter array to optimize the binary search.
    - We use binary search to find a partition in nums1 such that the elements on the left side of the partition are less than or equal to the elements on the right side.
    - We calculate corresponding partitions in nums2.
    - We check if the partitioning is correct, and if so, we calculate the median based on the values at the boundaries of the partitions.
    - If the partitioning is not correct, we adjust the search range based on whether we need to move left or right in the search space.
      > This approach has a time complexity of O(log(min(m, n))).

     </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/median-of-two-sorted-arrays/)

<br>

[🔼 Back to top](#table-of-contents)

## LinkedList

27. ### ❓ **_Reverse Linked List:-_** Given the head of a singly linked list, reverse the list, and return the reversed list.

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: head = [1,2,3,4,5]
    Output: [5,4,3,2,1]

    Example 2:
    Input: head = [1,2]
    Output: [2,1]

    Example 3:
    Input: head = []
    Output: []
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    function reverseList(head) {
      let prev = null;
      let curr = head;
      let next = null;

      while (curr !== null) {
        next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
      }

      return prev;
    }
    ```

    **In this implementation:**

    > The time complexity of this algorithm is O(n), where n is the length of the linked list, as we traverse the list once. The space complexity is O(1), as we use a constant amount of extra space regardless of the input size.

     </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/reverse-linked-list/)

28. ### ❓ **_Merge Two Sorted Lists:-_** You are given the heads of two sorted linked lists list1 and list2. Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists. Return the head of the merged linked list.

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: list1 = [1,2,4], list2 = [1,3,4]
    Output: [1,1,2,3,4,4]

    Example 2:
    Input: list1 = [], list2 = []
    Output: []

    Example 3:
    Input: list1 = [], list2 = [0]
    Output: [0]
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    // Time O(N + M) | Space O(1)
    class ListNode {
      constructor(val, next = null) {
        this.val = val;
        this.next = next;
      }
    }

    function mergeTwoLists(list1, list2) {
      // Create a dummy node to simplify the code
      const dummy = new ListNode(0);
      let current = dummy;

      while (list1 !== null && list2 !== null) {
        if (list1.val < list2.val) {
          current.next = list1;
          list1 = list1.next;
        } else {
          current.next = list2;
          list2 = list2.next;
        }
        current = current.next;
      }

      // If one of the lists is not empty, append the remaining nodes
      current.next = list1 || list2;

      // OR

      // if (list1 !== null) {
      //  current.next = list1;
      // } else {
      //  current.next = list2;
      // }

      return dummy.next;
    }

    // Example usage:
    const list1 = new ListNode(1, new ListNode(2, new ListNode(4)));
    const list2 = new ListNode(1, new ListNode(3, new ListNode(4)));
    const mergedList = mergeTwoLists(list1, list2);
    console.log(mergedList);

    ////////////////////////
    // Recursive solution
    // Time O(N + M) | Space O(N + M)
    ///////////////////////
    function mergeTwoLists(list1, list2) {
      if (!list1) return list2;
      if (!list2) return list1;

      if (list1.val <= list2.val) {
        list1.next = mergeTwoLists(list1.next, list2);
        return list1;
      } else {
        list2.next = mergeTwoLists(list1, list2.next);
        return list2;
      }
    }
    ```

    **In this implementation:**

    > This implementation uses a dummy node to simplify handling of the merged list. The mergeTwoLists function iterates through both lists, comparing the values of the current nodes, and appends the smaller node to the merged list. The process continues until one of the lists is exhausted. Finally, if one of the lists still has remaining nodes, they are appended to the merged list.

    > The time complexity of this algorithm is O(m + n), where m and n are the lengths of the input linked lists. This is because we iterate through both lists once. The space complexity is O(1), as we use a constant amount of extra space regardless of the input sizes.

     </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/merge-two-sorted-lists/)

29. ### ❓ **_Reorder List:-_** You are given the head of a singly linked-list. The list can be represented as:

    ```smart
    L0 → L1 → … → Ln - 1 → Ln
    Reorder the list to be on the following form:

    L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
    You may not modify the values in the list's nodes. Only nodes themselves may be changed.
    ```

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: head = [1,2,3,4]
    Output: [1,4,2,3]

    Example 2:
    Input: head = [1,2,3,4,5]
    Output: [1,5,2,4,3]
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    class ListNode {
      constructor(val, next = null) {
        this.val = val;
        this.next = next;
      }
    }

    function reorderList(head) {
      if (!head || !head.next) {
        return head; // Handling empty or single-node list
      }

      // Step 1: Find the middle of the linked list
      let slow = head;
      let fast = head;

      while (fast.next && fast.next.next) {
        slow = slow.next;
        fast = fast.next.next;
      }

      // Step 2: Reverse the second half of the linked list
      let secondHalf = reverseList(slow.next);
      slow.next = null; // Cut off the first half

      // Step 3: Merge the first half and the reversed second half
      mergeLists(head, secondHalf);
    }

    function reverseList(head) {
      let prev = null;
      let current = head;

      while (current !== null) {
        const nextNode = current.next;
        current.next = prev;
        prev = current;
        current = nextNode;
      }

      return prev;
    }

    function mergeLists(first, second) {
      while (second !== null) {
        const nextFirst = first.next;
        const nextSecond = second.next;

        first.next = second;
        second.next = nextFirst;

        first = nextFirst;
        second = nextSecond;
      }
    }

    // Example usage:
    const originalList = new ListNode(
      1,
      new ListNode(2, new ListNode(3, new ListNode(4, new ListNode(5))))
    );
    console.log("Original List:", getListValues(originalList)); // Original List: [ 1, 2, 3, 4, 5 ]

    reorderList(originalList);
    console.log("Reordered List:", getListValues(originalList)); // Reordered List: [ 1, 5, 2, 4, 3 ]

    function getListValues(head) {
      const values = [];
      let current = head;
      while (current !== null) {
        values.push(current.val);
        current = current.next;
      }
      return values;
    }
    ```

    **In this implementation:**

    - reverseList function reverses a linked list.
    - mergeLists function merges two linked lists, alternating nodes from each list.
      > The time complexity is O(n), where n is the length of the linked list, and the space complexity is O(1), as we use a constant amount of extra space.

     </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/reorder-list/)

30. ### ❓ **_Linked List Cycle:-_** Given head, the head of a linked list, determine if the linked list has a cycle in it. There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter. Return true if there is a cycle in the linked list. Otherwise, return false.

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: head = [3,2,0,-4], pos = 1
    Output: true
    Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).

    Example 2:
    Input: head = [1,2], pos = 0
    Output: true
    Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.

    Example 3:
    Input: head = [1], pos = -1
    Output: false
    Explanation: There is no cycle in the linked list.
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    // Time O(n) | Space O(1)
    function hasCycle(head) {
      let slow = head;
      let fast = head;

      // Use the slow and fast algorithm to detect a cycle
      while (fast.next && fast.next.next) {
        slow = slow.next;
        fast = fast.next.next;

        // If there is a cycle, the slow and fast will eventually meet
        if (slow === fast) {
          return true;
        }
      }

      // If fast reaches the end, there is no cycle
      return false;
    }
    ```

    **In this algorithm:**

    - The tortoise and hare pointers are initialized at the head of the linked list.
    - The hare moves twice as fast as the tortoise. If there is a cycle, the hare will eventually catch up to the tortoise within the cycle.
    - If there is no cycle, the hare will reach the end of the list.
      > If the hare and tortoise meet at some point during the traversal, it means there is a cycle in the linked list, and the function returns true. If the hare reaches the end of the list without meeting the tortoise, there is no cycle, and the function returns false.

     </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/linked-list-cycle/)

31. ### ❓ **_Linked List Cycle II:-_** Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null. There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter. Do not modify the linked list.

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: head = [3,2,0,-4], pos = 1
    Output: tail connects to node index 1
    Explanation: There is a cycle in the linked list, where tail connects to the second node.

    Example 2:
    Input: head = [1,2], pos = 0
    Output: tail connects to node index 0
    Explanation: There is a cycle in the linked list, where tail connects to the first node.

    Example 3:
    Input: head = [1], pos = -1
    Output: no cycle
    Explanation: There is no cycle in the linked list.
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    function detectCycle(head) {
      let slow = head;
      let fast = head;

      // Detect the cycle
      while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;

        if (slow === fast) {
          // Cycle detected, break the loop
          break;
        }
      }

      // If fast reached the end of the list, no cycle
      if (!fast || !fast.next) {
        return null;
      }

      // Move slow back to the head
      slow = head;

      // Move both slow and fast one step at a time until they meet
      while (slow !== fast) {
        slow = slow.next;
        fast = fast.next;
      }

      // The meeting point is the start of the cycle
      return slow;
    }
    ```

    **In this algorithm:**

    - The tortoise and hare pointers are used to detect the cycle. If there is a cycle, they will eventually meet at some point within the cycle.
    - After detecting the cycle, the tortoise is moved back to the head, and both pointers move one step at a time until they meet again. The meeting point is the start of the cycle.
    - If there is no cycle, the function returns null. If there is a cycle, it returns the node where the cycle begins.

     </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/linked-list-cycle-ii/)

32. ### ❓ **_Remove Nth Node From End of List:-_** Given the head of a linked list, remove the nth node from the end of the list and return its head.

     <details>
     <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: head = [1,2,3,4,5], n = 2
    Output: [1,2,3,5]

    Example 2:
    Input: head = [1], n = 1
    Output: []

    Example 3:
    Input: head = [1,2], n = 1
    Output: [1]
    ```

     </details>

     <details>
     <summary>Solutions 👉</summary>

    ```js
    function removeNthFromEnd(head, n) {
      // Create a dummy node to simplify edge cases
      const dummy = new ListNode(0);
      dummy.next = head;

      let first = dummy;
      let second = dummy;

      // Move the second pointer n+1 steps ahead
      for (let i = 0; i <= n; i++) {
        second = second.next;
      }

      // Move both pointers until the second pointer reaches the end
      while (second !== null) {
        first = first.next;
        second = second.next;
      }

      // Remove the nth node from the end
      first.next = first.next.next;

      return dummy.next;
    }
    ```

    **In this algorithm:**

    - We use two pointers, first and second, initially pointing to the dummy node.
    - We move the second pointer n+1 steps ahead.
    - We move both pointers simultaneously until the second pointer reaches the end of the list.
    - At this point, the first pointer is pointing to the node just before the nth node from the end.
    - We remove the nth node by updating the next pointer of the first node.
      > This algorithm has a time complexity of O(n), where n is the length of the linked list, and a space complexity of O(1).

     </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

33. ### ❓ **_Copy List with Random Pointer:-_** A linked list of length n is given such that each node contains an additional random pointer, which could point to any node in the list, or null. Construct a deep copy of the list. The deep copy should consist of exactly n brand new nodes, where each new node has its value set to the value of its corresponding original node. Both the next and random pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. None of the pointers in the new list should point to nodes in the original list.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
    Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]

    Example 2:
    Input: head = [[1,1],[2,1]]
    Output: [[1,1],[2,1]]

    Example 3:
    Input: head = [[3,null],[3,0],[3,null]]
    Output: [[3,null],[3,0],[3,null]]
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    //Time O(n) | Space O(1)
    function copyRandomList(head) {
      if (!head) {
        return null;
      }

      // Step 1: Insert new nodes next to the original nodes
      let current = head;
      while (current) {
        const newNode = new Node(current.val);
        newNode.next = current.next;
        current.next = newNode;
        current = newNode.next;
      }

      // Step 2: Set random pointers for the new nodes
      current = head;
      while (current) {
        if (current.random) {
          current.next.random = current.random.next;
        }
        current = current.next.next;
      }

      // Step 3: Separate the combined list into two lists
      const newHead = head.next;
      let original = head;
      let copied = newHead;

      while (original) {
        original.next = original.next ? original.next.next : null;
        copied.next = copied.next ? copied.next.next : null;
        original = original.next;
        copied = copied.next;
      }

      return newHead;
    }

    // --------------------------------------------------------------

    //////////////////////////////////
    // HashMap and Recursive Approach
    // Time O(n) | Space O(n)
    //////////////////////////////////
    function copyRandomList(head, map = new Map()) {
      if (!head) return null;
      if (map.has(head)) return map.get(head);

      const clone = new Node(head.val);

      map.set(head, clone);
      clone.next = copyRandomList(head.next, map);
      clone.random = copyRandomList(head.random, map);

      return clone;
    }
    ```

    To deep copy a linked list with random pointers, you can follow these steps:

    - Iterate through the original linked list and create a new node for each node in the original list. Insert the new node next to its corresponding original node.
    - Iterate again through the combined list (original and new nodes) to set the random pointers for the new nodes based on the random pointers of the original nodes.
    - Separate the combined list into two separate lists: the original list and the copied list.

      > This algorithm has a time complexity of O(n) where n is the number of nodes in the linked list, and it uses only constant extra space.

      </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/copy-list-with-random-pointer/)

34. ### ❓ **_Add Two Numbers:-_** You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list. You may assume the two numbers do not contain any leading zero, except the number 0 itself.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: l1 = [2,4,3], l2 = [5,6,4]
    Output: [7,0,8]
    Explanation: 342 + 465 = 807.

    Example 2:
    Input: l1 = [0], l2 = [0]
    Output: [0]

    Example 3:
    Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
    Output: [8,9,9,9,0,0,0,1]
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    function addTwoNumbers(l1, l2) {
      const dummy = new ListNode(0);
      let current = dummy;
      let carry = 0;

      while (l1 || l2) {
        const x = l1 ? l1.val : 0;
        const y = l2 ? l2.val : 0;
        const sum = x + y + carry;

        carry = Math.floor(sum / 10);
        current.next = new ListNode(sum % 10);
        current = current.next;

        if (l1) l1 = l1.next;
        if (l2) l2 = l2.next;
      }

      if (carry > 0) {
        current.next = new ListNode(carry);
      }

      return dummy.next;
    }
    ```

    **Steps**

    - Initialize a dummy node to keep track of the head of the result linked list.
    - Initialize a carry variable to handle cases where the sum of two digits results in a carry.
    - Traverse both linked lists simultaneously, adding corresponding digits along with the carry.
    - If one linked list is longer than the other, consider it in the addition.
    - Update the carry for the next iteration.
    - Create a new node with the sum of digits (considering the carry) and update the result linked list.
    - Move to the next nodes in both linked lists.
    - After the traversal, if there is a carry left, create a new node with the carry and append it to the result linked list.
    - Return the head of the result linked list.

      </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/copy-list-with-random-pointer/)

35. ### ❓ **_Find the Duplicate Number:-_** Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive. There is only one repeated number in nums, return this repeated number. You must solve the problem without modifying the array nums and uses only constant extra space.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: nums = [1,3,4,2,2]
    Output: 2

    Example 2:
    Input: nums = [3,1,3,4,2]
    Output: 3
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    function findDuplicate(nums) {
      let slow = nums[0];
      let fast = nums[0];

      // Phase 1: Find the meeting point in the cycle
      do {
        slow = nums[slow];
        fast = nums[nums[fast]];
      } while (slow !== fast);

      // Phase 2: Find the entrance to the cycle
      slow = nums[0];
      while (slow !== fast) {
        slow = nums[slow];
        fast = nums[fast];
      }

      // The meeting point is the entrance to the cycle
      return slow;
    }
    ```

    > To solve this problem without modifying the array and using constant extra space, you can apply the Floyd's Tortoise and Hare algorithm (Cycle Detection algorithm) to find the cycle in a linked list. Here, we consider the array as a linked list where the indices represent nodes and the values at those indices represent the next nodes.

    **The steps are as follows:**

    - Initialize two pointers, slow and fast, both starting at the first element (index 0).
    - Move slow one step at a time and fast two steps at a time until they meet in the cycle.
    - Reset one pointer (either slow or fast) to the start (index 0) and move both pointers one step at a time until they meet again. The meeting point is the entrance of the cycle.
    - The value at the meeting point is the repeated number.

      > This algorithm has a time complexity of O(n) and a space complexity of O(1), meeting the requirements of not modifying the array and using constant extra space.

        </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/find-the-duplicate-number/)

36. ### ❓ **_LRU Cache:-_** Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

    ```smart
    Implement the LRUCache class:

    - LRUCache(int capacity) Initialize the LRU cache with positive size capacity.
    - int get(int key) Return the value of the key if the key exists, otherwise return -1.
    - void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.

    The functions get and put must each run in O(1) average time complexity.
    ```

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input
    ["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
    [[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
    Output
    [null, null, null, 1, null, -1, null, -1, 3, 4]

    Explanation
    LRUCache lRUCache = new LRUCache(2);
    lRUCache.put(1, 1); // cache is {1=1}
    lRUCache.put(2, 2); // cache is {1=1, 2=2}
    lRUCache.get(1);    // return 1
    lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
    lRUCache.get(2);    // returns -1 (not found)
    lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
    lRUCache.get(1);    // return -1 (not found)
    lRUCache.get(3);    // return 3
    lRUCache.get(4);    // return 4
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    class ListNode {
      constructor(key, value) {
        this.key = key;
        this.value = value;
        this.prev = null;
        this.next = null;
      }
    }

    class LRUCache {
      constructor(capacity) {
        this.capacity = capacity;
        this.size = 0;
        this.cache = new Map();
        this.head = new ListNode(); // Dummy head
        this.tail = new ListNode(); // Dummy tail
        this.head.next = this.tail;
        this.tail.prev = this.head;
      }

      moveToHead(node) {
        // Remove the node from its current position
        this.removeNode(node);
        // Move the node to the front (next to dummy head)
        this.addToHead(node);
      }

      addToHead(node) {
        node.next = this.head.next;
        node.prev = this.head;
        this.head.next.prev = node;
        this.head.next = node;
      }

      removeNode(node) {
        const prevNode = node.prev;
        const nextNode = node.next;
        prevNode.next = nextNode;
        nextNode.prev = prevNode;
      }

      removeTail() {
        const tailNode = this.tail.prev;
        this.removeNode(tailNode);
        return tailNode;
      }

      get(key) {
        if (this.cache.has(key)) {
          const node = this.cache.get(key);
          this.moveToHead(node);
          return node.value;
        }
        return -1;
      }

      put(key, value) {
        if (this.cache.has(key)) {
          const node = this.cache.get(key);
          node.value = value;
          this.moveToHead(node);
        } else {
          if (this.size === this.capacity) {
            const tailNode = this.removeTail();
            this.cache.delete(tailNode.key);
            this.size--;
          }

          const newNode = new ListNode(key, value);
          this.cache.set(key, newNode);
          this.addToHead(newNode);
          this.size++;
        }
      }
    }

    // Example usage:
    const lruCache = new LRUCache(2);
    lruCache.put(1, 1);
    lruCache.put(2, 2);
    console.log(lruCache.get(1)); // Output: 1
    lruCache.put(3, 3); // Evicts key 2
    console.log(lruCache.get(2)); // Output: -1 (not found)
    lruCache.put(4, 4); // Evicts key 1
    console.log(lruCache.get(1)); // Output: -1 (not found)
    console.log(lruCache.get(3)); // Output: 3
    console.log(lruCache.get(4)); // Output: 4
    ```

    > To implement a Least Recently Used (LRU) cache, you can use a combination of a doubly linked list and a hash map. The doubly linked list helps maintain the order of recently used items, and the hash map provides quick access to items based on their keys.

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/lru-cache/)

37. ### ❓ **_LFU Cache:-_** Design and implement a data structure for a Least Frequently Used (LFU) cache.

    ```smart
    Implement the LFUCache class:

    - LFUCache(int capacity) Initializes the object with the capacity of the data structure.
    - int get(int key) Gets the value of the key if the key exists in the cache. Otherwise, returns -1.
    - void put(int key, int value) Update the value of the key if present, or inserts the key if not already present. When the cache reaches its capacity, it should invalidate and remove the least frequently used key before inserting a new item. For this problem, when there is a tie (i.e., two or more keys with the same frequency), the least recently used key would be invalidated.

    To determine the least frequently used key, a use counter is maintained for each key in the cache. The key with the smallest use counter is the least frequently used key.

    When a key is first inserted into the cache, its use counter is set to 1 (due to the put operation). The use counter for a key in the cache is incremented either a get or put operation is called on it.

    The functions get and put must each run in O(1) average time complexity.
    ```

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input
    ["LFUCache", "put", "put", "get", "put", "get", "get", "put", "get", "get", "get"]
    [[2], [1, 1], [2, 2], [1], [3, 3], [2], [3], [4, 4], [1], [3], [4]]
    Output
    [null, null, null, 1, null, -1, 3, null, -1, 3, 4]

    Explanation
    // cnt(x) = the use counter for key x
    // cache=[] will show the last used order for tiebreakers (leftmost element is  most recent)
    LFUCache lfu = new LFUCache(2);
    lfu.put(1, 1);   // cache=[1,_], cnt(1)=1
    lfu.put(2, 2);   // cache=[2,1], cnt(2)=1, cnt(1)=1
    lfu.get(1);      // return 1
                    // cache=[1,2], cnt(2)=1, cnt(1)=2
    lfu.put(3, 3);   // 2 is the LFU key because cnt(2)=1 is the smallest, invalidate 2.
                    // cache=[3,1], cnt(3)=1, cnt(1)=2
    lfu.get(2);      // return -1 (not found)
    lfu.get(3);      // return 3
                    // cache=[3,1], cnt(3)=2, cnt(1)=2
    lfu.put(4, 4);   // Both 1 and 3 have the same cnt, but 1 is LRU, invalidate 1.
                    // cache=[4,3], cnt(4)=1, cnt(3)=2
    lfu.get(1);      // return -1 (not found)
    lfu.get(3);      // return 3
                    // cache=[3,4], cnt(4)=1, cnt(3)=3
    lfu.get(4);      // return 4
                    // cache=[4,3], cnt(4)=2, cnt(3)=3
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    class Node {
      constructor(key, value) {
        this.key = key;
        this.value = value;
        this.frequency = 1;
        this.prev = null;
        this.next = null;
      }
    }

    class LFUCache {
      constructor(capacity) {
        this.capacity = capacity;
        this.keyToNode = new Map();
        this.frequencyToBucket = new Map();
        this.minFrequency = 1;
      }

      moveToNextFrequency(node) {
        this.removeFromBucket(node);
        node.frequency += 1;
        this.addToBucket(node);
        this.updateMinFrequency(node.frequency);
      }

      addToBucket(node) {
        const frequency = node.frequency;
        if (!this.frequencyToBucket.has(frequency)) {
          this.frequencyToBucket.set(frequency, new DoublyLinkedList());
        }
        this.frequencyToBucket.get(frequency).addToHead(node);
      }

      removeFromBucket(node) {
        const frequency = node.frequency;
        const bucket = this.frequencyToBucket.get(frequency);
        bucket.remove(node);
        if (bucket.isEmpty()) {
          this.frequencyToBucket.delete(frequency);
          if (this.minFrequency === frequency) {
            this.minFrequency += 1;
          }
        }
      }

      updateMinFrequency(newFrequency) {
        if (this.minFrequency > newFrequency) {
          this.minFrequency = newFrequency;
        }
      }

      removeLeastFrequent() {
        const leastFrequentBucket = this.frequencyToBucket.get(
          this.minFrequency
        );
        const toRemove = leastFrequentBucket.removeFromTail();
        this.keyToNode.delete(toRemove.key);
      }

      get(key) {
        if (!this.keyToNode.has(key)) {
          return -1;
        }

        const node = this.keyToNode.get(key);
        this.moveToNextFrequency(node);
        return node.value;
      }

      put(key, value) {
        if (this.capacity === 0) {
          return;
        }

        if (this.keyToNode.has(key)) {
          const node = this.keyToNode.get(key);
          node.value = value;
          this.moveToNextFrequency(node);
        } else {
          const newNode = new Node(key, value);
          if (this.keyToNode.size >= this.capacity) {
            this.removeLeastFrequent();
          }

          this.keyToNode.set(key, newNode);
          this.addToBucket(newNode);
          this.updateMinFrequency(newNode.frequency);
        }
      }
    }

    class DoublyLinkedList {
      constructor() {
        this.head = new Node(null, null);
        this.tail = new Node(null, null);
        this.head.next = this.tail;
        this.tail.prev = this.head;
      }

      addToHead(node) {
        node.next = this.head.next;
        node.prev = this.head;
        this.head.next.prev = node;
        this.head.next = node;
      }

      removeFromTail() {
        const toRemove = this.tail.prev;
        this.remove(toRemove);
        return toRemove;
      }

      remove(node) {
        const prevNode = node.prev;
        const nextNode = node.next;
        prevNode.next = nextNode;
        nextNode.prev = prevNode;
      }

      isEmpty() {
        return this.head.next === this.tail;
      }
    }

    // Example Usage:
    const lfuCache = new LFUCache(2);
    lfuCache.put(1, 1);
    lfuCache.put(2, 2);
    console.log(lfuCache.get(1)); // Output: 1
    lfuCache.put(3, 3); // evicts key 2
    console.log(lfuCache.get(2)); // Output: -1 (not found)
    console.log(lfuCache.get(3)); // Output: 3
    ```

    > This implementation includes the LFUCache class, Node class, and DoublyLinkedList class. The LFUCache uses a combination of a hash map (keyToNode) and a frequency-based doubly linked list (frequencyToBucket) to efficiently manage the cache. The example usage demonstrates the basic operations of putting and getting items from the LFUCache.

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/lfu-cache/)

38. ### ❓ **_Most Recently Used (MRU) Queue:-_** Design and implement a data structure for Most Recently Used (MRU) Queue.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    // Example Usage:
    const mruQueue = new MRUQueue(5);
    mruQueue.add(1);
    mruQueue.add(2);
    mruQueue.add(3);
    mruQueue.print(); // Output: 3 2 1

    mruQueue.fetch(2);
    mruQueue.print(); // Output: 2 3 1

    mruQueue.add(4);
    mruQueue.add(5);
    mruQueue.add(6);
    mruQueue.print(); // Output: 6 5 4 2 3
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    class Node {
      constructor(value) {
        this.value = value;
        this.prev = null;
        this.next = null;
      }
    }

    class MRUQueue {
      constructor(size) {
        this.size = size;
        this.head = null;
        this.tail = null;
        this.nodeMap = new Map(); // Map to store nodes by their values
      }

      fetch(k) {
        if (this.nodeMap.has(k)) {
          const node = this.nodeMap.get(k);
          this.moveToFront(node);
          return true;
        }
        return false;
      }

      add(k) {
        if (this.nodeMap.has(k)) {
          // If the element already exists, move it to the front
          const node = this.nodeMap.get(k);
          this.moveToFront(node);
        } else {
          // Add a new element to the front
          const newNode = new Node(k);
          this.nodeMap.set(k, newNode);
          this.addToFront(newNode);

          // Check if the size exceeds the specified limit, and remove the least recently used element if needed
          if (this.nodeMap.size > this.size) {
            const removedNode = this.removeFromEnd();
            this.nodeMap.delete(removedNode.value);
          }
        }
      }

      moveToFront(node) {
        if (node !== this.head) {
          // Remove the node from its current position
          node.prev.next = node.next;
          if (node.next) {
            node.next.prev = node.prev;
          } else {
            this.tail = node.prev;
          }

          // Add the node to the front
          node.next = this.head;
          node.prev = null;
          this.head.prev = node;
          this.head = node;
        }
      }

      addToFront(node) {
        if (!this.head) {
          this.head = node;
          this.tail = node;
        } else {
          node.next = this.head;
          this.head.prev = node;
          this.head = node;
        }
      }

      removeFromEnd() {
        if (!this.tail) {
          return null;
        }

        const removedNode = this.tail;
        this.tail = this.tail.prev;

        if (this.tail) {
          this.tail.next = null;
        } else {
          this.head = null;
        }

        return removedNode;
      }

      print() {
        let current = this.head;
        while (current) {
          console.log(current.value);
          current = current.next;
        }
      }
    }

    // Example Usage:
    const mruQueue = new MRUQueue(5);
    mruQueue.add(1);
    mruQueue.add(2);
    mruQueue.add(3);
    mruQueue.print(); // Output: 3 2 1

    mruQueue.fetch(2);
    mruQueue.print(); // Output: 2 3 1

    mruQueue.add(4);
    mruQueue.add(5);
    mruQueue.add(6);
    mruQueue.print(); // Output: 6 5 4 2 3
    ```

    > This implementation uses a doubly linked list to maintain the order of elements and a map to quickly retrieve nodes based on their values. The fetch method moves an element to the front when accessed, and the add method adds a new element to the front while handling the size constraint. The print method is included for demonstration purposes.

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/design-most-recently-used-queue/)

39. ### ❓ **_Merge k Sorted Lists:-_** You are given an array of k linked-lists lists, each linked-list is sorted in ascending order. Merge all the linked-lists into one sorted linked-list and return it.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: lists = [[1,4,5],[1,3,4],[2,6]]
    Output: [1,1,2,3,4,4,5,6]
    Explanation: The linked-lists are:
    [
      1->4->5,
      1->3->4,
      2->6
    ]
    merging them into one sorted list:
    1->1->2->3->4->4->5->6

    Example 2:
    Input: lists = []
    Output: []

    Example 3:
    Input: lists = [[]]
    Output: []
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    // Time O(N) | Space O(N)
    function mergeKLists(lists) {
      let previous = null;

      for (let i = 0; i < lists.length; i++) {
        previous = mergeTwoLists(previous, lists[i]);
      }

      return previous;
    }

    function mergeTwoLists(list1, list2) {
      let sentinel = (tail = new ListNode(0));

      while (list1 && list2) {
        const canAddL1 = list1.val <= list2.val;
        if (canAddL1) {
          tail.next = list1;
          list1 = list1.next;
        } else {
          tail.next = list2;
          list2 = list2.next;
        }

        tail = tail.next;
      }

      tail.next = list1 || list2;

      return sentinel.next;
    }
    ```

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/merge-k-sorted-lists/)

40. ### ❓ **_Reverse Nodes in k-Group:-_** Given the head of a linked list, reverse the nodes of the list `k` at a time, and return the modified list. `k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is. You may not alter the values in the list's nodes, only nodes themselves may be changed.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: head = [1,2,3,4,5], k = 2
    Output: [2,1,4,3,5]

    Example 2:
    Input: head = [1,2,3,4,5], k = 3
    Output: [3,2,1,4,5]
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    //  Time O(N) | Space O(N)
    class ListNode {
      constructor(val, next) {
        this.val = val;
        this.next = next;
      }
    }

    const reverseKGroup = (head, k) => {
      const sentinel = new ListNode(0, head);
      let tail = sentinel;

      while (true) {
        let [start, last] = moveNode(tail, k);
        if (!last) break;

        reverse([start, tail.next, start]);

        const next = tail.next;
        tail.next = last;
        tail = next;
      }

      return sentinel.next;
    };

    const moveNode = (curr, k) => {
      const canMove = () => k && curr;
      while (canMove()) {
        curr = curr.next;
        k--;
      }

      return [curr?.next || null, curr];
    };

    const reverse = ([prev, curr, start]) => {
      const isSame = () => curr === start;
      while (!isSame()) {
        const next = curr.next;
        curr.next = prev;

        prev = curr;
        curr = next;
      }
    };

    const result = reverseKGroup(
      new ListNode(
        1,
        new ListNode(2, new ListNode(3, new ListNode(4, new ListNode(5))))
      ),
      2
    );

    console.log(result); // [2, 1, 4, 3, 5]
    ```

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/reverse-nodes-in-k-group/)

41. ### ❓ **_Swap Nodes in Pairs:-_** Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: head = [1,2,3,4]
    Output: [2,1,4,3]

    Example 2:
    Input: head = []
    Output: []

    Example 3:
    Input: head = [1]
    Output: [1]
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    class ListNode {
      constructor(val, next = null) {
        this.val = val;
        this.next = next;
      }
    }

    const swapPairs = function (head) {
      const dummy = new ListNode(0);
      dummy.next = head;
      let current = dummy;

      while (current.next && current.next.next) {
        const first = current.next;
        const second = current.next.next;

        // Swap the pairs
        first.next = second.next;
        second.next = first;
        current.next = second;

        // Move to the next pair
        current = first;
      }

      return dummy.next;
    };

    // Example linked list: 1 -> 2 -> 3 -> 4
    const head = new ListNode(
      1,
      new ListNode(2, new ListNode(3, new ListNode(4)))
    );

    const swappedHead = swapPairs(head);

    // The result will be: 2 -> 1 -> 4 -> 3
    ```

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/swap-nodes-in-pairs/)

42. ### ❓ **_Swapping Nodes in a Linked List:-_** You are given the head of a linked list, and an integer k. Return the head of the linked list after swapping the values of the kth node from the beginning and the kth node from the end (the list is 1-indexed).

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: head = [1,2,3,4,5], k = 2
    Output: [1,4,3,2,5]

    Example 2:
    Input: head = [7,9,6,6,7,8,3,0,9,5], k = 5
    Output: [7,9,6,6,8,7,3,0,9,5]
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    class ListNode {
      constructor(val, next = null) {
        this.val = val;
        this.next = next;
      }
    }

    const swapNodes = function (head, k) {
      let length = 0;
      let current = head;

      // Find the length of the linked list
      while (current) {
        length++;
        current = current.next;
      }

      // Find the kth node from the beginning
      let first = head;
      for (let i = 1; i < k; i++) {
        first = first.next;
      }

      // Find the kth node from the end
      let second = head;
      for (let i = 0; i < length - k; i++) {
        second = second.next;
      }

      // Swap their values
      const temp = first.val;
      first.val = second.val;
      second.val = temp;

      return head;
    };

    // Example linked list: 1 -> 2 -> 3 -> 4 -> 5
    const head = new ListNode(
      1,
      new ListNode(2, new ListNode(3, new ListNode(4, new ListNode(5))))
    );

    const k = 2;
    const result = swapNodes(head, k);

    // The result will be: 1 -> 4 -> 3 -> 2 -> 5
    ```

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/)

<br>

[🔼 Back to top](#table-of-contents)

 <!------------------
     Trees Start
 ------------------->

## Trees

43. ### ❓ **_Invert Binary Tree:-_** Given the root of a binary tree, invert the tree, and return its root.

    > To invert a binary tree, you can perform a simple depth-first traversal (pre-order, in-order, or post-order) and swap the left and right children at each node. Here's a

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: root = [4,2,7,1,3,6,9]
    Output: [4,7,2,9,6,3,1]

    Example 2:
    Input: root = [2,1,3]
    Output: [2,3,1]

    Example 3:
    Input: root = []
    Output: []
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    class TreeNode {
      constructor(val, left = null, right = null) {
        this.val = val;
        this.left = left;
        this.right = right;
      }
    }

    // Depth First Search
    // Time O(N) | Space O(N)
    const invertTree = function (root) {
      // Base case: If the current node is null, return null
      if (!root) {
        return null;
      }

      // Swap the left and right children
      const temp = root.left;
      root.left = root.right;
      root.right = temp;

      // Recursively invert the left and right subtrees
      invertTree(root.left);
      invertTree(root.right);

      return root;
    };

    // Example binary tree:
    //        1
    //       / \
    //      2   3
    //     / \ / \
    //    4  5 6  7
    const root = new TreeNode(
      1,
      new TreeNode(2, new TreeNode(4), new TreeNode(5)),
      new TreeNode(3, new TreeNode(6), new TreeNode(7))
    );

    const invertedRoot = invertTree(root);

    // The inverted tree will be:
    //        1
    //       / \
    //      3   2
    //     / \ / \
    //    7  6 5  4

    //////////////////////////////////////////

    ////////////////////////////
    // Breadth First Search
    // Time O(N) | Space O(N)
    /////////////////////////////
    const invertTree = function (root) {
      if (!root) {
        return null;
      }

      const queue = [root];

      while (queue.length > 0) {
        const currentNode = queue.shift();

        // Swap left and right children
        const temp = currentNode.left;
        currentNode.left = currentNode.right;
        currentNode.right = temp;

        if (currentNode.left) {
          queue.push(currentNode.left);
        }

        if (currentNode.right) {
          queue.push(currentNode.right);
        }
      }

      return root;
    };
    ```

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/invert-binary-tree/)

44. ### ❓ **_Maximum Depth of Binary Tree:-_** Given the root of a binary tree, return its maximum depth. A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: root = [3,9,20,null,null,15,7]
    Output: 3

    Example 2:
    Input: root = [1,null,2]
    Output: 2
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    class TreeNode {
      constructor(val, left = null, right = null) {
        this.val = val;
        this.left = left;
        this.right = right;
      }
    }

    /////////////////////////
    // Depth First Search
    // Time O(N) | Space O(N)
    ////////////////////////
    const maxDepth = function (root) {
      // Base case: If the current node is null, the depth is 0
      if (!root) {
        return 0;
      }

      // Recursively calculate the depth of the left and right subtrees
      const leftDepth = maxDepth(root.left);
      const rightDepth = maxDepth(root.right);

      // The depth of the current subtree is the maximum depth of its left and right subtrees, plus 1 for the current node
      return Math.max(leftDepth, rightDepth) + 1;
    };

    // Example binary tree:
    //        3
    //       / \
    //      9  20
    //        /  \
    //       15   7
    const root = new TreeNode(
      3,
      new TreeNode(9),
      new TreeNode(20, new TreeNode(15), new TreeNode(7))
    );

    const depth = maxDepth(root);
    console.log(depth); // Output: 3

    //////////////////////////////////////////////////////////////////////

    ////////////////////////
    // Breadth First Search
    // Level of Order
    // Time O(N) | Space O(N)
    ////////////////////////
    const maxDepthBFS = function (root) {
      if (!root) {
        return 0;
      }

      const queue = [root];
      let depth = 0;

      while (queue.length > 0) {
        const levelSize = queue.length;

        for (let i = 0; i < levelSize; i++) {
          const currentNode = queue.shift();

          if (currentNode.left) {
            queue.push(currentNode.left);
          }

          if (currentNode.right) {
            queue.push(currentNode.right);
          }
        }

        depth++;
      }

      return depth;
    };
    ```

    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

45. ### ❓ **_Minimum Depth of Binary Tree:-_** Given a binary tree, find its minimum depth. The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node. Note: A leaf is a node with no children.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: root = [3,9,20,null,null,15,7]
    Output: 2

    Example 2:
    Input: root = [2,null,3,null,4,null,5,null,6]
    Output: 5
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    ////////////////////////
    // Breadth First Search
    // Level of Order
    // Time O(N) | Space O(N)
    ////////////////////////
    const minDepth = function (root) {
      if (!root) {
        return 0;
      }

      const queue = [root];
      let depth = 1;

      while (queue.length > 0) {
        const levelSize = queue.length;

        for (let i = 0; i < levelSize; i++) {
          const currentNode = queue.shift();

          if (!currentNode.left && !currentNode.right) {
            // We found the first leaf node, return the current depth
            return depth;
          }

          if (currentNode.left) {
            queue.push(currentNode.left);
          }

          if (currentNode.right) {
            queue.push(currentNode.right);
          }
        }

        depth++;
      }

      return depth;
    };

    /////////////////////////////////////////////////

    /////////////////////////
    // Depth First Search
    // Time O(N) | Space O(N)
    ////////////////////////
    const minDepth = function (root) {
      if (!root) {
        return 0;
      }

      if (!root.left && !root.right) {
        // If the node is a leaf, return 1
        return 1;
      }

      let minDepthValue = Number.POSITIVE_INFINITY;

      if (root.left) {
        minDepthValue = Math.min(minDepth(root.left), minDepthValue);
      }

      if (root.right) {
        minDepthValue = Math.min(minDepth(root.right), minDepthValue);
      }

      return minDepthValue + 1;
    };
    ```
    </details>
 
    [Original Problem in LeetCode](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

46. ### ❓ **_Diameter of Binary Tree:-_** Given the root of a binary tree, return the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root. The length of a path between two nodes is represented by the number of edges between them.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: root = [1,2,3,4,5]
    Output: 3
    Explanation: 3 is the length of the path [4,2,1,3] or [5,2,1,3].

    Example 2:
    Input: root = [1,2]
    Output: 1
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    ////////////////////////
    // Depth First Search
    // Time O(N) | Space O(N)
    ////////////////////////
    class TreeNode {
      constructor(val, left = null, right = null) {
        this.val = val;
        this.left = left;
        this.right = right;
      }
    }

    const diameterOfBinaryTree = function (root) {
      let diameter = 0;

      const depth = function (node) {
        if (!node) {
          return 0;
        }

        const leftDepth = depth(node.left);
        const rightDepth = depth(node.right);

        // Update the diameter with the sum of heights for each node
        diameter = Math.max(diameter, leftDepth + rightDepth);

        // Return the height of the subtree rooted at the current node
        return 1 + Math.max(leftDepth, rightDepth);
      };

      depth(root);
      return diameter;
    };

    // Example usage:
    // Binary tree:
    //        1
    //       / \
    //      2   3
    //     / \
    //    4   5
    const root = new TreeNode(
      1,
      new TreeNode(2, new TreeNode(4), new TreeNode(5)),
      new TreeNode(3)
    );

    const result = diameterOfBinaryTree(root);
    console.log(result); // Output: 3
    ```
    </details>

    [Original Problem in LeetCode](https://leetcode.com/problems/diameter-of-binary-tree/)

47. ### ❓ **_Balanced Binary Tree:-_** Given a binary tree, determine if it is height-balanced.

    > To determine if a binary tree is height-balanced, you need to check if the heights of the left and right subtrees of every node differ by no more than 1, and both subtrees are also balanced.

    <details>
    <summary>Examples 👉</summary>

    ```smart
    Example 1:
    Input: root = [3,9,20,null,null,15,7]
    Output: true

    Example 2:
    Input: root = [1,2,2,3,3,null,null,4,4]
    Output: false

    Example 3:
    Input: root = []
    Output: true
    ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

    ```js
    ////////////////////////
    // Depth First Search
    // Time O(N) | Space O(H)
    ////////////////////////
    class TreeNode {
      constructor(val) {
        this.val = val;
        this.left = this.right = null;
      }
    }

    function isBalanced(root) {
      if (!root) {
        return true; // An empty tree is always balanced
      }

      // Helper function to calculate the height of a tree
      const getHeight = (node) => {
        if (!node) {
          return 0;
        }

        const leftHeight = getHeight(node.left);
        const rightHeight = getHeight(node.right);

        // If at any node, the subtree is not balanced, return -1
        if (
          leftHeight === -1 ||
          rightHeight === -1 ||
          Math.abs(leftHeight - rightHeight) > 1
        ) {
          return -1;
        }

        // Return the height of the current subtree
        return Math.max(leftHeight, rightHeight) + 1;
      };

      // If the height of the tree is -1, it means the tree is not balanced
      return getHeight(root) !== -1;
    }

    // Example usage:
    const root = new TreeNode(1);
    root.left = new TreeNode(2);
    root.right = new TreeNode(3);
    root.left.left = new TreeNode(4);
    root.left.right = new TreeNode(5);
    root.right.right = new TreeNode(6);

    console.log(isBalanced(root)); // Output: false
    ```
    
    > This code defines a TreeNode class representing a node in the binary tree and a function isBalanced to check if the tree is height-balanced. The getHeight helper function calculates the height of the subtree rooted at a given node and checks for balance conditions.

    </details>
  
    [Original Problem in LeetCode](https://leetcode.com/problems/balanced-binary-tree/)

<br>

[🔼 Back to top](#table-of-contents)

 <!------------------
     Trees End
 ------------------->

 <!------------------
 Design System Start
 ------------------->

## Design System

- ### [❓ **_LRU Cache:-_** Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.](#❓-lru-cache--design-a-data-structure-that-follows-the-constraints-of-a-least-recently-used-lru-cache)

- ### [❓ **_LFU Cache:-_** Design and implement a data structure for a Least Frequently Used (LFU) cache.](#❓-lfu-cache--design-and-implement-a-data-structure-for-a-least-frequently-used-lfu-cache)

- ### [❓ **_Most Recently Used (MRU) Queue:-_** Design and implement a data structure for Most Recently Used (MRU) Queue.](#❓-most-recently-used-mru-queue--design-and-implement-a-data-structure-for-most-recently-used-mru-queue)

- ### ❓ **_Design In-Memory File System:-_** Design and implement a data structure for a In-Memory File System.

    <details>
    <summary>Examples 👉</summary>

  ```smart
  // Example Usage:
  const fileSystem = new FileSystem();
  console.log(fileSystem.ls('/')); // Output: []
  fileSystem.mkdir('/a/b/c');
  fileSystem.addContentToFile('/a/b/c/d', 'hello');
  console.log(fileSystem.ls('/')); // Output: ['a']
  console.log(fileSystem.ls('/a/b')); // Output: ['c']
  console.log(fileSystem.ls('/a/b/c')); // Output: ['d']
  console.log(fileSystem.readContentFromFile('/a/b/c/d')); // Output: 'hello'
  ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

  ```js
  class File {
    constructor(isDirectory = false) {
      this.isDirectory = isDirectory;
      this.children = new Map();
      this.content = "";
    }
  }

  class FileSystem {
    constructor() {
      this.root = new File(true);
    }

    separatePath(path) {
      return path.split("/").filter((part) => part !== "");
    }

    ls(path) {
      const parts = this.separatePath(path);
      let current = this.root;

      for (const part of parts) {
        current = current.children.get(part);
      }

      if (current.isDirectory) {
        return [...current.children.keys()].sort();
      } else {
        return [parts[parts.length - 1]];
      }
    }

    mkdir(path) {
      const parts = this.separatePath(path);
      let current = this.root;

      for (const part of parts) {
        if (!current.children.has(part)) {
          current.children.set(part, new File(true));
        }
        current = current.children.get(part);
      }
    }

    addContentToFile(filePath, content) {
      const parts = this.separatePath(filePath);
      let current = this.root;

      for (const part of parts.slice(0, -1)) {
        if (!current.children.has(part)) {
          current.children.set(part, new File(true));
        }
        current = current.children.get(part);
      }

      const fileName = parts[parts.length - 1];
      if (!current.children.has(fileName)) {
        current.children.set(fileName, new File());
      }

      current = current.children.get(fileName);
      current.content += content;
    }

    readContentFromFile(filePath) {
      const parts = this.separatePath(filePath);
      let current = this.root;

      for (const part of parts) {
        current = current.children.get(part);
      }

      return current.content;
    }
  }

  // Example Usage:
  const fileSystem = new FileSystem();
  console.log(fileSystem.ls("/")); // Output: []
  fileSystem.mkdir("/a/b/c");
  fileSystem.addContentToFile("/a/b/c/d", "hello");
  console.log(fileSystem.ls("/")); // Output: ['a']
  console.log(fileSystem.ls("/a/b")); // Output: ['c']
  console.log(fileSystem.ls("/a/b/c")); // Output: ['d']
  console.log(fileSystem.readContentFromFile("/a/b/c/d")); // Output: 'hello'
  ```

  > This implementation uses a tree structure to represent the file system. The File class represents a file or directory, and the FileSystem class provides methods for the required operations. The example usage demonstrates creating directories, adding content to files, and listing the contents of directories.

    </details>

  [Original Problem in LeetCode](https://leetcode.com/problems/design-in-memory-file-system/)

<br>

[🔼 Back to top](#table-of-contents)

 <!------------------
 Design System Ends
 ------------------->

## Misc

- ### ❓ **_Encode and Decode TinyURL:-_** TinyURL is a URL shortening service where you enter a URL such as https://leetcode.com/problems/design-tinyurl and it returns a short URL such as http://tinyurl.com/4e9iAk. Design a class to encode a URL and decode a tiny URL.

    <details>
    <summary>Examples 👉</summary>

  ```smart
  Example 1:
  Input: url = "https://leetcode.com/problems/design-tinyurl"
  Output: "https://leetcode.com/problems/design-tinyurl"

  Explanation:
  Solution obj = new Solution();
  string tiny = obj.encode(url); // returns the encoded tiny url.
  string ans = obj.decode(tiny); // returns the original url after decoding it.
  ```

    </details>

    <details>
    <summary>Solutions 👉</summary>

  ```js
  class Codec {
    constructor() {
      // Initialize an empty mapping to store longUrl to shortUrl and vice versa.
      this.urlMapping = new Map();
      // Define the base URL for the short URLs.
      this.baseUrl = "http://tinyurl.com/";
    }

    generateKey() {
      // Generate a random key for the short URL.
      const characters =
        "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
      let key = "";
      for (let i = 0; i < 6; i++) {
        key += characters.charAt(Math.floor(Math.random() * characters.length));
      }
      return key;
    }

    encode(longUrl) {
      // Check if the longUrl is already in the mapping.
      if (this.urlMapping.has(longUrl)) {
        return this.urlMapping.get(longUrl);
      }

      // Generate a new key and create the short URL.
      const key = this.generateKey();
      const shortUrl = this.baseUrl + key;

      // Store the mapping in both directions.
      this.urlMapping.set(longUrl, shortUrl);
      this.urlMapping.set(shortUrl, longUrl);

      return shortUrl;
    }

    decode(shortUrl) {
      // Return the original long URL from the mapping.
      return this.urlMapping.get(shortUrl) || "";
    }
  }

  // Example usage:
  const codec = new Codec();
  const longUrl = "https://leetcode.com/problems/design-tinyurl";
  const shortUrl = codec.encode(longUrl);
  console.log(shortUrl); // Output: http://tinyurl.com/abcdefgh
  const decodedUrl = codec.decode(shortUrl);
  console.log(decodedUrl); // Output: https://leetcode.com/problems/design-tinyurl
  ```

  > In this JavaScript implementation, the Codec class has encode and decode methods, similar to the Python implementation. The generateKey method generates a random key for the short URL. The mapping is stored using a Map object.

  > Note: This is a basic implementation, and in a real-world scenario, you might want to handle edge cases, ensure uniqueness of generated keys, and possibly persist the mapping in a database for durability across service restarts. Additionally, this implementation may not guarantee globally unique short URLs.

    </details>

  [Original Problem in LeetCode](https://leetcode.com/problems/encode-and-decode-tinyurl/)

<br>

[🔼 Back to top](#table-of-contents)

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
