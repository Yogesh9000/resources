# LEETCODE

## [check-if-array-is-sorted-and-rotated](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/submissions/1494169461/)
**Solution:** 
```cpp
bool check(std::vector<int> &vec) {
    if (vec.empty() || vec.size() == 1) return true;

    auto cvec{vec};
    std::ranges::sort(cvec);
    for (int i{0}; i < vec.size(); ++i) {
      if (cvec == vec) return true;
      int temp{cvec.back()};
      for (int i{0}; i < cvec.size(); ++i) {
        std::swap(cvec[i], temp);
      }
    }
    return false;
  }
```
**Note:** spent some time trying to implement a O(n) solution, but should have tried a brute force approach with time complexity O(n^2) early on, since the size of vec <= 100

## [Single Number](https://leetcode.com/problems/single-number/description/)
**Solution:** 
```cpp
int singleNumber(vector<int>& nums) {
  int xor1{0};
  for(const auto &ele : nums)
  {
    xor1 ^= ele;
  }
  return xor1;
}
```
**Note:** Needed to implement the solution in O(n) time complexity and O(1) space complexity, for this need to know that xor of a number with itself is 0

## [Longest Subarray with Sum K](https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=longest-sub-array-with-sum-k)
**Solution:**
```cpp
int longestSubarray(std::vector<int>& arr, int k) {
    int ans{0};
    std::map<int, int> prefixSum{};
    int currentSum{0};
    for (int i{0}; i < arr.size(); ++i) {
      currentSum += arr[i];
      if (currentSum == k)
      {
        ans = std::max(ans, i + 1);
      }
      else if(prefixSum.find(currentSum - k) != prefixSum.end())
      {
        ans = std::max(ans, i - prefixSum[currentSum - k]);
      }
      if (prefixSum.find(currentSum) == prefixSum.end())
      {
        prefixSum[currentSum] = i;
      }
    }
    return ans;
  }
```
**Note:** gotta to a O(n^2) solution on my own, but had to look up that need to use hashing to reduce the time compelxity to O(n) by storing the prefix sum of subarrays

## [Sort Colors](https://leetcode.com/problems/sort-colors/description/) 
**Solution:**
```cpp
void sortColors(std::vector<int>& nums)
  {
    int l{0};
    int m{0};
    int e = nums.size() - 1;
    while(m <= e)
    {
      if (nums[m] == 0)
      {
        std::swap(nums[l], nums[m]);
        ++l;
        ++m;
      }
      else if (nums[m] == 1) ++m;
      else if (nums[m] == 2)
      {
        std::swap(nums[e], nums[m]);
        --e;
      }
    }
  }
 ``` 

- problem is simple, can be solved using sorting or keeping a count of number of 0s, 1s, 2s and then writing it back in the array in sorted order.
- Since this problem is a variant of [Dutch National flag algorithm](https://en.wikipedia.org/wiki/Dutch_national_flag_problem) we can also use the three pointer approach.

## [Majority Element](https://leetcode.com/problems/majority-element/submissions/1513393153/)
**Solution:**
```cpp
int majorityElement(std::vector<int>& nums)
  {
    int candidate{0};
    int count{0};
    for(const auto &num : nums) {
      if (count == 0) candidate = num;
      if (candidate == num) ++count;
      else --count;
    }
    return count;
  }
```

- problem can be solved easily by keeping a frequency count of elements and returing the element with the most highest frequency.
- Since the constraints state that a element with frequency n/2 always exist, we can also use the [Boyer–Moore majority vote algorithm](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm)

## [Majority Element II](https://leetcode.com/problems/majority-element-ii/description/)
**Solution:**
```cpp
std::vector<int> majorityElement(std::vector<int> &nums)
{
  int candidate1{ -1 };
  int count1{ 0 };
  int candidate2{ -1 };
  int count2{ 0 };

  for (const auto &num : nums)
  {
    if (count1 == 0 && num != candidate2)
    {
      candidate1 = num;
      ++count1;
      continue;
    }
    if (count2 == 0 && num != candidate1)
    {
      candidate2 = num;
      ++count2;
      continue;
    }
    else if (candidate1 == num)
      ++count1;
    else if (candidate2 == num)
      ++count2;
    else
    {
      count1 = std::max(0, count1 - 1);
      count2 = std::max(0, count2 - 1);
    }
  }

  std::vector<int> ans{};
  if (count1 != 0 && std::count(nums.begin(), nums.end(), candidate1) > nums.size() / 3)
    ans.push_back(candidate1);
  if (count2 != 0 && std::count(nums.begin(), nums.end(), candidate2) > nums.size() / 3)
    ans.push_back(candidate2);
  return ans;
}
```

- Simple approach is to keep track of frequency and then return elements with frequency more than n/3
- Since there can be atmost 2 elements with frequency more than n/3   we can use a modified version of [Boyer–Moore majority vote algorithm](https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm)
