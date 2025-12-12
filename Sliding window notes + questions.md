# 🚀 SLIDING WINDOW — COMPLETE NOTES

## ✅ 1. When to think of Sliding Window

Use sliding window when:

- You need something about subarrays / substrings that are contiguous.
    
- Window size is either:
    

- Fixed (k given)
    
- Variable (expand–shrink until some condition holds)
    

- You need to maintain something like:
    

- Sum
    
- Count
    
- Max/Min
    
- Frequency
    
- Distinct elements
    
- K unique
    
- Longest/shortest valid window
    

Key idea: Move left and right pointers, add on the right, remove on the left.

---

## ✅ 2. Why maintain a frequency map / array?

Maintaining frequencies helps you track how many of each element are inside the window.

Used when:

- You need to check duplicates
    
- You need k distinct
    
- You need at most / exactly / at least K uniques
    
- You’re matching patterns (like anagram problems)
    
- "Window is valid if element counts satisfy some condition"
    

Benefits:

- Check validity of window in O(1)
    
- Efficiently shrink window
    
- Know how many times something entered/exited
    
- Avoid full rescanning of window every time
    

---

## ✅ 3. Fixed-size Sliding Window

Use when window size k is fixed.

Template:

l = 0

for r inrange(n):  
    add(arr[r])  
    if r - l + 1 > k:  
        remove(arr[l])  
        l += 1if r - l + 1 == k:  
        ans = update()

Use cases:

- Max sum of size k
    
- Count subarrays of size k with some condition
    
- Moving average
    

---

## ✅ 4. Variable-size Sliding Window

Expand r  
Shrink l until window becomes valid  
Keep track of max/min length.

Template:

l = 0

for r inrange(n):  
    add(arr[r])  
  
    while window_invalid():  
        remove(arr[l])  
        l += 1  
  
    ans = update()

Use cases:

- Longest substring without repeating chars
    
- Longest subarray with sum ≤ k
    
- At most k distinct
    
- Exactly k distinct → use:
    

- exactly(k) = atMost(k) - atMost(k-1)
    

---

## ✅ 5. Sliding Window with Frequency Array

Instead of dict, you use an array when:

- Values are small (like chars → 26, or ASCII → 256).
    
- Fast O(1) update.
    

Example: longest substring with no repeat  
(Frequency > 1 → shrink).

---

## ✅ 6. When Sliding Window DOES NOT work

- If subarray is not contiguous
    
- If order doesn't matter (use two pointers only for sorted)
    
- If you need a dynamic DP-like choice
    
- If removing from left changes the final condition in a non-monotonic way  
    (like sum that goes negative and breaks logic)
    

---

## ✅ 7. Key Pattern Recognition

Always think Sliding Window when:

- “Longest / shortest subarray…”
    
- “At most k …”
    
- “Exactly k …”
    
- “First window of size k…”
    
- “Number of substrings…”
    
- “Find subarray with sum ≤ / ≥ target”
    
- “Check duplicates in a window of size k”
    

More formally:

### Valid window condition must be MONOTONIC

Meaning:

- If window becomes invalid when expanding → shrinking will fix it.
    

---

## 📌 QUICK CHEATSHEET (super short)**

|Problem Type|Approach|
|---|---|
|Fixed size k|Move r, maintain size, remove l when needed|
|Longest valid window|Expand r, shrink l until valid|
|K distinct|freq + shrink if distinct > k|
|No duplicates|freq + shrink if freq[x] > 1|
|Minimum window substring|Expand until valid, shrink until breaking|
|Count subarrays with sum ≤ k|variable-sized + prefix|

---


A structure can look like:

start with including J in the result. 

then write the shrinking logic,
		while (when shrinking needs to be done):
			i+=1

THen we are at a place where answer can be possible. 

j+=1
