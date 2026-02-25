# Array

## Subsequence
- A subsequence of an array is a sequence of elements from the array, maintaining their relative order, but not necessarily appearing consecutively.
- If a array/sequence has n elements then it will have **2^n** subsequences
```
We can arrive at this result if we take an example of 3 elements:

S = {a, b, c}
Now to generate every sub-set we can model the presence of an element using a binary digit:

xxx where x is either 0 or 1
Now lets enumerate all possibilities:

000 // empty sub-set
001
010
011
100
101
110
111 // the original set it self!

lets take 011 as an example. The first digit is 0 then, a is not in this subset, but b and c do exist because their respective binary digits are 1's.
```
- Example
![[subsequence.png]]