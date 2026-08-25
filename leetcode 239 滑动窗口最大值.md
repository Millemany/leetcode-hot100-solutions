# leetcode 239 滑动窗口最大值

最经典的单调队列题目，不多解释。维护一个递减的单调队列，队头元素对应的值就是当前滑动窗口的最大值。

滑动窗口每次向右移动一格，先从队头移除所有不在窗口内的元素，然后入队新元素。凡是小于等于新元素的值全部从队尾弹出。

时间复杂度$O(n)$。

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> q(1e5 + 10, 0);
        vector<int> res;

        for(int i = 0; i < nums.size(); i ++){
            while(q.size() && q.front() <= i - k) q.pop_front();
            while(q.size() && nums[q.back()] <= nums[i]) q.pop_back();
            q.push_back(i);

            if(i >= k - 1) res.push_back(nums[q.front()]);
        }
        return res;
    }
};
```
