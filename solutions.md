# Leetcode Solutions

## 1. Two Pointers

==============

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
