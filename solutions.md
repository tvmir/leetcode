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
