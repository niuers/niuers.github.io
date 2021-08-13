---
title: "String Problems"
date: 2021-07-18
categories:
  - blog
tags:
  - algorithm
  - string
  - summary
---

1. Palindromes
    1. Check if a string is palindrome
        * Reverse the string and compare with the original string
        * Use two pointers from left and right, and compare each character along the way
    2. Find the longest palindromic substrings
        1. dynamic programming: `O(n^2)`
        2. Expand from center: for each position, expand for the cases of even/odd number of characters and find the longest palindrome. This is much faster than the dynamic programming solution even it's still `O(n^2)`
    7. Problems
        * [LC5. Longest Palindromic Substring][LC5. Longest Palindromic Substring]

2. ZigZag Conversion
    1. Use a combination of current row number and direction to record the string on each row
    2. Problems
        * [LC6. ZigZag Conversion][LC6. ZigZag Conversion]

3. Anagrams
    1. Two strings are anagrams if and only if their sorted strings are equal.
    2. Two strings are anagrams if and only if their character counts (respective number of occurrences of each character) are the same.
    3. The main issue is how to generate the key for the dictionary?
        1. Sort each string, and use the sorted string as key, `O(KlogK)`, where `K` is the string length
        2. Count the letters in each string, and put the counts in an array, convert the array into tuple, and use the tuple as key. `O(K)`
            * You can also use the array to generate a unique string as key, e.g. use `#` as separator or put count after each letter.
        3. Create a map from each character to a prime number (Godel's encoding), and compute the product of prime numbers corresponding to each letter in the string. `O(K)`
            ```
            primes = [2,3,5,7,11,13,17,19,23,29,31,37,41,43,47,53,59,61,67,71,73,79,83,89,97,101]
            hash_key = 1            
            for character in string:
                hash_key *= primes[ord(character)-ord('a')]
            ```
    4. Problems
        * [LC49. Group Anagrams][LC49. Group Anagrams]


4. Interleaving String
    1. Problems
        * [LC97. Interleaving String][LC97. Interleaving String]

5. Time complexity of string slice `s[i:j]` is `O(j-i+1)`

[LC5. Longest Palindromic Substring]: https://leetcode.com/problems/longest-palindromic-substring/
[LC6. ZigZag Conversion]: https://leetcode.com/problems/zigzag-conversion/
[LC49. Group Anagrams]: https://leetcode.com/problems/group-anagrams/
[LC97. Interleaving String]: https://leetcode.com/problems/interleaving-string/