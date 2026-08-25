# leetcode 215 数组中的第K个最大元素

本题使用快速排序的变体，快速选择算法。代码和快排几乎一样。

因为只求第 k 大的元素，所以不需要对数组中所有元素进行排序。每次只要排序含有答案的那一部分就行了。

平均时间复杂度是$O(n) = T(n) + T(n/2) + T(n/4) + \cdots T(1)$。

```c++
class Solution {
    void quick_sort(vector<int>& q, int l, int r, int k){
        if(l >= r) return;
        int x = q[(l + r) >> 1];

        int i = l - 1, j = r + 1;
        while(i < j){
            do i ++; while(q[i] < x);
            do j --; while(q[j] > x);
            if(i < j) swap(q[i], q[j]);
        }
        // 左半边一共有 j - l + 1 个元素    (l, j)
        // 右半边一共有 r - j 个元素    (r, j + 1)
        if(k <= r - j) quick_sort(q, j + 1, r, k);	// 第 k 大的元素在右半边，只处理右半边
        else quick_sort(q, l, j, k - r + j);		// 只处理左半边
    }
public:
    int findKthLargest(vector<int>& nums, int k) {
        int n = nums.size();
        quick_sort(nums, 0, n - 1, k);
        return nums[n - k];
    }
};
```

