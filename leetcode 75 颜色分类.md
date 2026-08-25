# leetcode 75 颜色分类

荷兰国旗算法。

维护三个指针`l`, `i`和`r`。其中：

- `[0, l)` 全都是`0`。初始的时候`l == 0`，表示还没有整理出`0`。
- `[l, i)`全都是`1`。初始的时候`i == 0`，表示还没整理出`1`。
- `[i, r]`表示没有整理好的数字。初始的时候`r == n - 1`。
- `(r, n - 1]`全都是`2`。

让`i`从`[0, r]`不断遍历。

- 如果`nums[i] == 0`，则交换`nums[i]`和`nums[l]`。

  此时`nums[l]`已经是`0`了，需要`l ++`。

  根据上面的约定，`nums[l]`在交换之前一定是`1`，因此现在`nums[i] == 1`。因此需要`i ++`。

- 如果`nums[i] == 1`，则`i ++`。

- 如果`nums[i] == 2`，则交换`nums[i]`和`nums[r]`。

  此时`nums[r]`已经是`2`了，需要`r --`。

  根据上面的约定，`nums[r]`在交换之前是没有整理的数字，因此`nums[r]`交换之前是未定的数字。`nums[i]`交换之后也是未定的，因此`i`不能变动，要继续讨论。

时间复杂度是<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">。

```c++
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n = nums.size();
        int l = 0, r = n - 1, i = 0;
        while(i <= r){
            if(nums[i] == 0){
                swap(nums[i], nums[l]);
                l ++, i ++;
            }
            else if(nums[i] == 1) i ++;
            else{
                swap(nums[i], nums[r]);
                r --;
            }
        }
    }
};
```



