# leetcode 739 每日温度

对于每个元素，求其后面的比它大的元素中离它最近的一个。经典的单调栈题目。

单调栈最基础的作用，就是对于数组中每个元素，求其前面（或者后面）比它小（或者大）的元素中离它最近的一个。

具体到这一题，就是反向遍历数组，维护一个递减的单调栈。

时间复杂度是$`O(n)`$，因为每个元素会入栈一次，最多出栈一次。

```c++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        stack<int> st;	// 栈里面存的是元素下标，因为求的是元素之间的距离
    
        int n = temperatures.size();
        vector<int> res(n);

        for(int i = n - 1; i >= 0; i --){
            while(st.size() && temperatures[st.top()] <= temperatures[i])
                st.pop(); // 弹出所有比当前值小的元素
            
            if(st.empty()) res[i] = 0; // 栈空说明后面没有比它大的元素
            else res[i] = st.top() - i;	

            st.push(i);	
        }
        return res;
    }
};
```

