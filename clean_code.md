# Clean Code

## Meaningful Names

> [!NOTE]
> One guideline is that the length of a variable name should be in proportion to its scope - global variables should have long names, local variables should have short ones.

### Some rules for creating names

* **Use intention-revealing names:**

> [!IMPORTANT]
> The names of a variable, function, or class should make the context of the code explicit.

  The name of a variable, function, or class, should answer all the big questions. It should tell you why it exists, what it does, and how it is used.

  **Example:**
  ```java
  // the below function has a simple implementation, but the context of the code is not explicit
  public List<int[]> getThem() {
    List<int[]> list1 = new ArrayList<int[]>(); // what does list1 hold?
    for (int[] x : theList)
    if (x[0] == 4) // what are 0 and 4?
    list1.add(x);
    return list1; // how to use this return value?
  }

  // same function with better names to make the context more explicit
  public List<int[]> getFlaggedCells() {
    List<int[]> flaggedCells = new ArrayList<int[]>();
    for (int[] cell : gameBoard)
    if (cell[STATUS_VALUE] == FLAGGED)
    flaggedCells.add(cell);
    return flaggedCells;
  }

  // take a step further and use a class for cells instead of int[], we can hide the magic numbers from user
  public List<Cell> getFlaggedCells() {
    List<Cell> flaggedCells = new ArrayList<Cell>();
    for (Cell cell : gameBoard)
    if (cell.isFlagged())
    flaggedCells.add(cell);
    return flaggedCells;
  }
  ```

* **Avoid Disinformation:** 

  We should avoid words whose acutal meanings vary from our intended meaning.

  **Example:** 

  Do not use the name **accountList** for a list of accounts unless the undelying data structure used to hold the list is acutally a **list**, instead a plain **accounts** would be better.

* **Make Meaningful Distinctions:**

  If you need to name the variables, functions, or classes which does something similar differently, then do not just use **noise words** or **number series**, choose names which make an actual distinction

  **Example:**
  ```cpp
  // It is difficult for the user to figure out from the name of the below functions, which one to call for his use case
  getActiveAccount();
  getActiveAccounts();
  getActiveAccountInfo();
  ```

* **Use Pronounceable Names** 

* **Use Searchable Names:** 

  It is much easier to search **MAX_CLASSES_PER_STUDENT**, then  something like **a**, **b**, **7**, etc

* **Avoid Encodings:**
  
  Do not try to encode things like type or scoping information into names, this adds an extra burdern of deciphering.

* **Avoid Mental Mapping:** 

  Readers shouldn’t have to mentally translate your names into other names they already know. This problem generally arises from a choice to use neither problem domain terms nor solution domain terms.

* **Class Names:**

  Classes and objects should have noun or noun phrase names like Customer, WikiPage, Account, and AddressParser, this is because classes are usually an abstraction for an entity/thing/concept. Avoid words like Manager, Processor, etc this sound more like function names as they refer to some action.

  But this is not a hard-and-fast rule, and can be ignored in cases where it makes sense to.

* **Method Names:**

  Methods should have verb or verb phrase names like **postPayment**, **deletePage**, or **save**.

  When constructors are overloaded, use static factory methods with names that describe the arguments. For example,
  `Complex fulcrumPoint = Complex.FromRealNumber(23.0);` 
  is generally better than,
  `Complex fulcrumPoint = new Complex(23.0);` 
  Consider enforcing their use by making the corresponding constructors private.

* **Pick One Word per Concept:** 

  Pick one word for one abstract concept and stick with it. For instance, it’s confusing to have fetch, retrieve, and get as equivalent methods of different classes. How do you remember which method name goes with which class?

* **Don’t Pun:**

  Avoid using the same word for two purposes. Using the same term for two different ideas is essentially a pun.

  Let’s say we have many classes where add will create a new value by adding or concatenating two existing values. Now let’s say we are writing a new class that has a method that puts its single parameter into a collection, insteading using add as the name of method for consistency, it might be better to use a name like **insert** or **append**.

* **Use Solution Domain Names:** 

  Our code will be read by fellow programmers, so go ahead and use computer science terms, algorithm names, pattern names, math terms, etc.
  It is not always wise to try and derive name from the problem domain, this creates a need to know what those names mean.

* **Use Problem Domain Names:** 

  When there is no **programmer-eese** term, use names from problem domain.

## Functions

* **Small:**
  
  The ﬁrst rule of functions is that they should be small. The second rule of functions is that they should be smaller than that.

* **Do One Thing:** 

  Functions should do one thing. They should do it well. They should do it only.
  > One way to know that a function is doing more than “one thing” is if you can extract another function from it with a name that is not merely a restatement of its implementation
