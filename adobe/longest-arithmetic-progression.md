# Longest Arithmetic Progression

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/longest-arithmetic-progression1019/1/#)

Given an array called A[] of sorted integers having no duplicates, find the length of the Longest Arithmetic Progression (LLAP) in it.

### Sample Input
```
6
1 7 10 13 14 19
```

### Sample Output
```
4
```

### Brute-force (TLE)
```cpp
class Solution {   
public:
    int AP_SIZE(int A[], int n, bitset<1000> selection) {
        
        int last_num, dif, size = 0;

        for(int i = 0; i < n; ++i) {
            if(size == 0 && selection[i]) {
                ++size;
                last_num = A[i];
            }
            else if(size == 1 && selection[i]) {
                ++size;
                dif = A[i] - last_num;
                last_num = A[i];
            }
            else if(size > 1 && selection[i]) {
                if(dif == A[i] - last_num) {
                    ++size;
                    dif = A[i] - last_num;
                    last_num = A[i];
                }
                else {
                    return 0;
                }
            }
        }
        return size;
    }

    int max_size(int A[], int n, int i, bitset<1000> selection) {

        if(i >= n) {
            return AP_SIZE(A, n, selection);
        }

        bitset<1000> new_selection = selection;
        new_selection[i] = 1;

        return max(max_size(A, n, i + 1, selection), max_size(A, n, i + 1, new_selection));
    }

    int lengthOfLongestAP(int A[], int n) {
        bitset<1000> selection(0);
        return max_size(A, n, 0, selection);
    }
};
```

### Brute-force with caching (TLE)
```cpp
class Solution {   
public:
    int AP_SIZE(int A[], int n, bitset<1000> selection) {
        
        int last_num, dif, size = 0;

        for(int i = 0; i < n; ++i) {
            if(size == 0 && selection[i]) {
                ++size;
                last_num = A[i];
            }
            else if(size == 1 && selection[i]) {
                ++size;
                dif = A[i] - last_num;
                last_num = A[i];
            }
            else if(size > 1 && selection[i]) {
                if(dif == A[i] - last_num) {
                    ++size;
                    dif = A[i] - last_num;
                    last_num = A[i];
                }
                else {
                    return 0;
                }
            }
        }
        return size;
    }

    int max_size(int A[], int n, int i, bitset<1000> selection, vector<unordered_map<bitset<1000>, int>>& cache) {

        if(i >= n) {
            // for(int k = 0; k < 6; ++k) {
            //     cout << selection[k];
            // }
            // cout << endl;
            return AP_SIZE(A, n, selection);
        }
        if(cache[i].count(selection)) return cache[i][selection];

        bitset<1000> new_selection = selection;
        new_selection[i] = 1;

        return cache[i][selection] = max(max_size(A, n, i + 1, selection, cache), max_size(A, n, i + 1, new_selection, cache));
    }

    int lengthOfLongestAP(int A[], int n) {
        bitset<1000> selection(0);
        vector<unordered_map<bitset<1000>, int>> cache(1000);
        return max_size(A, n, 0, selection, cache);
    }
};
```

<!-- ### Accepted -->
<!-- [![image](...image...)](...solution...) -->