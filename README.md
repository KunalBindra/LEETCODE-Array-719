# LEETCODE-Array-719
Let’s walk through the provided Java code to understand how it works, specifically for the problem of finding the k-th smallest distance pair in an array of integers. I’ll explain the components of the code and perform a dry run using an example.

### Code Explanation

1. **Sorting the Array**: The function begins by sorting the array `nums`. Sorting is crucial because it allows us to efficiently calculate distances between pairs.

2. **Binary Search for Distance**: We initialize two pointers, `l` and `r`. 
   - `l` starts at 0 (the minimum possible distance).
   - `r` is set to the maximum distance, which is the difference between the largest and smallest elements in the array (`nums[nums.length - 1] - nums[0]`).

3. **Finding the k-th Smallest Distance**:
   - A binary search is performed on the distance values.
   - For each midpoint `m`, we use the helper function `numPairDistancesNoGreaterThan` to count how many pairs have distances no greater than `m`.
   - If the count is greater than or equal to `k`, it means we need to look for smaller distances (update `r` to `m`).
   - Otherwise, we look for larger distances (update `l` to `m + 1`).

4. **Counting Valid Pairs**: The method `numPairDistancesNoGreaterThan` counts how many pairs `(i, j)` exist such that `|nums[j] - nums[i]| <= m`. It uses a two-pointer technique to efficiently count pairs.

### Dry Run Example

Let’s take a simple example to illustrate how the code works.

**Input**: `nums = [1, 3, 1], k = 1`

1. **Sorting**: The sorted array becomes `[1, 1, 3]`.

2. **Initial Values**:
   - `l = 0`
   - `r = 3 - 1 = 2`

3. **First Iteration of Binary Search**:
   - Calculate `m = (0 + 2) / 2 = 1`.
   - Call `numPairDistancesNoGreaterThan(nums, 1)`:
     - Initialize `count = 0`, `j = 1`.
     - For `i = 0`, `j` increments while `nums[j] <= nums[0] + 1` (i.e., `1 + 1`):
       - `j = 1`: `1 <= 2` (increment `j`)
       - `j = 2`: `3 <= 2` (stop)
       - Count pairs: `count += j - i - 1 = 1 - 0 - 1 = 0`
     - For `i = 1`:
       - `j` stays at 2 (since `nums[1] + 1` is still `2`).
       - Count pairs: `count += j - i - 1 = 2 - 1 - 1 = 0`
     - For `i = 2`:
       - `j` stays at 2.
       - Count pairs: `count += j - i - 1 = 2 - 2 - 1 = -1` (not valid).
     - Total `count = 2`.
   - Since `2 >= 1`, we update `r = 1`.

4. **Second Iteration**:
   - Calculate `m = (0 + 1) / 2 = 0`.
   - Call `numPairDistancesNoGreaterThan(nums, 0)`:
     - For each index `i`, since we are looking for pairs with distance `0`, we find that:
       - For `i = 0`, `j` remains `1`: `count = 0`.
       - For `i = 1`, `j` remains `2`: `count = 0`.
       - For `i = 2`, `j` is 2: `count = 0`.
     - Total `count = 0`.
   - Since `0 < 1`, we update `l = 1`.

5. **Termination**: Now `l` is not less than `r`, so we return `l` (which is `1`).

### Final Output

For the input `nums = [1, 3, 1]` and `k = 1`, the function returns `1`, which is the k-th smallest distance pair.

### Summary

The provided code efficiently finds the k-th smallest distance between pairs of elements in a sorted array using a combination of sorting, binary search, and a two-pointer technique for counting. The dry run demonstrates the algorithm step by step, clarifying its logic and workings.
