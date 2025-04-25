# Number Theory

## Divisors

A number **a** is divisor/factor of number **b** if **a** divides **b**, i.e remainder of **b/a** is **0**.
For a number **a** to be divisor of **b** there must exist a number **k** such that **b = a * k** and **k** must also be a divisor of **b**.

> [!NOTE]
> **k** can be equal to **a** as well, this is the case for square of prime numbers.
> If a number n is a squar of prime number p then it will have 3 divisors, i.e **1, p, n**

**Example:** 1, 2, 4, 8 are divisors of 16

## Prime Number

A number is prime number if it has only two factors, i.e 1 and itself.

We can use **Trial Division** to check if a number is prime or not.
In **Trial Division** to check if a number **n** is prime or not we check if it is divisible by any prime number in range $`[2,\sqrt{n}]`$.

**Explanation why to we only look up to $`\sqrt{n}`$:**
If n is not prime then it will have two numbers **a** and **b** such that **n = a * b**, `a,b != 1`, `a,b != n`.
There are two possibilities for values of **a** and **b**, both **a** and **b** equal $`\sqrt{n}`$, or one of the value is greater than $`\sqrt{n}`$ and other is less than $`\sqrt{n}`$.
In both the cases checking for divisor above $`\sqrt{n}`$ is useless as for values greater than $`\sqrt{n}`$ we will need another divisor less than $`\sqrt{n}`$ to satisfy the equation **n = a * b**, but we already checked that no divisor exists with value less than $`\sqrt{n}`$.

**Explanation why we check for divison with only prime numbers:**
If n is divisible by a number x then it will also be divisible by its prime factors, therefore only checking for division with factors is enough.

**Trial Division Code:**
```cpp
bool IsPrime(n)
{
  if (n < 2 ) return false;
  for (i = 2; i * i <= n; ++i)
  {
    // here we check division with each i but we can optimize and
    // only check for division prime numbers less than equal to n
    if (n % i == 0)
    {
      return false;
    }
  }
  return true;
}
```

To find all prime numbers in range $`[1, \sqrt{n}]`$ we can use **Sieve of Eratosthenes** 

## Composite Number

A number is composite if it is not prime.
