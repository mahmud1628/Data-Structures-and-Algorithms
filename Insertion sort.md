# Insertion sort
***
 * Efficient algorithm for sorting a small number of elements

### Input:
A sequence of n numbers.
### Output:
The input sequence in non-decreasing order.


```cpp
#include<iostream>
#include<vector>
using namespace std;

template<typename E> void insertion_sort(vector<E> & a) {
    int n = a.size();
    for(int i = 1; i < n ; i++) {
        E t = a[i];
        int j = i-1;
        while(j >= 0 && a[j] > t) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = t;
    }
}

int main() {
    vector<int> a = {6,4,5,1,3,2,9,4,8,0};
    insertion_sort(a);
    for(auto i : a) {
        cout << i << " ";
    }
    return 0;
}
```

#### Time complexity: O(n<sup>2</sup>)
#### Space complexity: O(1)