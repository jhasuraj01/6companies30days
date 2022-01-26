# Course Schedule II

[![Problem Link](../assets/lc.svg)](https://leetcode.com/problems/course-schedule-ii/)

There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

- For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

### Example 1
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: [0,1]
```

### Example 2
```
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3]
```

### Solution
```cpp
class Solution {
public:
    bool topologicalSort(int course, vector<vector<int>> &courses, vector<int> &state, vector<int> &ans) {
        if(state[course] == 2) return true;
        if(state[course] == 1) return false;

        state[course] = 1; // visited

        for(auto prerequisites: courses[course]) {
            if(!topologicalSort(prerequisites, courses, state, ans)) {
                return false;
            }
        }

        ans.push_back(course);

        state[course] = 2; // completed

        return true;
    }

    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> courses(numCourses);
        vector<int> state(numCourses, 0);

        for(auto course: prerequisites) {
            courses[course[0]].push_back(course[1]);
        }

        vector<int> ans;

        for(int i = 0; i < numCourses; ++i) {
            if(state[i]) continue;
            if(!topologicalSort(i, courses, state, ans)) {
                return vector<int>(0);
            }
        }

        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/151199708-dd67adfc-cb15-499b-8edd-39aeec7bda7c.png)](https://leetcode.com/submissions/detail/628341320/)
