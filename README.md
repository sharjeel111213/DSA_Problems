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

### Mathematical Formula:
$$\text{Max Balloons} = \min\left(\text{count}(b), \text{count}(a), \frac{\text{count}(l)}{2}, \frac{\text{count}(o)}{2}, \text{count}(n)\right)$$

---

## 🛠️ Code Implementation (Kotlin)

```kotlin
class Solution {
    fun maxNumberOfBalloons(text: String): Int {
        // Step 1: Initialize fixed-size frequency array for lowercase English letters
        val counts = IntArray(26)

        // Step 2: Populate frequencies for target characters
        for (char in text) {
            if (char in "balloon") {
                counts[char - 'a']++
            }
        }
        
        // Step 3: Extract individual counts and normalize duplicate characters
        val b = counts['b' - 'a']
        val a = counts['a' - 'a']
        val l = counts['l' - 'a'] / 2  // 'l' appears twice per word
        val o = counts['o' - 'a'] / 2  // 'o' appears twice per word
        val n = counts['n' - 'a']

        // Step 4: The bottleneck constraint decides the final answer
        return minOf(b, minOf(a, minOf(l, minOf(o, n))))
    }
}

fun main() {
    val solution = Solution()
    val testInput = "loonbalxballpoon"
    val result = solution.maxNumberOfBalloons(testInput)
    
    println("Input Text: $testInput")
    println("Output (Max Balloons): $result") // Output: 2
}
