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

6. [Check if a string pattern matches an array of words][LC290. Word Pattern]
    1. Use a hashmap and a set
    2. Use a single hash map of indices for each pattern and word, and check if the indices match. 
        * N.B. This doesn't work if the word is single character. 
            * Example: pattern = "abba", words = "dog a a dog"
        * But it can be resolved using two hash maps.
        * Or add prefix for the keys, e.g. 'char_' and 'word_'

7. Encoding and decoding
    1. Chunked Transfer Encoding
        * Data stream is divided into chunks. Each chunk is preceded by its size in bytes.
        * For each chunk compute its length, and convert that length into 4-bytes string.
            * Encode a 32-bit integer to a 4-byte string
            ```
            def int_to_str(x):
                """
                Encodes integer to bytes string
                """
                #Convert each byte into a character
                bytes = [chr(x >> (i * 8) & 0xff) for i in range(4)]
                bytes.reverse()
                bytes_str = ''.join(bytes)
                return bytes_str            
            ```
        * Append to encoded string :
            * 4-bytes string with information about chunk size in bytes.
            * Chunk itself.
    2. Decoding
        * Read `4` bytes `s[i: i + 4]`. It's chunk size in bytes. Convert this 4-bytes string to integer length.
        ```
        def str_to_int(bytes_str):
            result = 0
            for ch in bytes_str:
                result = result * 256 + ord(ch)
            return result
        ```

8. [Remove Duplicate Letters][LC316. Remove Duplicate Letters]
    1. Use stack: this is similar to problem of [creating maximum number][Create Maximum Number]
    2. 


[LC5. Longest Palindromic Substring]: https://leetcode.com/problems/longest-palindromic-substring/
[LC6. ZigZag Conversion]: https://leetcode.com/problems/zigzag-conversion/
[LC49. Group Anagrams]: https://leetcode.com/problems/group-anagrams/
[LC97. Interleaving String]: https://leetcode.com/problems/interleaving-string/
[LC290. Word Pattern]: https://leetcode.com/problems/word-pattern/
[LC316. Remove Duplicate Letters]: https://leetcode.com/problems/remove-duplicate-letters/
[Create Maximum Number]: https://leetcode.com/problems/remove-duplicate-letters/discuss/76769/Java-solution-using-Stack-with-comments/80556
