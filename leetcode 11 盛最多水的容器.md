# leetcode 11 盛最多水的容器

利用**双指针**统计不同宽度下的面积，然后获得其最大值。

面积由两端柱子中较短的一根决定，因此每次计算完面积后，移动高度较小的指针。移动较高的柱子只会让宽度变小，不可能得到更大的面积。

当然，如果移动了较短的柱子，面积也没有变大，说明宽度变小之后无论如何都无法得到更大面积。

移动较高的柱子一定不会让面积变大，所以每次移动短柱子筛选掉的一定都是错误答案，因此一定可以得到最优解。

时间复杂度$`O(n)`$，空间复杂度$`O(1)`$。

```c++
class Solution {
public:
    int maxArea(vector<int>& height) {
        int m_area = 0;

        int l = 0, r = height.size() - 1;
        while(l < r){
            int area = min(height[l], height[r])  * (r - l);
            m_area = max(area, m_area);

            if(height[l] < height[r]) l ++;
            else r --;
        }
        return m_area;
    }
};
```
