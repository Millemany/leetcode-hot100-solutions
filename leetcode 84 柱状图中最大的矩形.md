# leetcode 84 柱状图中最大的矩形

就是 [leetcode 42 接雨水](./leetcode 42 接雨水.md) 的变式。

对于某个柱子来说，想得到和它自身高度相同的矩形，那么就要想办法得到这个矩形的左右边界。

很明显，左边界就是它左边比它小的所有矩形里最近的一个；右边界就是它右边比它小的所有矩形里最近的一个。

因此这还是一个单调栈问题。

时间复杂度$O(n)$。

```c++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> st;

        int n = heights.size();
        vector<int> fr(n), bk(n);

        for(int i = 0; i < n; i ++){
            while(st.size() && heights[st.top()] >= heights[i]) st.pop();

            int t = st.size() ? st.top() : -1;
            fr[i] = i - t - 1;	// 求出对于每个元素，它左边最近的最小值下标

            st.push(i);
        }

        while(st.size()) st.pop();

        for(int i = n - 1; i >= 0; i --){
            while(st.size() && heights[st.top()] >= heights[i]) st.pop();

            int t = st.size() ? st.top() : n;
            bk[i] = t - i - 1;	// 求出对于每个元素，它右边最近的最小值下标

            st.push(i);
        }

        int m_area = -1;
        for(int i = 0; i < n; i ++){
            m_area = max(m_area, (fr[i] + bk[i] + 1) * heights[i]);
        }

        return m_area;
    }
};
```



上面的代码还可以做优化。

刚刚我们是对于每个元素，分别向左向右寻找边界。除此之外，还可以专门处理**以当前位置为右边界**的矩形。

从前向后遍历数组，维护一个递增的单调栈。由此可知，每当栈弹出元素的时候，就是栈顶`st.top()`第一次遇到了比自己小的柱子。所以`st.top()`弹出的时候，其高度`height[st.top()]`就是矩形的高度，当前位置`i`就是右边界。

至于左边界，就是弹栈之后的新栈顶元素。因为这个单调栈的作用就是找到每个元素的左边界。凡是比`st.top()`大的元素在它入栈的时候都已经被弹出了。

时间复杂度还是$O(n)$，但是只需要遍历一次。

```c++
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> st;
        heights.push_back(0);
        // 需要在尾部添加一个 0
        // 因为每次遍历，是以当前位置作为右边界结算的
        // 因此需要人为在最右侧添加一个最小右边界，做一个彻底结算

        int n = heights.size();
        int m_area = 0;

        for(int i = 0, h; i < n; i ++){
            while(st.size() && heights[st.top()] > heights[i]){
                // 这时候就不是 >= 了，而是 >
                // 因为当前高度和栈顶元素高度相等的时候，当前位置并不是右边界。
                h = heights[st.top()];
                st.pop();

                int left = st.size() ? st.top() : -1;
                m_area = max(m_area, (i - left - 1) * h);
            }
            st.push(i);
        }

        return m_area;
    }
};
```

