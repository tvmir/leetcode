# Leetcode Solutions

## 1. Two Pointers

Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number.

Return the indices of the two numbers, index1 and index2, **added by one**.

#### Example:

- Input: nums = [2,7,11,15], target = 9
- Output: [1,2]

#### Solution:

- Steps:

  - Initialize a pointer at 0th index and a pointer at the N-1 index
  - Loop through the list while the left pointer is smaller than the right pointer
  - Get the **sum of values** of left and right pointers
  - If the sum is > than the target then decrement the right pointer
  - If the sum is < than the target then increment the left pointer
  - Else return a new list containing both the left and right pointers + 1

- Code:

  ```python
  def twoSum(nums, target):
    N = len(nums)
    left, right = 0, N - 1

    while left < right:
      sum = nums[left] + nums[right]

      if sum > target:
        right -= 1

      elif sum < target:
        left += 1

      else:
        return [left + 1, right + 1]
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given an integer array nums, **move all 0's to the end** of it while maintaining the relative order of the non-zero elements.

#### Example:

- Input: nums = [0,1,0,3,12]
- Output: [1,3,12,0,0]

#### Solution:

- Breakdown:

  1. 0 1 0 3 12

     l . r (swap 0 and 1)

  2. 1 0 0 3 12

     .. l ... r (Move left by 1, move right by 2, swap)

  3. 1 3 0 0 12

     ..... l .... r (Move left by 2, move right by 3, swap)

  4. 1 3 12 0 0

- Steps:

  - Initialize a pointer at the 0<sup>th</sup> index and a pointer at the 1<sup>st</sup> index
  - Loop through the list while the right pointer is less than N
  - If the value at the left pointer is != 0 then increment both left and right pointers by 1
  - If the value at the right pointer is == 0 then increment the right pointer by 1
  - Else if we found the value of the left pointer to be 0 and the value of the right pointer to be > 0 then swap both values

- Code:

  ```python
  def moveZeroes(nums):
    N = len(nums)
    left, right = 0, 1

    while right < N:
      if nums[left] != 0:
        left += 1
        right += 1

      elif nums[right] == 0:
        right += 1

      else:
        nums[left], nums[right] = nums[right], nums[left]
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)
