# leetcode 207 课程表

拓扑排序题目。类似于 bfs。

1. 先把入度为 0 的结点入队。
2. 然后依次出队，出队结点的终点入度减一。
3. 如果出现了新的入度为 0 的结点，再把它入队。
4. 循环往复前三步，直到队伍为空
5. 统计出队结点的数量，是否与全体结点数相等。相等的话说明存在拓扑序。

时间复杂度是$`O(m)`$，其中$`m`$是边的数量。

```c++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> gr(numCourses);
        vector<int> d(numCourses, 0);

        for(auto t: prerequisites){
            int b = t[0], a = t[1];
            gr[a].push_back(b);
            d[b] ++;
        }

        queue<int> q;
        for(int i = 0; i < numCourses; i ++)
            if(d[i] == 0) q.push(i);
        
        int cnt = 0;
        while(q.size()){
            int t = q.front();
            q.pop();
            cnt ++;
            for(auto b: gr[t]){
                d[b] --;
                if(d[b] == 0) q.push(b);
            }
        }

        return cnt == numCourses;
    }
};
```

