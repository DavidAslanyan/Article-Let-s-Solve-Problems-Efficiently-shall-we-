# Let's Solve Problems Efficiently, shall-we?

**Author:** David Aslanyan
**Reading time:** ~4 min    
 

When solving algorithmic problems, brute force solutions may work, but they’re rarely efficient.  
To stand out in coding interviews or competitive programming, it’s crucial to know **patterns and techniques** that reduce complexity and make your solutions elegant.

In this article, I’ll walk through some of the simplest yet useful techniques you can apply across strings, arrays, and number problems.  
Each section comes with a short description, code snippet, and where it’s commonly used.

## 1) Two Pointers
  
**Description:**  
The **two-pointer technique** uses one pointer at the start and another at the end of an array (or string).  
You move them towards each other while performing some checks or logic.  

This helps reduce nested loops (O(n²)) into linear time (O(n)).

**Example – Check if an Array is a Palindrome:**
```js
const isPalindrome = (arr) => {
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    if (arr[left] !== arr[right]) {
      return false;
    }
    left++;
    right--;
  }

  return true;
}
````

**Use cases:**

* Palindrome problems
* Pair sum problems (e.g., 2-sum in sorted array)
* Reversing arrays in place

---

## 2) In-Place Swapping of Elements

**Description:**
Instead of creating new arrays or strings, you can **swap elements in place** to save memory and keep complexity low.

**Example – Reverse a String:**

```js
var reverseString = function(s) {
  let left = 0;
  let right = s.length - 1;

  while (left < right) {
    let temp = s[left];
    s[left] = s[right];
    s[right] = temp;

    left++;
    right--;
  }

  return s;
};
```

**Use cases:**

* Reversing arrays or strings
* QuickSort partition logic
* Rotating arrays

---

## 3) Check if a Character is Alphanumeric

**Description:**
Sometimes you need to filter out only letters and digits when parsing strings.
Checking ASCII ranges is an efficient way.

**Example – Alphanumeric Check:**

```js
function isAlphaNumeric(char) {
  if (char.length !== 1) return false;
  if (char >= "0" && char <= "9") return true;
  const code = char.charCodeAt(0);

  return code >= 97 && code <= 122;
}
```

**Use cases:**

* Cleaning strings for palindrome checks
* Token validation
* Regex replacement in performance-sensitive cases

---

### Why is Regex not More Efficient Here?

**Regex approach:**

```js
function isAlphaNumeric(char) {
  return /^[a-z0-9]$/i.test(char);
}
```

* Very concise
* Under the hood, regex has to compile a pattern and run the regex engine.
  That’s extra overhead compared to a simple ASCII check.

**So, which one is really efficient?**

* In **tight loops** (e.g., scanning millions of characters) → `charCodeAt` is more performant.
* For **one-off checks** or **readability** → regex is fine.

**Rule of thumb:**

* Use **regex** when readability > micro-optimization.
* Use **charCodeAt / ASCII checks** when performance matters.

---

## 4) Storing Character Occurrences

**Description:**
When working with frequency counts, an **object (hash map)** is the fastest way to store how many times each character appears.

**Example – Count Characters:**

```js
const obj = {};
for (const char of s) {
  obj[char] = (obj[char] | 0) + 1;
}
```

**Use cases:**

* Anagram problems
* Character uniqueness checks
* Frequency analysis

---

## 5) Reverse Integers Purely

**Description:**
Instead of converting integers to strings, you can **reverse digits mathematically** using `%` and `/`.

**Example – Reverse Integer:**

```js
var reverse = function(x) {
  let result = 0;

  while (x !== 0) {
    let digit = x % 10;
    x = Math.trunc(x / 10);
    result = result * 10 + digit;
  }

  return result;
};
```

**Use cases:**

* Integer manipulation without extra memory
* Digit DP problems
* Palindrome numbers

---

## 6) Fixed Sliding Window

**Description:**
The **sliding window technique** is used to efficiently calculate something over a continuous subarray.
In the **fixed window**, the size (k) is constant.

**Example – Find Max Average Subarray:**

```js
var findMaxAverage = function(nums, k) {
  let curSum = 0;

  for (let i = 0; i < k; i++) {
    curSum += nums[i];
  }

  let maxAvg = curSum / k;

  for (let i = k; i < nums.length; i++) {
    curSum += nums[i] - nums[i - k];
    maxAvg = Math.max(maxAvg, curSum / k);
  }

  return maxAvg;
};
```

**Use cases:**

* Max/min subarray sums
* Moving averages
* Continuous sequence analysis

---

## 7) Dynamic Sliding Window

**Description:**
In a **dynamic window**, the size expands or shrinks depending on conditions.
This helps solve problems where the window length isn’t fixed.

**Example – Length of the Longest Substring Without Repeating Characters:**

```js
var lengthOfLongestSubstring = function(s) {
    const set = new Set();
    let left = 0;
    let max = 0;

    for (let right = 0; right < s.length; right++) {
        while (set.has(s[right])) {
            set.delete(s[left]);
            left++;
        }

        set.add(s[right]);
        max = Math.max(max, right - left + 1);
    }

    return max;
};
```

**Use cases:**

* Longest substring without repeating characters
* Minimum window substring
* Subarray sum problems

**More details on sliding windows:**
[The Sliding Window Algorithm and When We Should Use It](https://medium.com/@dav.aslanyan2003/the-sliding-window-algorithm-and-when-we-should-use-it-f26dd7c2eae5)

---

# Conclusion

These techniques are **reusable building blocks** that appear in many algorithmic problems.
By mastering them, you’ll not only speed up your problem-solving but also recognize patterns faster in coding interviews.

I hope you learned something useful today.
Thanks for reading my article, and keep learning! 🚀

---

```

---

Do you want me to also add a **summary table at the end** (Technique → Where it’s useful → Complexity) so readers can quickly reference it?
```

