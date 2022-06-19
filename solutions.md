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
        right -= 1

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

---

Given an integer array nums, **return all the triplets** [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

#### Example:

- Input: nums = [-1,0,1,2,-1,-4]
- Output: [[-1,-1,2],[-1,0,1]]

#### Solution:

- Breakdown:

  1. Original: -1 . 0 . 1 . 2 . -1 . -4
  2. **Sorted**: -4 . -1 . -1 . 0 . 1 . 2
  3. -4 . -1 . -1 . 0 . 1 . 2

     . i .... l ................. r <br>
     curr_sum = -4 + -1 + 2 = -3 (< 0, increment left pointer)

  4. -4 . -1 . -1 . 0 . 1 . 2

     . i .......... l ........... r <br>
     curr_sum = -4 + -1 + 2 = -3 (< 0, increment left pointer)

  5. -4 . -1 . -1 . 0 . 1 . 2

     . i ............... l ...... r <br>
     curr_sum = -4 + 0 + 2 = -2 (< 0, increment left pointer)

  6. -4 . -1 . -1 . 0 . 1 . 2

     ........ i ... l ............ r (After calculating all sums for single index, we move on to the next one)<br>
     curr_sum = -1 + -1 + 2 = 0 (== 0, increment left pointer and decrement right pointer, store it in a sub list)

  7. -4 . -1 . -1 . 0 . 1 . 2

     ........ i ........ l .. r (After calculating all sums for single index, we move on to the next one)<br>
     curr_sum = -1 + 0 + 1 = 0 (== 0, increment left pointer and decrement right pointer, store it in a sub list)

  8. -4 . -1 . -1 . 0 . 1 . 2

     ................... i .. l .. r (If the current index is the same as the previous one, skip it)<br>
     curr_sum = 0 + 1 + 2 = 3 (Reached the end of calculations, break)

- Steps:

  - Initalize a res list to store all sums
  - Return an empty list if the list contains < than 3 elements
  - **Sort** the list in ascending order
  - Loop through the entire list, whilst the current index is equal to the previous index continue with the calculation
  - Initialize the left pointer to be i + 1, and the right pointer to be the last element in the list
  - Loop through the list while the left pointer is < than the right pointer
  - Calculate the current sum by adding all 3 values (i, left, right)
  - If the sum is == to 0 then append all the values to a sub list, then append it to res, increment the left pointer, decrement the right pointer
  - Increment the left pointer if the current value is == to the prev value
  - Decrement the right pointer if the current value is == to the prev value
  - Increment the left pointer if the curr_sum is < than 0
  - Otherwise decrement the right pointer
  - Return the res list

- Code:

  ```python
  def threeSum(nums):
    N = len(nums)
    res = []

    # Base case
    if N < 3:
      return res

    # Sort List
    nums.sort()

    # Iterate through the list
    for i in range(N):
      if i != 0 and nums[i] == nums[i - 1]:
        continue

      left, right = i + 1, N - 1

      while left < right:
        curr_sum = nums[i] + nums[left] + nums[right]

        if curr_sum == 0:
          sub_list = []
          sub_list.append(nums[i])
          sub_list.append(nums[left])
          sub_list.append(nums[right])

          # Adding all sub lists to the global res list
          res.append(sub_list)

          left += 1
          right -= 1

          while left < right and nums[left] == nums[left - 1]:
            # Skip to the next element if the current is == to the prev value
            left += 1

          while left < right and nums[right] == nums[right + 1]:
            right -= 1

        elif curr_sum < 0:
          left += 1

        else:
          right -= 1

    return res

  ```

- Big-O:
  - Time Complexity: O(n<sup>2</sup>)
  - Space Complexity: O(n)

---

Given an integer array nums of length **n** and an integer **target**, find **three integers in nums** such that the **sum is closest to target**.

Return the sum of the three integers.

#### Example:

- Input: nums = [-1,2,1,-4], target = 1
- Output: 2

#### Solution:

- Breakdown:

  1. Original: -1 . 2 . 1 . -4
  2. **Sorted**: -4 . -1 . 1 . 2
  3. **target**: 1
  4. -4 . -1 . 1 . 2

     . i .... l ...... r <br>
     curr_sum: -4 + -1 + 2 = -3 <br>
     curr_diff: -3 - 1 = |-4| = 4 (curr_sum - target)

  5. -4 . -1 . 1 . 2

     . i ......... l . r <br>
     curr_sum: -4 + 1 + 2 = -1 <br>
     curr_diff: -1 - 1 = |-2| = 2 <br>
     diff: 2 < 4 (< than the curr_diff, so we update the diff) <br>
     ans = -1 (new curr_sum)

  6. -4 . -1 . 1 . 2

     ........ i .. l . r <br>
     curr_sum: -1 + 1 + 2 = 2 <br>
     curr_diff: 2 - 1 = |1| = 1 <br>
     diff: 1 < 2 (< than the curr_diff, so we update the diff) <br>
     ans = 2 (Closest to the target)

- Steps:

  - Initialize 2 variables, one to hold the diff in closeness between the sum and the target, and the other to hold the final answer
  - Sort the list
  - Loop through the list, initialize the left pointer to be i + 1, and the right pointer to be N - 1
  - Loop through the list while the left pointer is less than the right pointer
  - Calculate the current sum between all 3 values (i, left, right)
  - Calculate the difference between the current sum and the target, use absolute value to eliminate -ve numbers
  - If the current diff is **less** than the previous diff, **update the diff to be the current diff** and the **ans to be the current sum**
  - Return the current sum if it's == to the target
  - Else if the current sum is < than the target, increment the left pointer
  - Otherwise decrement the right pointer
  - Return the closest ans to the target

- Code:

  ```python
  def threeSumClosest(nums, target):
    N = len(nums)
    diff, ans = float('inf'), 0

    # Sort list
    nums.sort()

    # Iterate through the list
    for i in range(N):
      left, right = i + 1, N - 1

      while left < right:
        curr_sum = nums[i] + nums[left] + nums[right]
        curr_diff = abs(curr_sum - target)

        if curr_diff < diff:
          diff = curr_diff
          ans = curr_sum

        if curr_sum == target:
          return curr_sum

        elif curr_sum < target:
          left += 1

        else:
          right -= 1

    return ans

  ```

- Big-O:
  - Time Complexity: O(n<sup>2</sup>)
  - Space Complexity: O(1)

---

You are given a string s. We want to **partition the string into as many parts as possible** so that **each letter appears in at most one part**.

Return a list of integers representing the size of these parts.

#### Example:

- Input: s = "ababcbacadefegdehijhklij"
- Output: [9,7,8]

#### Solution:

- Breakdown:

  1. String: a . b . a . b . c . b . a . c . a . d . e . f . e . g . d . e . h . i . j . h .. k . l ... i .. j <br>
     Index: .0 . 1 . 2 . 3 . 4 . 5 . 6 . 7 . 8 . 9 10 11 12 13 .14 15 16 17 18 19 20 21 22 23

  2. Get the last index of each character via a **Hash Map** <br>

  3. First partiton is "ababcbaca" <br>

     a b a b c b a c a <br>
     i <br>
     l <br>
     ...................... r <br>
     size: (r - l) + 1 = (8-0) + 1 = 9 <br>
     res = [9]

  4. Second partiton is "defegde" <br>

     d e f e g d e <br>
     i <br>
     l <br>
     ................. r <br>
     size: (r - l) + 1 = (15-9) + 1 = 7 <br>
     res = [9, 7]

  5. Third partiton is "hijhklij" <br>

     h i j h k l i j <br>
     i <br>
     l <br>
     ............... r <br>
     size: (r - l) + 1 = (23-16) + 1 = 8 <br>
     res = [9, 7, 8]

- Steps:

  - Initialize a hash map that holds all the last indices of each character
  - Initialize a res list to store the sizes of each partition
  - Loop through the string and assign the last index of the character to the current i<sup>th</sup> index
  - Initialize both left and right pointers and assign them to 0
  - Loop through the string
  - Update the right pointer to be the max position of itself or the last index of the current character via the hash map
  - If the right pointer is equal to the current index then calculate the size of that partition
  - Append the size to the res list
  - Increment the right pointer, then update the left pointer to be the new right pointer

- Code:

  ```python
  def partitionLabels(s):
    last_idx = {}
    res = []

    for i, ch in enumerate(s):
      last_idx[ch] = i

    left, right = 0, 0

    for i, ch in enumerate(s):
      right = max(right, last_idx[ch])

      if right == i:
        size = (right - left) + 1
        res.append(size)

        # Moving on to the next partition
        right += 1
        # i, left, and right will start at the same index of the new partition
        left = right

    return res
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(n)

---

Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

#### Example:

- Input: nums = [2,0,1]
- Output: [0,1,2]

#### Solution:

- Breakdown:

  1. 2 . 0 . 1 <br>
     i <br>
     l ........ r

  2. 1 . 0 . 2 <br>
     i <br>
     l .. r (l == 2, swap l and r, r - 1)

  3. 1 . 0 . 2 <br>
     i <br>
     .... l <br>
     .... r (l == 1, l + 1)

  4. 0 . 1 . 2 <br>
     .... i <br>
     ......... l <br>
     .... r (l == 0, swap i and l, i + 1 and l + 1)

- Steps:

  - Initialize 3 pointers, 2 at the 0<sup>th</sup> index and 1 at N - 1
  - Loop through the list while the left pointer is <= to the right pointer
  - If the value of the left value is == 2, **swap the left and right values**, then decrement the right pointer by one
  - Otherwise if the value of the left pointer is == 1 then increment the left pointer by 1
  - Else when the value of the pointer is == 0 then **swap the i and left values**, then increment both the left and i pointers

- Code:

  ```python
  def sortColors(nums):
    N = len(nums)
    i, left, right = 0, 0, N - 1

    while left <= right:
      if nums[left] == 2:
        nums[left], nums[right] = nums[right], nums[left]
        right -= 1

      elif nums[left] == 1:
        left += 1

      else:
        nums[left], nums[i] = nums[i], nums[left]
        i += 1
        left += 1
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

#### Example:

- Input: head = [1,1,1,2,3]
- Output: [2,3]

#### Solution:

- Breakdown:

  1. .... 1 . 1 . 1 . 2 . 3 <br>
     p . c

  2. .... 1 . 1 . 1 . 2 . 3 <br>
     p . c . c (c == c.next, assign c to be c.next and now p points to new c.next)

  3. .... 1 . 1 . 1 . 2 . 3 <br>
     p . ............. c (now p points to 2 and because c != c.next, we return the new list which is [2, 3])

- Steps:

  - Base case where if the head is empty we return the head itself
  - Initialize a **dummy** pointer to contain the prev pointer, and a curr pointer pointing to the head
  - Loop through the list while the curr pointer is not empty
  - If curr.next is not empty and the current value is == to the curr.next value, loop again to check if there are multiple duplicates back to back
  - Assign the current value to be curr.next, break out of the loop and now point the prev.next pointer to be the current curr.next
  - Else assign the prev pointer to point to prev.next
  - return the dummy list **.next** to get all the values of the new list

- Code:

  ```python
  def deleteDuplicates(head):
    if not head:
      return head

    dummy = ListNode(0, head)
    curr, prev = head, dummy

    while curr:
      if curr.next and curr.val == curr.next.val:
        while curr.next and curr.val == curr.next.val:
          curr = curr.next

        prev.next = curr.next

      else:
        prev = prev.next

      curr = curr.next

    return dummy.next
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

#### Example:

- Input: height = [4,2,0,3,2,5]
- Output: 9

#### Solution:

- Breakdown:

  1. .

- Steps:

  - Base

- Code:

  ```python
  def trap(height):

  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

## 2. Sliding Window

Given an array of positive integers nums and a **positive integer** **target**, return the **minimal length of a contiguous subarray** [numsl, numsl+1, ..., numsr-1, numsr] of which the sum is greater than or equal to target. If there is no such subarray, return 0 instead.

#### Example:

- Input: nums = [2,3,1,2,4,3], target = 7
- Output: 2

#### Solution:

- Breakdown:

  1. 2 . 3 . 1 . 2 . 4 . 3 <br>
     l <br>
     .............. r (move r until it's >= target)<br>
     curr_min: 4 (r - l) + 1 <br>
     sum: 8 >= target

  2. 2 . 3 . 1 . 2 . 4 . 3 <br>
     ..... l (move l after getting a valid sum) <br>
     .............. r <br>
     curr_min: still 4 <br>
     sum: still 8

  3. 2 . 3 . 1 . 2 . 4 . 3 <br>
     ..... l <br>
     .................... r <br>
     curr_min: 4 <br>
     sum: 10 >= target (3+1+2+4)

  4. 2 . 3 . 1 . 2 . 4 . 3 <br>
     .......... l <br>
     .................... r <br>
     curr_min: 3 <br>
     sum: 7 == target

  5. 2 . 3 . 1 . 2 . 4 . 3 <br>
     .............. l <br>
     .................... r <br>
     curr_min: still 3 <br>
     sum: still 7

  6. 2 . 3 . 1 . 2 . 4 . 3 <br>
     .............. l <br>
     ........................ r <br>
     curr_min: 3 <br>
     sum: 9

  7. 2 . 3 . 1 . 2 . 4 . 3 <br>
     ................... l <br>
     ........................ r <br>
     curr_min: 2 <br>
     sum: 7 == target (after this r would be out of bounds, hence we break out of the loop)

- Steps:

  - Initialize both left and right pointers and assign them to 0
  - Initialize a curr_min to be a max value, and the sum to be 0
  - Iterate through the list while the right pointer is < than N
  - Calculate the sum by adding it to nums[right] (see comment)
  - While the sum is >= the target get the curent minimum length between the 2 pointers
  - Remove the left pointer's value from the sum calculation because we'll be moving it by 1 afterwards
  - Increment the right pointer whilst the sum is smaller than the target
  - Return 0 if the we couldnt find the sum of the list to be >= to the target, otherwise if it does exists return the curr_min

- Code:

  ```python
  def minSubArrayLen(nums, target):
    N = len(nums)
    left, right = 0, 0
    curr_min, sum = float('inf'), 0

    while right < N:
      # Summing all values from left to right pointer inclusive
      sum += nums[right]

      while sum >= target:
        curr_min = min(curr_min, (right - left) + 1)
        sum -= nums[left]
        left += 1

      right += 1

    return 0 if curr_min == float('inf') else curr_min
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given a string s, find the length of the longest substring without repeating characters.

#### Example:

- Input: s = "abcabcbb"
- Output: 3

#### Solution:

- Breakdown:

  1. p w w k e w r <br>
     l <br>
     r <br>
     max_len = (r - l) + 1 <br>
     set = {}

  2. p w w k e w r <br>
     l <br>
     ... r <br>
     max_len = 2 <br>
     set = {p, w}

  3. p w w k e w r <br>
     l <br>
     ....... r (while the letter is already in the set, move the left pointer)<br>
     max_len = <br>
     set = {}

  4. p w w k e w r <br>
     ....... l <br>
     .......... r <br>
     max_len = 2 <br>
     set = {w, k}

  5. p w w k e w r <br>
     ....... l <br>
     ............ r <br>
     max_len = 3 <br>
     set = {w, k, e}

  6. p w w k e w r <br>
     .......... l <br>
     ................ r <br>
     max_len = 3 <br>
     set = {k, e, w}

  7. p w w k e w r <br>
     .......... l <br>
     ................... r <br>
     max_len = **4** <br>
     set = {k, e, w, r}

- Steps:

  - Base case where if N is empty then return N
  - Initialize an empty set, a max_len and 2 pointers
  - While the right pointer is < than N check while the letter at the right pointer is already in the set
  - If it is remove the letter at the left pointer, otherwise add the letter of the right pointer and increment the left pointer
  - Get the max length between the 2 pointer
  - Increment the right pointer to move to the next letter
  - Return the max length

- Code:

  ```python
  def lengthOfLongestSubstring(s):
    N = len(s)
    set_s = set()
    left, right = 0, 0
    max_len = 0

    # Base Case
    if not N and N == 0:
      return 0

    while right < N:
      while s[right] in set_s:
        set_s.remove(s[left])
        left += 1

      set_s.add(s[right])
      max_len = max(max_len, (right - left) + 1)
      right += 1

    return max_len
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(n) or O(1)

---

Given a binary array nums and an integer k, return the **maximum number of consecutive 1's** in the array if you can **flip at most k 0's**.

#### Example:

- Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
- Output: 6

#### Solution:

- Breakdown:

  1. 1 1 1 0 0 0 1 1 1 1 0 <br>
     l <br>
     ....... r (keep moving r until we reach a 0)<br>
     count = 0 <br>
     max_len = 0

  2. 1 1 1 0 0 0 1 1 1 1 0 <br>
     l <br>
     ....... r <br>
     count = 1 (we encountered a 0, so increment count) <br>
     max_len = 4 (the length between l and r inclusive)

  3. 1 1 1 0 0 0 1 1 1 1 0 <br>
     l <br>
     .......... r <br>
     count = 2 (we encountered another 0, so increment count) <br>
     max_len = 5

  4. 1 1 1 0 0 0 1 1 1 1 0 <br>
     .............. l <br>
     .............. r <br>
     count = 0 (we encountered another 0, but this time it's > than k, so we decrement the 0 count and move l) <br>
     max_len = 0

  5. 1 1 1 0 0 0 1 1 1 1 0 <br>
     .............. l <br>
     ........................... r <br>
     count = 2 <br>
     max_len = 6

- Steps:

  - Initialize two pointers starting at 0, a max_len and a count variable to keep track of the amount of 0s
  - Loop through the list while right is < than N
  - if the right pointer value contains a 0 then we increment the count, afterwards increment the right pointer
  - Whilst count is > than k then we check if the value at the left pointer is 0, if it is then we decrement the count and increment the left pointer until count reaches 0
  - Get the maximum length between left and right pointers inclusive
  - Return the maximum length

- Code:

  ```python
  def longestOnes(nums, k):
    N = len(nums)
    left, right = 0, 0
    max_len = 0
    count = 0

    while right < N:
      if nums[right] == 0:
        count += 1

      right += 1

      while count > k:
        if nums[left] == 0:
          count -= 1

        left += 1

      max_len = max(max_len, right - left)

    return max_len
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

You are given a **string s and an integer k**. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.

Return the **length of the longest substring containing the same letter** you can get after performing the above operations.

#### Example:

- Input: s = "AABABBA", k = 1
- Output: 4

#### Solution:

- Breakdown:

  1. A A B A B B A <br>
     l <br>
     r <br>
     count = {A: 1} <br>
     max_len = 1

  2. A A B A B B A <br>
     l <br>
     ...... r <br>
     count = {A: 2, B: 1} <br>
     max_len = 3 (3-2 = 1 <= k) Get the length of the two pointers - the highest frequency letter in the map (A: 2 in this instance)

  3. A A B A B B A <br>
     l <br>
     ......... r <br>
     count = {A: 3, B: 1} <br>
     max_len = 4 (4-3 = 1 <= k)

  4. A A B A B B A <br>
     l <br>
     ............. r <br>
     count = {A: 3, B: 2} <br>
     max_len = 5 (5-3 = 2 >= k so move the left pointer)

  5. A A B A B B A <br>
     ...... l <br>
     ............. r <br>
     count = {A: 1, B: 2} <br>
     max_len = 1 (3-2 = 1 >= k)

  6. A A B A B B A <br>
     ...... l <br>
     ................ r <br>
     count = {A: 1, B: 3} <br>
     max_len = **4** (4-3 = 1 >= k)

- Steps:

  - Initialize two pointers, a max_len, and a count dictionary to store the letters and their frequencies
  - Loop through the string while the right pointer is < than N
  - Assign the characters to their current frequency
  - Calculate the length between the two pointers, subtract is buy the highest frequency in the ,ap and check while it's greater than k
  - Decrement (eliminate) the element at the left pointer that was already in the map and increment the left pointer
  - Calculate the maximum length between the 2 pointers inclusive
  - Increment the right pointer
  - Return the maximun length

- Code:

  ```python
  def characterReplacement(s, k):
    N = len(s)
    left, right = 0, 0
    max_len = 0
    count = {}

    while right < N:
      count[s[right]] = 1 + count.get(s[right], 0)

      while (right - left + 1) - max(count.values()) > k:
        count[s[left]] -= 1
        left += 1

      max_len = max(max_len, (right - left) + 1)
      right += 1

    return max_len
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(n) -> O(26) bec. it only contains uppercase characters

---

## 3. Binary Search

Given the sorted rotated array nums of **unique** elements, return the **minimum element** of this array.

#### Example:

- Input: nums = [3,4,5,1,2]
- Output: 1

#### Solution:

- Breakdown:

  1. Original Sorted: 1 2 3 4 5
  2. Rotated: 3 4 5 1 2
  3. 3 4 5 1 2
  4. nums[mid] = 5 > nums[right] = 2
  5. Remove everything before 5
  6. **1** 2 (lowest is 1)

- Steps:

  - Typical binary search using 2 pointers
  - Find the middle pointer in the list
  - If the value at mid is > than the value at right then move left to be at mid + 1
  - Otherwise move the right pointer to mid
  - Return The first element of the founded sub list as it would be sorted, thus getting the minimum element

- Code:

  ```python
  def findMin(nums):
    N = len(nums)
    left, right = 0, N - 1

    while left < right:
      mid = left + (right - left) // 2

      if nums[mid] > nums[right]:
        left = mid + 1

      else:
        right = mid

    return nums[left]
  ```

- Big-O:
  - Time Complexity: O(log n)
  - Space Complexity: O(1)

---

Given the sorted rotated array nums that may **contain duplicates**, return the **minimum element** of this array.

#### Example:

- Input: nums = [2,2,2,0,1]
- Output: 0

#### Solution:

- Steps:

  - Same steps as the last question but instead introduce a check where if the value at mid is == to the value at right, then decrement the right pointer to ensure it's the right index if the value's duplicated

- Code:

  ```python
  def findMin(nums):
    N = len(nums)
    left, right = 0, N - 1

    while left < right:
      mid = left + (right - left) // 2

      if nums[mid] > nums[right]:
        left = mid + 1

      elif nums[mid] < nums[right]:
        right = mid

      else:
        right -= 1

    return nums[left]
  ```

- Big-O:
  - Time Complexity: O(log n)
  - Space Complexity: O(1)

---

Given a characters array letters that is sorted in non-decreasing order and a character target, return the **smallest character** in the array that is **larger than target**.

#### Example:

- Input: letters = ["c","f","j"], target = "c"
- Output: "f"

#### Solution:

- Breakdown:

  1. c . f . j
  2. "f" is greater than the target "c" so we return "f"

- Steps:

  - Initialize left and right pointers
  - Initialize a variable to hold the smallest character at the 0th index
  - Loop through the list while left is <= right
  - Get the mid pointer
  - If the letter at the mid pointer is <= to the target, then assign left to be mid + 1
  - Otherwise assign the smallest letter to be the letter at the mid point
  - Assign right to be mid - 1
  - Return the smallest letter in the list

- Code:

  ```python
  def nextGreatestLetter(nums):
    N = len(nums)
    left, right = 0, N - 1
    smallest = letters[0]

    while left <= right:
      mid = left + (right - left) // 2

      if letters[mid] <= target:
        left = mid + 1

      else:
        smallest = letters[mid]
        right = mid - 1

    return smallest
  ```

- Big-O:
  - Time Complexity: O(log n)
  - Space Complexity: O(1)

---

A peak element is an element that is strictly greater than its neighbors.

Given an integer array nums, **find a peak element, and return its index**. If the array contains multiple peaks, return the index to any of the peaks.

#### Example:

- Input: nums = [1,2,1,3,5,6,4]
- Output: 5 **or** 1 (peaks from the left and right side of the middle index)

#### Solution:

- Breakdown:

  1. 1 2 1 3 5 6 4 <br>
     l ..... m <br>
     ................. r <br>

  2. 1 2 1 3 5 6 4 <br>
     ....... m l <br>
     ................. r <br>
     (nums[mid] <= nums[mid+1], so left will be mid + 1, meaning we'll solely look at everything **after** the mid point)

  3. Biggest value in this list is 6 which is at index 5, so we would return 5

- Steps:

  - Initialize left and right pointers
  - Loop through the list while left is <= right
  - Get the mid point
  - Check if nums[mid] is <= nums[mid + 1], if it is then update the position of left to be mid + 1
  - Otherwise assign the right pointer to be the mid point
  - Return either the left or right pointers, dependent on which side of the list we'll be looking at

- Code:

  ```python
  def findPeakElement(nums):
    N = len(nums)
    left, right = 0, N - 1

    while left <= right:
      mid = left + (right - left) // 2

      if nums[mid] <= nums[mid + 1]:
        left = mid + 1

      else:
        right = mid

    return left or right
  ```

- Big-O:
  - Time Complexity: O(log n)
  - Space Complexity: O(1)

---

Given the array nums **after the possible rotation** and an integer target, **return the index of target if it is in nums**, or -1 if it is not in nums.

#### Example:

- Input: nums = [4,5,6,7,0,1,2], target = 0
- Output: 4 (return the index of 0)

#### Solution:

- Steps:

  - Initialize left and right pointers
  - Loop through the list while left is <= right
  - Get the mid point
  - If the value at the mid point is == to the target then return mid directly
  - Check if nums[mid] is >= nums[left]
  - If it is then have another check and see if nums[mid] is < than the target **or** if nums[left] is > than the target
  - If it satisfies the conditions above the move left to be mid + 1
  - Otherwise move right to be mid - 1
  - If nums[mid] is < than nums[left]
  - Check if nums[mid] is > than the target **or** if nums[right] is < than the target
  - If the conditions are met then move right to be mid - 1
  - Otherwise assign left to be mid + 1
  - Return -1 if we couldn't find the target

- Code:

  ```python
  def search(nums, target):
    N = len(nums)
    left, right = 0, N - 1

    while left <= right:
      mid = left + (right - left) // 2

      if nums[mid] == mid:
        return mid

      if nums[mid] >= nums[left]:
        if nums[mid] < target or nums[left] > target:
          left = mid + 1
        else:
          right = mid - 1

      else:
        if nums[mid] > target or nums[right] < target:
          right = mid - 1
        else:
          left = mid + 1

    return -1
  ```

- Big-O:
  - Time Complexity: O(log n)
  - Space Complexity: O(1)

---

Given an array of integers nums sorted in non-decreasing order, find the **starting** and **ending** position of a given target value.

If target is not found in the array, return [-1, -1].

#### Example:

- Input: nums = [5,7,7,8,8,10], target = 8
- Output: [3,4]

#### Solution:

- Steps:

  - Have a seperate function to perform binary search
  - Initialize a left and right pointer, and a firstPos variable that holds N
  - Loop through the list while left is <= than right
  - Initialize the mid point
  - If the value at the mid point is less than the target, move left to be mid + 1
  - Otherwise assign the firstPos of the list to be the mid point, and the right to be mid - 1
  - return the firstPos
  - On the main function, initialize the first position element to be assigned to the search function assigned above, simply holds the nums[] and target
  - The last position element would hold nums[], and the last target value (target + 1) - 1
  - If the first element is <= the last element then return a new list holding both first and last indices [first, last]
  - Otherwise return [-1, -1]

- Code:

  ```java
  static int search(int[] nums, int target) {
    int N = nums.length;
    int left = 0, right = N - 1;
    int firstPos = N;

    while (left <= right) {
      int mid = left + (right - left) / 2;

      if (nums[mid] < target) {
        left = mid + 1;
      } else {
        firstPos = mid;
        right = mid - 1;
      }
    }
    return firstPos;
  }

  public int[] searchRange(int[] nums, int target) {
    int first = search(nums, target);
    int last = search(nums, target + 1) - 1;

    if (first <= last) return new int[] {first, last};

    return new int[] {-1, -1};
  }
  ```

- Big-O:
  - Time Complexity: O(log n)
  - Space Complexity: O(1)

---

Given a sorted integer array arr, two integers k and x, return the **k closest integers to x in the array**. The result should also be sorted in ascending order.

#### Example:

- Input: arr = [1,2,3,4,5], k = 4, x = 3
- Output: [1,2,3,4]

#### Solution:

- Breakdown:

  - Pretty much take the "target" element x, and get the numbers closest to it on both sides (left and right). k resembles the amount of elements we have to have in the list. In the constraints if left closest element is equal to the right closest element, **always** take left first.

- Code:

  ```java
  public List<Integer> findClosestElements(int[] arr, int k, int x) {
    int N = arr.length;
    int left = 0, right = N - k;
    List<Integer> res = new LinkedList<>();

    while (left < right) {
      int mid = left + (right - left) / 2;

      // Comparing the distances between left, x and right
      // If the distance between left and x is LARGER than x and right
      // Shift left to the right side, and vice versa
      if (x - arr[mid] > arr[mid + k] - x) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }

    // Add the elements closest to x to the new list
    for (int i = left; i < left + k; ++i)
      res.add(arr[i]);

    return res;
  }
  ```

- Big-O:
  - Time Complexity: O(log (n - k))
  - Space Complexity: O(k)

---

## 4. Fast & Slow Pointers

Given the head of a linked list, determine if the linked list has a **cycle** in it.

#### Example:

- Input: head = [3,2,0,-4], pos = 1
- Output: true (both pointers eventually connect as the 1st node)

#### Solution:

- Breakdown:

  - Floyd's Tortoise and Hare Algorithm: The algorithm is split into 2 pointers, a slow and fast pointer. The fast pointer moves 2 spots wheras the slow pointer moves 1 spot. Because the fast pointer moves twice as fast there's a high possibility in one of its rounds that it is at the same spot as the slow pointer. If it is then we've found a cycle.

- Code:

  ```java
  public boolean hasCycle(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
      slow = slow.next;
      fast = fast.next.next;

      if (slow == fast) return true;
    }
    return false;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given the head of a linked list, **return the node** where the **cycle begins**. If there is no cycle, return **null**.

#### Example:

- Input: head = [3,2,0,-4], pos = 1
- Output: index 1

#### Solution:

- Steps:

  - Implementing the Floyd's Tortoise and Hare Algorithm
  - Base case: check if head or head.next are null, if they are then return null
  - Initialize a slow and fast pointer and assign them to head
  - Loop through the list while fast and fast.next are not null
  - Move slow pointer by 1
  - Move fast pointer by 2
  - If slow is == to fast then reset the slow pointer
  - Have a loop to check whether slow is != fast
  - Move the slow pointer by 1
  - Move the fast pointer by 1
  - Exit the loop and return slow
  - Otherwise return null as we have not found a cycle

- Code:

  ```java
  public ListNode detectCycle(ListNode head) {
    if (head == null || head.next == null) return null
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
      slow = slow.next;
      fast = fast.next.next;

      if (slow == fast) {
        // Reset slow
        slow = head;
        while (slow != fast) {
          slow = slow.next;
          fast = fast.next;
        }
        return slow;
      }
    }
    return null;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given the head of a singly linked list, return the **middle node** of the linked list.

If there are **two middle nodes, return the second middle node.**

#### Example:

- Input: head = [3,2,0,-4], pos = 1
- Output: index 1

#### Solution:

- Breakdown:

  - Because the fast pointer moves twice as fast, every time it goes out of bounds the slow pointer automatically ends up in the middle, and if there are 2 middle nodes it'll always end up on the second one.

- Code:

  ```java
  public ListNode middleNode(ListNode head) {
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
      slow = slow.next;
      fast = fast.next.next;
    }
    return slow;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given the head of a singly linked list, return true if it is a **palindrome**.

#### Example:

- Input: head = [1,2,2,1]
- Output: true

#### Solution:

- Breakdown:

  - **Reverse the second half** of the list and compare the elements, if they're equal then it's a palindrome.

- Code:

  ```java
  public boolean isPalindrome(ListNode head) {
    // Base case
    if (head == null || head.next == null) return true;
    ListNode slow = head;
    ListNode fast = head;

    while (fast != null && fast.next != null) {
      slow = slow.next;
      fast = fast.next.next;
    }

    ListNode left = head;
    ListNode right = reverse(slow);

    while (right != null) {
      // Move both pointers to their next element until they're all equal
      if (left.val == right.val) {
        left = left.next;
        right = right.next;
      } else {
        return false;
      }
    }
    return true;
  }

  private ListNode reverse(ListNode head) {
    // Base case
    if (head == null || head.next == null) return head;
    ListNode prev = null, next = null;

    for (ListNode curr = head; curr != null; curr = next) {
      next = curr.next;
      curr.next = prev;
      prev = curr;
    }
    return prev;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

You are given the head of a singly linked-list. **Reorder the list** to be on the following form: <br>
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …

#### Example:

- Input: head = [1,2,3,4,5]
- Output: [1,5,2,4,3]

#### Solution:

- Breakdown:

  - 1 2 3 4 5 <br>
    ..... s (Slow pointer ends up in the middle when the fast pointer is out of bounds)
  - Split the list into 2 halves
    - 1->2->null
    - 3->4->5
  - Break the list, assign its next to null, then reverse the second half
    - 1->2->null
    - 5->4->3->null
  - Now point each node in the first half with its corresponding position in the second half
  - Output: 1->5->2->4->3

- Code:

  ```java
  public void reorderList(ListNode head) {
    // Base case
    if (head == null || head.next == null) return;
    ListNode slow = head;
    ListNode fast = head;
    ListNode prev = null;

    // Move the slow pointer to be the middle node
    while (fast != null && fast.next != null) {
      prev = slow;
      slow = slow.next;
      fast = fast.next.next;
    }

    // Break list and assign its tail to be null
    prev.next = null;

    // Assigning the head and tail of the second half
    ListNode left = head, right = reverse(slow);
    while (left != null && right != null) {
      // Have a reference to the next nodes of the new list
      ListNode nextLeft = left.next;
      ListNode nextRight = right.next;
      // Assigning the node in the first half to point to the corresponding node in the second half
      left.next = right;
      right.next = nextLeft == null ? nextRight : nextLeft;
      // Move to the next pointers and do the same operation till it's done
      left = nextLeft;
      right = nextRight;
    }
  }

  private ListNode reverse(ListNode head) {
    // Base case
    if (head == null || head.next == null) return head;
    ListNode prev = null, next = null;
    ListNode curr = head;

    for (; curr != null; curr = next) {
      next = curr.next;
      curr.next = prev;
      prev = curr;
    }
    return prev;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

## 5. Linked List

You are given two non-empty linked lists representing two non-negative integers. **The digits are stored in reverse order**, and each of their nodes contains a single digit. **Add the two numbers and return the sum** as a linked list.

#### Example:

- Input: l1 = [2,4,3], l2 = [5,6,4]
- Output: [7,0,8] (342 + 465 = 807)

#### Solution:

- Steps:

  - Initialize a dummy node to hold the previous node in the list
  - Initialize a carry over variable for all numbers added that are >= 10
  - Loop through the lists while they're not null, or the carry over is not 0
  - Get the values of both lists
  - Calculate the sum using those 2 values as well as whatever carry over element there is
  - Afterwards calculate the carry over by dividing the sum by 10
  - Then assign another node to be the current node, holing the sum % 10
  - Based off that we found a carry over elemenet, so we assign the prev.next to be the current node
  - Now update the pointers by assigning prev to curr
  - and move the pointers of both lists to the next element to calcuate them
  - Return dummy.next to get all the elements we've found

- Code:

  ```java
  public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode();
    ListNode prev = dummy;
    int carry = 0;

    while (l1 != null || l2 != null || carry != 0) {
      int val1 = l1 != null ? l1.val : 0;
      int val2 = l2 != null ? l2.val : 0;
      int sum = val1 + val2 + carry;

      // Find the carry overs
      carry = sum / 10;
      ListNode curr = new ListNode(sum % 10);
      prev.next = curr;

      // Update pointers
      prev = curr;
      l1 = l1 != null ? l1.next : null;
      l2 = l2 != null ? l2.next : null;
    }
    return dummy.next;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given the head of a singly linked list, **group all the nodes with odd indices together followed by the nodes with even indices**, and return the reordered list.

The first node is considered odd, and the second node is even, and so on.

#### Example:

- Input: head = [2,1,3,5,6,4,7]
- Output: [2,3,6,7,1,5,4] (odd indices first, then even)

#### Solution:

- Breakdown:

  - We'll have 3 nodes, 1 holds the odd indices which would be head, the other would hold even indices which would start at head.next, and a third to get the head of the even portion of the list. With that we'll move through the list and group them by getting their next.next index, after looping through it we'll get the odd.next (which is even) and assign it to evenHead and return the head

- Code:

  ```java
  public ListNode oddEvenList(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode odd = head;
    ListNode even = head.next;
    ListNode evenHead = even;

    while (even != null && even.next != null) {
      odd.next = odd.next.next;
      even.next = even.next.next;

      odd = odd.next;
      even = even.next;
    }
    odd.next = evenHead;
    return head;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given the heads of two singly linked-lists headA and headB, return **the node at which the two lists intersect**. If the two linked lists have no intersection at all, return null.

#### Example:

- Input: headA = [1,9,1,2,4], headB = [3,2,4]
- Output: 2

#### Solution:

- Breakdown:

  - So we can remove the added complexity of calculating both lengths and finding the intersections that way, we could instead wait until the lists reach the end (null) and assign them to the head of the other list, this way we can iterate however many times needed until we find an intersection, if we don't then return null

- Code:

  ```java
  public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    if (headA == null || headB == null) return null;
    ListNode l1 = headA;
    ListNode l2 = headB;

    while (l1 != l2) {
      l1 = l1 != null ? l1.next : headB;
      l2 = l2 != null ? l2.next : headA;
    }
    // We could return either l1 or l2
    return l1;
  }
  ```

- Big-O:
  - Time Complexity: O(n + m)
  - Space Complexity: O(1)

---

You are given a **doubly linked list**, which contains nodes that have a next pointer, a previous pointer, and an additional child pointer. Given the head of the first level of the list, **flatten the list so that all the nodes appear in a single-level, doubly linked list**. Return the head of the flattened list. The nodes in the list must have all of their child pointers set to null.

#### Example:

- Input: head = [1,2,null,3]
- Output: [1,3,2]

#### Solution:

- Breakdown:

  - <img src="https://assets.leetcode.com/uploads/2021/11/09/flatten2.1jpg" width="200px">

  - We'll always store 2 values in the **stack** if they're not null, the **next** node and the **child** node. Because we're trying to flatten the list the **child** node comes first, so we pop it out of the stack and make it the new next pointer, we'll do this for all levels until we have no child nodes, after we're done with the child nodes we'll add the rest of the original **next** nodes

- Code:

  ```java
  public Node flatten(Node head) {
    if (head == null) return head;
    Node dummy = new Node();
    Node prev = dummy;

    Stack<Node> stack = new Stack<>();
    stack.push(head);

    while (!stack.isEmpty()) {
      Node curr = stack.pop();

      if (curr.next != null) stack.push(curr.next);
      if (curr.child != null) stack.push(curr.child);

      // Resetting and updating pointers
      prev.next = curr;
      curr.prev = prev;
      curr.child = null;
      prev = curr;
    }
    dummy.next.prev = null;
    return dummy.next;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(n)

---

Given the head of a linked list and a value x, **partition it** such that all nodes less than x come before nodes greater than or equal to x.

You should p**reserve the original relative order of the nodes** in each of the two partitions.

#### Example:

- Input: head = [1,4,3,2,5,2], x = 3
- Output: [1,2,2,4,3,5]

#### Solution:

- Breakdown:

  - Have 2 lists, one that contains the values that are **<** than x, and the other has values that are **>=** x. Pretty much we'll go one node at a time and compare it to x, then add it to its respective list. Afterwards we'll merge both lists and at the end assign the **high** list to contain **null** at its last pointed node.
  - low: 1->2->2
  - high: 4->3->5->null
  - Ans: 1->2->2->4->3->5

- Code:

  ```java
  public ListNode partition(ListNode head, int x) {
    // Base case
    if (head == null) return head;

    // Assigning the new sub lists
    ListNode p1 = new ListNode(), p2 = new ListNode();
    ListNode low = p1, high = p2;

    ListNode curr = head;

    while (curr != null) {
      if (curr.val < x) {
        low.next = curr;
        low = curr;
      } else {
        high.next = curr;
        high = curr;
      }
      curr = curr.next;
    }
    // Merge lists
    low.next = p2.next;
    high.next = null;

    return p1.next;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given the head of a linked list, return the list after **sorting it** in ascending order.

#### Example:

- Input: head = [4,2,1,3]
- Output: [1,2,3,4]

#### Solution:

- Breakdown:

  - Apply the **Merge Sort Algorithm** by splitting the list in half, sort each half then merge both lists.

- Code:

  ```java
  public ListNode sortList(ListNode head) {
    if (head == null || head.next == null) return head;
    // Splitting the list in half
    ListNode left = head;
    ListNode right = getMidNode(head);

    // After getting the middle node, we need to make sure the first node in the second half is right.next
    ListNode curr = right.next;
    right.next = null;
    right = curr;

    // Sort both lists
    left = sortList(left);
    right = sortList(right);

    // Merge both lists
    return merge(left, right);
  }

  private ListNode getMidNode(ListNode head) {
    ListNode slow = head;
    ListNode fast = head.next;

    while (fast != null && fast.next != null) {
      slow = slow.next;
      fast = fast.next.next;
    }
    return slow;
  }

  private ListNode merge(ListNode left, ListNode right) {
    ListNode dummy = new ListNode();
    ListNode curr = dummy;

    while (left != null && right != null) {
      // If the value of left is less, then point the new list.next to be the left node, then move to the next node. Same with right.
      if (left.val < right.val) {
        curr.next = left;
        left = left.next;
      } else {
        curr.next = right;
        right = right.next;
      }
      curr = curr.next;
    }

    // Combine the elements to the list
    if (left != null) curr.next = left;
    if (right != null) curr.next = right;

    return dummy.next;
  }
  ```

- Big-O:
  - Time Complexity: O(n logn)
  - Space Complexity: O(logn)

---

You are given an array of k linked-lists lists, each linked-list is **sorted in ascending order**.

**Merge all the linked-lists** into one sorted linked-list and return it.

#### Example:

- Input: lists = [[1,4,5],[1,3,4],[2,6]]
- Output: [1,1,2,3,4,4,5,6]

#### Solution:

- Breakdown:

  - 1->4->5, <br>
    1->3->4, <br>
    2->6
  - Take the first element from all 3 lists
  - Min Heap: 1 1 2 (All 3 are pointing to different nodes, so we **pop** the one at the top (first/lowest node) and add whichever node it's pointing at
  - curr: 1
  - Min Heap: 1 2 4 (Always in ascending order)
  - curr: 1->1
  - Min Heap: 2 3 4
  - curr: 1->1->2
  - Min Heap: 3 4 6
  - curr: 1->1->2->3
  - We keep doing it until we add all the nodes, The min heap has to **ALWAYS** have the lowest node at the **top**

- Code:

  ```java
  public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> minHeap = new PriorityQueue<>((a, b) -> a.val - b.val);

    // Adding the nodes to the heap
    for (ListNode node : lists) {
      if (node != null) minHeap.add(node);
    }

    ListNode dummy = new ListNode();
    ListNode curr = dummy;

    while (!minHeap.isEmpty()) {
      // Popping out the top element in the heap bec. it's the lowest
      ListNode top = minHeap.poll();
      // Assigning the node thats been popped as the next node pointed from curr
      curr.next = top;
      curr = curr.next;

      // Adding the next pointed node from top to the heap
      if (top.next != null) minHeap.add(top.next);
    }
    return dummy.next;
  }
  ```

- Big-O:
  - Time Complexity: O(n logk)
  - Space Complexity: O(n)

---

Given the head of a singly linked list, **reverse the list**, and return the reversed list.

#### Example:

- Input: head = [1,2,3,4,5]
- Output: [5,4,3,2,1]

#### Solution:

- Code:

  ```java
  public ListNode reverseList(ListNode head) {
    if (head == null) return head;

    ListNode curr = head;
    ListNode prev = null;
    ListNode next = null;

    for (; curr != null; curr = next) {
      next = curr.next;
      curr.next = prev;
      prev = curr;
    }
    return prev;
  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---

Given the head of a singly linked list and two integers left and right where left <= right, **reverse the nodes of the list from position left to position right**, and return the reversed list.

#### Example:

- Input: head = [1,2,3,4,5], left = 2, right = 4
- Output: [1,4,3,2,5]

#### Solution:

- Breakdown:

  - 1->

- Code:

  ```java
  public ListNode reverseBetween(ListNode head, int left, int right) {

  }
  ```

- Big-O:
  - Time Complexity: O(n)
  - Space Complexity: O(1)

---
