# C++

## Links

- [regular cast vs staic_cast vs dynamic_cast](https://stackoverflow.com/questions/28002/regular-cast-vs-static-cast-vs-dynamic-cast)

## Notes

### Return Value Optimization (RVO)

> [!NOTE]
> [CppCon Talk On RVO](https://www.youtube.com/watch?v=WyxUilrR6fU&ab_channel=CppCon) 

- It is a form of optimization, which prevents unnecessary copies when returning temporary/local values from a function.
- **Copy Elision** is a form of rvo.
- Two types of rvo in C++:
  - Named Return Value Optimization (NRVO) : returning a named local variable from a function.
  - Unamed Return Value Optimization (URVO) : returning a rvalue/temporary value.
- (U)RVO is guaranteed in C++ starting C++17. NRVO is optional but recommended for compilers to implement. all major compilers like gcc, msvc, clang implement it.
- We can turn off rvo using the flag `-fno-elide-constructor`. Won't turn off (U)RVO starting C++ 17.
- **-Wnrvo** in **GCC v14** and above if the compiler does not elide copy from a local variable to the return value in a context where it is allowed
- RVO fails in following cases:
  - RVO will not work when returning a object not created in current scope.
  - Return type of function and type of object must match for rvo to work. That means inheritance will prevent rvo.
  - RVO will not work when returning different objects in different execution path from the function **(Only for NRVO)**
  ```cpp
  Obj foo(int num)
  {
    Obj x1 = Obj(3);
    Obj x2 = Obj(4);
    if (num < 5) // compiler cannot decide the execution path at compile time.
    {
      return x1; // No rvo optimization
    }
    return x2; // No rvo optimization
  }
  ```
  - When returning complex expression **(Only for NRVO)**
  ```cpp
  Obj foo()
  {
    Obj x1 = Obj(3);
    Obj x2 = Obj(3);
    int a = rand() % 100;
    return (a < 50 ? x1 : x2); // complex expression
  }

  Obj foo()
  {
    Obj x1 = Obj(3);
    return std::move(x1); // complex expression
  }
  ```

# DSA

## Algorithms

### Sorting

#### [Selection Sort](https://en.wikipedia.org/wiki/Selection_sort)

The algorithm divides the input list into two parts: a sorted sublist of items which is built up from left to right at the front (left) of the list and a sublist of the remaining unsorted items that occupy the rest of the list. Initially, the sorted sublist is empty and the unsorted sublist is the entire input list. The algorithm proceeds by finding the smallest (or largest, depending on sorting order) element in the unsorted sublist, exchanging (swapping) it with the leftmost unsorted element (putting it in sorted order), and moving the sublist boundaries one element to the right. 

- Selection sort is an in-place comparison sorting algorithm
- **Time Complexity:** O(n^2)
- Selection sort can also be used on list structures that make add and remove efficient, such as a linked list
- Selection sort implementaion involving swaps is unstable
- Selection sort performs better than bubble sort, but insertion sort performs better than selection sort, this is because insertion sort performs fewer comparisons.

**Example:**
| Sorted Sublist       | Unsorted Sublist     | Least Element in Unsorted Sublist |
| ---------------      | -------------------- | --------------------------------- |
| ()                   | (12, 25, 64, 11, 22) | 11                                |
| (11)                 | (12, 25, 64, 22)     | 12                                |
| (11, 12)             | (25, 64, 22)         | 22                                |
| (11, 12, 22)         | (25, 64)             | 25                                |
| (11, 12, 22, 25)     | (64)                 | 64                                |
| (11, 12, 22, 25, 64) | ()                   |                                   |

**Sample Implementaion:**
```cpp
void selectionSort(std::vector<int> &vec)
{
  int sortedListIdx{-1};
  for (int i{0}; i < vec.size(); ++i) {
    std::pair minValue{0, std::numeric_limits<int>::max()};
    for (int j{i}; j < vec.size(); ++j)
    {
      if (vec[j] < minValue.second)
      {
        minValue.first = j;
        minValue.second = vec[j];
      }
    }
    ++sortedListIdx;
    std::swap(vec[sortedListIdx], vec[minValue.first]);
  }
}
```

## NOTES

### GCD/HCF

#### Methods to Find GCD

There are multiple methods to find the Greatest Common Divisor (GCD) such as:

- Prime Factorization Method
- Euclid’s Division Algorithm
- Binary GCD Algorithm (Stein's Algorithm)

##### Prime Factorization Method to Find GCD

The prime factorization method involves breaking each number down into its prime factors (prime numbers that multiply to give the original number).
The GCD is found by taking the product of the lowest powers of all common prime factors.

**Sample Implementaion:**
```cpp
std::unordered_map<int, int> primeFactorize(int num)
{
  std::unordered_map<int, int> factors{};
  for (int i{2}; i < std::sqrt(num); ++i)
  {
    while (num % i == 0)
    {
      factors[i]++;
      num = num / i;
    }
  }
  if (num > 1)
  {
    factors[num]++;
  }
  return factors;
}

int gcdWithPrimFactorization(int num1, int num2)
{
  if (num1 == 0) return num2;
  if (num2 == 0) return num1;

  auto factor1 = primeFactorize(num1);
  auto factor2 = primeFactorize(num2);
  int gcd = 1;
  for (auto [factor, count] : factor1) {
    if (factor2.contains(factor))
    {
      gcd *= std::pow(factor, std::min(factor1[factor], factor2[factor]));
    }
  }
  return gcd;
}
```

##### Euclid's Division Algorithm

1. Apply Euclid’s division lemma to two numbers a and b, where a > b. The division lemma gives two numbers q (quotient) and r (remainder), such that: a=bq+rwhere 0≤r<ba=bq+rwhere 0≤r<b
2. If the remainder r = 0, then b is the GCD of a and b. If r≠0r=0, apply the division lemma again to b and r.
3. Continue the process until the remainder is zero.
4. When the remainder is zero, the divisor at that stage is the GCD of the given numbers.

**Sample Implementaion:**
```cpp
int gcdUsingEuclidsDivision(int num1, int num2)
{
  if (num1 == 0) return num2;
  if (num2 == 0) return num1;

  if (num1 < num2) std::swap(num1, num2);

  while (num1 % num2 != 0)
  {
    num1 = num1 % num2;
    if (num1 < num2) std::swap(num1, num2);
  }

  return num2;
}
```

##### Binary GCD Algorithm(aka Stein's Algorithm) 
The algorithm finds the GCD of two nonnegative numbers u and v by repeatedly applying these identities

1. gcd(u , 0)   = u                      : everything divides zero, and u is the largest number that divides u.
2. gcd(2u , 2v) = 2 * gcd(u , v)         : 2 is a common divisor.
3. gcd(u , 2v)  = gcd(u , v) if u is odd : 2 is then not a common divisor.
4. gcd(u , v)   = gcd(u , v−u) if u , v odd and u ≤ v.

**Sample Implementaion:**
```cpp
unsigned int gcdUsingSteinsAlgorithm(unsigned int num1, unsigned int num2)
{
  // case1: gcd(u, 0) = u
  if (num1 == 0) return num2;
  if (num2 == 0) return num1;

  // case2: gcd(2^i * u, 2^j * v) = 2^k gcd(u, v); k = min(i, j)
  // count the trailing zeroes in num1 and num2,
  // number of trailing zeroes determine the maximum power of 2 that will divide a number 
  // __builtin_ctzll is a builtin gcc/clang function to count trailing zeroes
  unsigned int i = __builtin_ctzll(num1);
  num1 >>= i;
  unsigned int j = __builtin_ctzll(num2);
  num2 >>= j;
  unsigned int k = std::min(i, j);

  while (true) { // at this point both num1 and num2 should be odd
    if (num1 > num2) std::swap(num1, num2);

    // case4: gcd(u, v) = gcd(u, v - u); u and v are odd, u <= v
    num2 = num2 - num1;

    if (num2 == 0) return num1 << k; // restore the common power of 2 that divides both num1 and num2 before returning the answer

    // case3: gcd(u, 2v) = gcd(u, v); u is odd so 2 is not a common divisor
    num2 >>= __builtin_ctzll(num2);
  }
}
```

### LCM

> [!NOTE]
> gcd(a, b) * lcm(a, b) = a * b
> therefore, lcm(a, b) = (a * b) / gcd(a, b)

**Sample Implementaion:**
```cpp
int lcm(int a, int b) {
  int hcf{};
  int lcm{};
  long product = static_cast<long>(a) * b;
  if (a == 0) hcf = b, lcm = 0;
  if (b == 0) hcf = a, lcm = 0;

  int i = __builtin_ctzl(a);
  a >>= i;
  int j = __builtin_ctzl(b);
  b >>= j;
  int k = std::min(i, j);
  while (true)
  {
    if (a > b) std::swap(a, b);

    b = b - a;

    if (b == 0) return static_cast<int>(product / (a << k)); // divide a*b by gcd to get the lcm. interger overflow could occur here

    b >>= __builtin_ctzll(b);
  }
}
```

### Armstrong Numbers

A number is *Armstrong Number* if it's equal to the sum of it's digit raised to the power of number of digit's in the number

*Example:*
n = 153
*Explanation:* 1^2 + 5^3 + 3^3 = 1 + 125 + 27 = 153

# Miscellaneous

## Notes

- [math](https://takeuforward.org/data-structure/print-all-divisors-of-a-given-number/) given two numbers a and b, if b is a divisor of a, then *a/b* is also a divisor of a.
