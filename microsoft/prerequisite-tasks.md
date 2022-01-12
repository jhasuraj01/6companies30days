# Prerequisite Tasks

[![Problem Link](../assets/gfg.svg)](https://practice.geeksforgeeks.org/problems/prerequisite-tasks/1/#)

There are a total of N tasks, labeled from 0 to N-1. Some tasks may have prerequisites, for example to do task 0 you have to first complete task 1, which is expressed as a pair: [0, 1]

Given the total number of tasks N and a list of prerequisite pairs P, find if it is possible to finish all tasks.

### Sample Input
```
4
3
1 0
2 1
3 2
```
### Sample Output
```
Yes
```

### Solution
```cpp
class Solution {
public:

    bool completeTask(int target, vector<vector<int>> &tasks, vector<int> &state) {

        if(state[target] == 2) {
            return true;
        }
        else if(state[target] == 1) {
            return false;
        }

        state[target] = 1; // visited

        for(auto task: tasks[target]) {
            bool done = completeTask(task, tasks, state);
            if(!done) {
                return false;
            }
        }

        state[target] = 2; // completed

        return true;
    }

	bool isPossible(int N, vector<pair<int, int> >& prerequisites) {
	    vector<vector<int>> tasks(N);
	    vector<int> state(N, 0);

	    for(auto task_pair: prerequisites) {
	        tasks[task_pair.first].push_back(task_pair.second);
	    }

        for(int i = 0; i < N; ++i) {
            bool done = completeTask(i, tasks, state);
            if(!done) {
                return false;
            }
        }

	    return true;
	}
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/149088955-394f5dea-4e42-40d2-8954-8c205e0db4cf.png)](https://practice.geeksforgeeks.org/viewSol.php?subId=9407a8a44472b1a5dbd29fd22e86ec5c&pid=702128&user=jhasuraj)
