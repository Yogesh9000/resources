# 4 common patters in two pointer problems

> [!NOTE] Need to revisit sliding window related problems, really struggling with them

## 1. Running from both ends of an array
- [x] https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
- [x] https://leetcode.com/problems/3sum/description/
- [x] https://leetcode.com/problems/4sum/description/
- [x] https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/
	-  utilized the binary exponentiation method to compute the value of 2^n % 1e9+7 in O(logn) computations
- [x] https://leetcode.com/problems/two-sum-iv-input-is-a-bst/
	- I implemented the O(n) time and space complexity solution, need to also implement the O(n) time and O(logn) space solution
- [x] https://leetcode.com/problems/sum-of-square-numbers/
	- Here the input constraint were quite large (2^31), so even though I got the two pointer approach I was getting tle, the key point was to realize the search space was between (0, sqrt(2^31)).
- [x] https://leetcode.com/problems/boats-to-save-people/
- [x] https://leetcode.com/problems/minimize-maximum-pair-sum-in-array/
- [x] https://leetcode.com/problems/3sum-with-multiplicity/
- [x] https://leetcode.com/problems/trapping-rain-water/
- [x] https://leetcode.com/problems/container-with-most-water/
- [x] https://leetcode.com/problems/next-permutation/
- [x] https://leetcode.com/problems/next-greater-element-iii/
- [x] https://leetcode.com/problems/minimum-adjacent-swaps-to-reach-the-kth-smallest-number/
- [x] https://leetcode.com/problems/valid-palindrome/
- [x] https://leetcode.com/problems/reverse-string/
- [x] https://leetcode.com/problems/reverse-vowels-of-a-string/
- [x] https://leetcode.com/problems/valid-palindrome-ii/
- [x] https://leetcode.com/problems/reverse-only-letters/
- [x] https://leetcode.com/problems/remove-element/
- [x] https://leetcode.com/problems/sort-colors/
- [x] https://leetcode.com/problems/flipping-an-image/
- [x] https://leetcode.com/problems/squares-of-a-sorted-array/
- [x] https://leetcode.com/problems/sort-array-by-parity/
- [x] https://leetcode.com/problems/sort-array-by-parity-ii/
- [x] https://leetcode.com/problems/pancake-sorting/
- [x] https://leetcode.com/problems/reverse-prefix-of-word/
- [x] https://leetcode.com/problems/reverse-string-ii/
- [x] https://leetcode.com/problems/reverse-words-in-a-string/
- [x] https://leetcode.com/problems/reverse-words-in-a-string-iii/
- [x] https://leetcode.com/problems/bag-of-tokens/
- [x] https://leetcode.com/problems/di-string-match/
- [x] https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends/
- [x] https://leetcode.com/problems/sentence-similarity-iii/
- [x] https://leetcode.com/problems/shortest-distance-to-a-character/
- [x] https://leetcode.com/problems/find-k-closest-elements/

## 2. Slow and Fast Pointers
- [x] https://leetcode.com/problems/linked-list-cycle/
- [x] https://leetcode.com/problems/linked-list-cycle-ii/
      - I found a solution using map/set which require O(n) space.
      - The optimal solution with constant space used two pointers to first find a point inside loop such that the point and head are equidistance from the start of the loop.
- [x] https://leetcode.com/problems/remove-nth-node-from-end-of-list/
- [x] https://leetcode.com/problems/rotate-list/
- [x] https://leetcode.com/problems/reorder-list/
- [x] https://leetcode.com/problems/palindrome-linked-list/
- [x] https://leetcode.com/problems/find-the-duplicate-number/
- [x] https://leetcode.com/problems/circular-array-loop/
- [x] https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum/
- [x] https://leetcode.com/problems/find-k-th-smallest-pair-distance/
    - The solution was to do a binary search on possible distance between pair and find the number of pairs with that distance, and find the smallest distance such that number of pairs with this distance is greater than or equal to k 
    - The other key thing was counting the number of pairs with distance d, it required using sliding window technique
- [ ] https://leetcode.com/problems/moving-stones-until-consecutive-ii/
- [x] https://leetcode.com/problems/rotating-the-box/
- [x] https://leetcode.com/problems/rotate-array/
- [x] https://leetcode.com/problems/string-compression/
- [ ] https://leetcode.com/problems/last-substring-in-lexicographical-order/
- [x] https://leetcode.com/problems/remove-duplicates-from-sorted-array/
- [x] https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/
- [x] https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/
- [x] https://leetcode.com/problems/duplicate-zeros/
- [x] https://leetcode.com/problems/statistics-from-a-large-sample/
- [x] https://leetcode.com/problems/partition-labels/
- [x] https://leetcode.com/problems/magical-string/
- [x] https://leetcode.com/problems/friends-of-appropriate-ages/
- [x] https://leetcode.com/problems/longest-mountain-in-array/
- [x] https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/
      Trust your intuition a bit more when coming up with solutions

## 3. Running from beginning of 2 arrays / Merging 2 arrays
- [x] https://leetcode.com/problems/merge-sorted-array/
- [x] https://leetcode.com/problems/heaters/
- [x] https://leetcode.com/problems/find-the-distance-value-between-two-arrays/
- [x] https://leetcode.com/problems/intersection-of-two-linked-lists/
- [x] https://leetcode.com/problems/intersection-of-two-arrays/
- [x] https://leetcode.com/problems/intersection-of-two-arrays-ii/
- [x] https://leetcode.com/problems/implement-strstr/\
- [x] https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/
- [x] https://leetcode.com/problems/long-pressed-name/
- [x] https://leetcode.com/problems/longest-uncommon-subsequence-ii/
- [x] https://leetcode.com/problems/compare-version-numbers/
- [x] https://leetcode.com/problems/compare-version-numbers/
- [x] https://leetcode.com/problems/camelcase-matching/
- [x] https://leetcode.com/problems/expressive-words/
- [x] https://leetcode.com/problems/find-median-from-data-stream/
- [x] https://leetcode.com/problems/ways-to-split-array-into-three-subarrays/
- [x] https://leetcode.com/problems/valid-triangle-number/
- [x] https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/
      - Had to look up solution for optimal approach
      - Was able to come up with a brute force solution, which was to just look for all subset with size n and then find the min difference, but this got tle.
      - The correct approach was to use **meet in the middle** technique to reduce the time complexity
- [x] https://leetcode.com/problems/closest-subsequence-sum/
- [x] https://leetcode.com/problems/shortest-unsorted-continuous-subarray/
- [x] https://leetcode.com/problems/most-profit-assigning-work/
- [x] https://leetcode.com/problems/largest-merge-of-two-strings/
- [x] https://leetcode.com/problems/swap-adjacent-in-lr-string/

## 4. Split & Merge of an array / Divide & Conquer
- [x] https://leetcode.com/problems/partition-list/
- [ ] https://leetcode.com/problems/sort-list/