# Find the missing no in string

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/find-the-missing-no-in-string/1/#)

Given a string consisting of some numbers, not separated by any separator. The numbers are positive integers and the sequence increases by one at each number except the missing number. The task is to complete the function missingNumber which return's the missing number. The numbers will have no more than six digits. Print -1 if input sequence is not valid.

**Note:** Its is guaranteed that if the string is valid, then it is sure that atleast one number would be missing from the string.

### Sample Input
```
1
1234567810111213141516
```

### Sample Output
```
9
```

### Solution
```cpp
int missingNumber(const string& str)
{
    int len = str.size();
    int max_window = min(6, len/2);

    for(int w = 1; w <= max_window; ++w) {
        int last_num = 0, num = 0;
        bool searching = true, solved = false;
        int missing_number;

        for(int i = 0; i < w; ++i) {
            last_num = last_num * 10 + str[i] - '0';
        }
        
        int window_size = (int) log10(last_num + 1) + 1;
        
        for(int d = w; d < len; d += window_size) {
            window_size = (int) log10(last_num + 1) + 1;
            num = 0;
            for(int i = 0; i < window_size; ++i) {
                num = num * 10 + str[d + i] - '0';
            }
            
            if(num != last_num + 1 && (int)log10(last_num + 1) < (int)log10(last_num + 2)) {
                num = 0;
                window_size = (int) log10(last_num + 2) + 1;
                for(int i = 0; i < window_size; ++i) {
                    num = num * 10 + str[d + i] - '0';
                }
            }

            if(num == last_num + 2) {
                if(searching) {
                    searching = false;
                    solved = true;
                    missing_number = last_num + 1;
                }
                else {
                    solved = false;
                    break;
                }
            }
            else if(num != last_num + 1) {
                solved = false;
                break;
            }
            last_num = num;
        }
        
        if(solved) {
            return missing_number;
        }
    }
    
    return -1;
}
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/150627354-0e9a6ba7-2f3b-452d-9e9a-5f9f387c900f.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=fe529bd2a37e75bfc3f73473c37b2595&pid=700489&user=jhasuraj)
