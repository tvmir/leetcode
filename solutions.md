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

---

Given an integer array nums sorted in non-decreasing order, **remove the duplicates in-place** such that each unique element appears **only once**. The relative order of the elements should be kept the same.

#### Example:

- Input: nums = [0,0,1,1,1,2,2,3,3,4]
- Output: 5, res = [0,1,2,3,4]

#### Solution:

- Breakdown:

  1. 0 0 1 1 1 2 2 3 3 4

     l . r (They're equal so move right by 1)

  2. 0 0 1 1 1 2 2 3 3 4

     l .... r (Now they're not equal, so make the left val = to the right val, and move left by 1)

  3. 0 1 1 1 1 2 2 3 3 4

     ... l ....... r (Keep moving right pointer until it's not equal to left, and assign the left val to be the next diff right val)

  4. 0 1 2 1 1 2 2 3 3 4

     ..... l ............ r

  5. 0 1 2 3 1 2 2 3 3 4

     ........ l ............... r

  6. 0 1 2 3 4 -> Output = 5

- Steps:

  - Initialize a pointer at the 0<sup>th</sup> index and a pointer at the 1<sup>st</sup> index
  - Loop through the list while right is smaller than N
  - If the value of the left pointer is != the value of the right pointer, increment left by 1 and assign the right value to be the new left value
  - Else if they're equal keep moving the right pointer by 1 until it finds a different value
  - Return the left pointer + 1 to get the elements of the new constructed list

- Code:

  ```python
  def removeDuplicates(nums):
    N = len(nums)
    left, right = 0, 1

    while right < N:
      if nums[left] != nums[right]:
        left += 1
        nums[left] = nums[right]

      else:
        right += 1

    return left + 1
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given an integer array nums sorted in non-decreasing order, remove some duplicates in-place such that **each unique element appears at most twice**. The relative order of the elements should be kept the same.

#### Example:

- Input: nums = [0,0,1,1,1,1,2,3,3]
- Output: 7, res = [0,0,1,1,2,3,3]

#### Solution:

- Breakdown:

  1. 0 0 1 1 1 1 2 3 3

     l .... r (Not equal so assign the left val + 2 to be the right val, then move both left and right pointers by 1)

  2. 0 0 1 1 1 1 2 3 3

     ... l .. r (Same thing as above)

  3. 0 0 1 1 1 1 2 3 3

     ...... l ....... r (Since they're equal, only move the right pointer until we find a different value, now do the same operation, make the new left value + 2 to be the current right value)

  4. 0 0 1 1 2 1 2 3 3

     ........ l ......... r

  5. 0 0 1 1 2 3 2 3 3

     ........... l .......... r

  6. 0 0 1 1 2 3 3 3 3

     .............. l ......... r

  7. 0 0 1 1 2 3 3 \_ 3

     ................. l ........ r

  8. 0 0 1 1 2 3 3 \_ \_

- Steps:

  - Initialize a pointer at the 0<sup>th</sup> index and a pointer at the 2<sup>nd</sup> index
  - Loop through the list while the right pointer is less than N
  - if the value of the left pointer is != the value of the right pointer, assign the value of the left pointer + 2 to be the current right value, and then increment the left and right pointers by 1
  - Else increment the right pointer by 1 until the next different element
  - Return the left pointer + 2 to get the elements of the new costructed list containing at most 2 of the same value

- Code:

  ```python
  def removeDuplicates(nums):
    N = len(nums)
    left, right = 0, 2

    while right < N:
      if nums[left] != nums[right]:
        nums[left + 2] = nums[right]
        left += 1
        right += 1

      else:
        right += 1

    return left + 2
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given an integer array nums sorted in non-decreasing order, return an array of the **squares of each number sorted** in non-decreasing order.

#### Example:

- Input: nums = [-4,-1,0,3,10]
- Output: [0,1,9,16,100]

#### Solution:

- Breakdown:

  1. Original: -4 -1 0 3 10
  2. **Absolute Value**: 4 1 0 3 10

  3. 4 . 1 . 0 . 3 . 10

     l .................. r (nums[r] > nums[l] so we square the right value, then decrement the right pointer by 1)

     -> [_, _, _, _, 100]

  4. 4 . 1 . 0 . 3 . 100

     l ............ r (nums[l] > nums[r] so we square the left value, then increment the left pointer by 1)

     -> [_, _, _, 16, 100]

  5. 16 . 1 . 0 . 3 . 100

     ...... l ....... r

     -> [_, _, 9, 16, 100]

  6. 16 . 1 . 0 . 9 . 100

     ...... l .. r

     -> [_, 1, 9, 16, 100]

  7. 16 . 1 . 0 . 9 . 100

     -> [0, 1, 9, 16, 100]

- Steps:

  - Initialize a pointer at the 0<sup>th</sup> index and a pointer at the N - 1<sup>th</sup> index
  - Initialize a list containing 1s with length N to not affect multiplication
  - Loop through the list in reverse order
  - If the absolute value of the left val is greater than the absolute value of the right val then square the left value and store it in the new list, afterwards increment the left pointer
  - Else square the right val and store it in the same new list, afterwards decrement the right pointer
  - Return the newly constructed list

- Code:

  ```python
  def sortedSquares(nums):
    N = len(nums)
    left, right = 0, N - 1
    res = [1] * N

    for i in range(N - 1, -1, -1):
      if abs(nums[left]) > abs(nums[right]):
        res[i] = pow(nums[left], 2)
        left += 1

      else:
        res[i] = pow(nums[right], 2)
        right += 1

    return res

  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(n)

---

You are given an integer array **height of length n**. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

<img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg">

#### Example:

- Input: height = [1,8,6,2,5,4,8,3,7]
- Output: 49

#### Solution:

- Breakdown:

  1. 1 8 6 2 5 4 8 3 7

     l ...................... r <br>
     (r > l), increment left pointer <br>
     width: 8-0 = 8 (indices) <br>
     height: 1 (min between the left and right values) <br>
     area: 8\*1 = 8

  2. 1 8 6 2 5 4 8 3 7

     .. l ................... r <br>
     (l > r), decrement the right pointer <br>
     width: 8-1 = 7 <br>
     height: 7 (min between the left and right values) <br>
     area: 7\*7 = **49**

  3. 1 8 6 2 5 4 8 3 7

     .. l ................ r

     width: 7-1 = 6 <br>
     height: 3 (min between the left and right values) <br>
     area: 6\*3 = 18

  4. 1 8 6 2 5 4 8 3 7

     .. l ............. r

     width: 6-1 = 5 (indices) <br>
     height: 8 (min between the left and right values) <br>
     area: 5\*8 = 40

  5. 1 8 6 2 5 4 8 3 7

     ..... l ....... r

     width: 5-2 = 3 (indices) <br>
     height: 4 (min between the left and right values) <br>
     area: 3\*4 = 12

  6. 1 8 6 2 5 4 8 3 7

     ..... l ... r

     width: 4-2 = 2 (indices) <br>
     height: 5 (min between the left and right values) <br>
     area: 2\*5 = 10

  7. 1 8 6 2 5 4 8 3 7

     ..... l . r

     width: 3-2 = 1 (indices) <br>
     height: 2 (min between the left and right values) <br>
     area: 1\*2 = 2

- Steps:

  - Initialize a pointer at the 0<sup>th</sup> index and a pointer at the N - 1<sup>th</sup> index
  - Get the max area and assign it to 0
  - Loop through the list while the left pointer is less than the right pointer
  - Initialize the width to be the right pointer - the left pointer
  - Get the minimum height between both left and right values
  - Calculate the area of the width and the minimum height
  - Use the max area we assigned and get the maximum area between itself and the area calculated
  - Increment the left pointer if the left height is < than the right height
  - Decrement the right pointer if the right height is < than the left height
  - Else increment the left pointer, and decrement the right pointer
  - Return the maximum area

- Code:

  ```python
  def maxArea(height):
    N = len(height)
    left, right = 0, N - 1
    max_area = 0

    while left < right:
      width = right - left
      min_height = min(height[left], height[right])
      area = width * min_height

      max_area = max(max_area, area)

      if height[left] < height[right]:
        left += 1

      elif height[right] < height[left]:
        right -= 1

      else:
        left += 1
        right -= 1

    return max_area
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)
