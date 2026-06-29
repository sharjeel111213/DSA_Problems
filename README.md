# Problem 1
# LeetCode 1189 - Maximum Number of Balloons

## 📝 Problem Description
Given a string `text`, you want to use the characters of `text` to form as many instances of the word **"balloon"** as possible.

You can use each character in `text` **at most once**. Return the maximum number of instances that can be formed.

---

## 💡 Core Logic & Algorithm (The Bottleneck Concept)
To form a single instance of the word **"balloon"**, we require a specific frequency of characters:
* **'b'** $\rightarrow$ 1 required
* **'a'** $\rightarrow$ 1 required
* **'l'** $\rightarrow$ **2** required
* **'o'** $\rightarrow$ **2** required
* **'n'** $\rightarrow$ 1 required

The maximum number of complete words we can form is determined by the **limiting factor (bottleneck)**—the character that runs out first. Since the letters `'l'` and `'o'` appear twice in the target word, we must divide their total frequencies by 2 (using integer division) before finding the minimum constraint.


# Problem 02: Median of Two Sorted Arrays

## 📝 Problem Description

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall run time complexity must be **$O(\log(m+n))$**.

## 💡 Algorithmic Approach

To achieve the optimal **$O(\log(\min(m, n)))$** time complexity, a **Binary Search on Partitions** approach is utilized instead of merging the two arrays.

1. **Array Size Optimization:** Ensure that the binary search is always performed on the smaller array (`nums1`). This keeps the search space minimal.
2. **Binary Partitioning:** We divide both arrays into a left half and a right half such that:
   * The total number of elements in the combined left halves equals the total elements in the combined right halves.
   * `maxLeftX <= minRightY` and `maxLeftY <= minRightX`
3. **Median Calculation:** * If the combined length $(m + n)$ is **odd**, the median is the maximum element of the left halves: 

$\max(\text{maxLeftX}, \text{maxLeftY})$.
   * If the combined length is **even**, the median is the average of the maximum of the left halves and the minimum of the right halves: 
   
   $\frac{\max(\text{maxLeftX}, \text{maxLeftY}) + \min(\text{minRightX}, \text{minRightY})}{2.0}$.
