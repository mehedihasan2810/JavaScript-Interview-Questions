# JavaScript Interview Questions

[Want to get a good grasp on **_DSA_** in JavaScript? Check out this doc.](https://github.com/mehedihasan2810/JavaScript-Data-Structures-and-Algorithms)

## Table Of Contents

- [NeetCode 150 Questions & Solutions](#neetcode-150-questions--solutions)
  - [Arrays & Hashing](#arrays--hashing)
  - [Two Pointers](#two-pointers)
  - [Stack](#stack)
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
