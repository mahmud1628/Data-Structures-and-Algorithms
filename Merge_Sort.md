# Merge Sort Algorithm (C Implementation)

## Overview
This program implements the **Merge Sort** algorithm in C — a classic **divide-and-conquer** sorting algorithm that efficiently sorts an array of integers in ascending order.

---

## Problem It Solves
The algorithm solves the **sorting problem** — arranging elements of an array in a particular order (ascending in this case).  
Formally, given an unsorted array `A` of `n` elements, the goal is to produce a sorted array such that:
```

A[0] ≤ A[1] ≤ A[2] ≤ ... ≤ A[n - 1]

```

---

```c
#include <stdio.h>
#include <stdlib.h>


void merge(int * arr, int p, int q, int r)
{
	int n1 = q - p + 1;
	int n2 = r - q;
	int * left = (int *) malloc(n1 * sizeof(int));
	int * right = (int *) malloc(n2 * sizeof(int));
	for(int i = 0; i < n1; i++) left[i] = arr[p + i];
	for(int i = 0; i < n2; i++) right[i] = arr[q + 1 + i];

	int left_index = 0, right_index = 0;

	for(int i = p; i <= r; i++)
	{
		if(left_index == n1)
		{
			arr[i] = right[right_index];
			right_index++;
		}
		else if(right_index == n2)
		{
			arr[i] = left[left_index];
			left_index++;
		}
			arr[i] = left[left_index];
			left_index++;
		}
		else if(right_index < n2 && left[left_index] >= right[right_index])
		{
			arr[i] = right[right_index];
			right_index++;
		}
	}
	free(left);
	free(right);
}

void merge_sort(int *arr, int start, int end)
{
	if(start >= end) return;
	int mid = (start + end) / 2;
	merge_sort(arr, start, mid);
	merge_sort(arr, mid + 1, end);
	merge(arr, start, mid, end);
}

int main()
{
	int n;
	scanf("%d", &n);
	int * arr = (int *) malloc(n * sizeof(int));
	for(int i = 0; i < n; i++) scanf("%d", &arr[i]);
	merge_sort(arr, 0, n - 1);
	for(int i = 0; i < n; i++) printf("%d ", arr[i]);
	free(arr);
	return 0;
}

```

## How It Works

### 1. **Divide**
The algorithm recursively splits the array into two halves until each subarray has only one element (which is trivially sorted).

### 2. **Conquer (Sort)**
Each half is individually sorted using recursive calls to `merge_sort()`.

### 3. **Combine (Merge)**
The two sorted halves are merged back together into a single sorted array using the `merge()` function.

---

## Function Details

### **`merge_sort(int *arr, int start, int end)`**
- **Purpose:** Recursively divides the array into halves and sorts them.
- **Steps:**
  1. If `start >= end`, return (base case — one element).
  2. Compute `mid = (start + end) / 2`.
  3. Recursively sort the left half: `merge_sort(arr, start, mid)`.
  4. Recursively sort the right half: `merge_sort(arr, mid + 1, end)`.
  5. Merge the two sorted halves using `merge(arr, start, mid, end)`.

---

### **`merge(int *arr, int p, int q, int r)`**
- **Purpose:** Merges two sorted subarrays `arr[p..q]` and `arr[q+1..r]` into a single sorted array.
- **Steps:**
  1. Create temporary arrays `left` and `right` for the two halves.
  2. Copy data from the original array into these temporary arrays.
  3. Use two pointers (`left_index`, `right_index`) to compare and merge elements back into the original array.
  4. Continue merging until all elements from both halves are combined.

---

## Example

**Input:**
```

5
4 2 5 1 3

```

**Process:**
```

Divide: [4,2,5,1,3] → [4,2,5] and [1,3]
Sort Left: [4,2,5] → [2,4,5]
Sort Right: [1,3]
Merge: [2,4,5] and [1,3] → [1,2,3,4,5]

```

**Output:**
```

1 2 3 4 5

```

---

## Time and Space Complexity

| Case | Time Complexity | Explanation |
|------|------------------|--------------|
| Best | O(n log n) | Always divides and merges balanced subarrays |
| Average | O(n log n) | Recursive divide-and-conquer process |
| Worst | O(n log n) | Same as best case (no performance degradation) |

**Space Complexity:** O(n) (due to temporary arrays `left` and `right`)

---

## Key Properties
- **Stable:** Yes (preserves order of equal elements)
- **In-place:** No (uses extra space)
- **Deterministic:** Yes (always produces the same result for the same input)
- **Efficient:** Performs well on large datasets

---

## Summary
Merge Sort is a **reliable**, **recursive**, and **efficient** sorting algorithm.  
It is particularly useful when stability is required and when dealing with **large datasets** where `O(n log n)` performance is desirable.
