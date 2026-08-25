# leetcode 108 将有序数组转换为二叉搜索树

迭代。其实不一定非要用它给的函数迭代，可以在它写的函数里调用我们自己写的迭代函数。

```c++
class Solution {
    TreeNode* work(vector<int>& v, int l, int r){
        if(l > r) return nullptr;

        int mid = (l + r) >> 1;
        TreeNode* res = new TreeNode(v[mid], work(v, l, mid - 1), work(v, mid + 1, r));
        
        return res;
    }
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return work(nums, 0, nums.size() - 1);
    }
};
```

