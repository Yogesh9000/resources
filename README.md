# C++

## Web

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
