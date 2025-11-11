## We are given an array `arr` of `n` elements. We need to sort the array in non-decreasing order.

## Idea: Pick an element in the array and move it to the left until it finds a smaller element on the left. Moving the element to the left is done in abstraction by actually shifting the larger elements on the right and at last placing the element at its correct position in the sorted sequence.

```c
#include <stdio.h>

void insertion_sort(int *arr, int length)
{
  for(int index = 1; index < length; index++) // for each element in the array
  {
 	int element = *(arr + index); // take the element
 	int prev_index = index - 1; // take its previous index
 	while(prev_index >= 0 && *(arr + prev_index) > element) // do while the previous element is greater then the choosen element
 	{
		*(arr + prev_index + 1) = *(arr + prev_index); // shift the previous element one position right
		prev_index--; // assuming the choosen element has been moved to the "prev_index" position, decrement "prev_index"
 	}
	*(arr + prev_index + 1) = element; // move the choosen element to its correct positin in the sorted sequence
  }
}

int main(void)
{
	int n;
	scanf("%d", &n);
	int arr[n];
	for(int i = 0; i < n; i++)
	{
		scanf("%d", &arr[i]);
	}
	insertion_sort(arr, n);
	for(int i = 0; i < n; i++)
	{
		printf("%d ", arr[i]);
	}
	return 0;
}
```

### Time complexity : O(n<sup>2</sup>)
### Space complexity : O(1)
