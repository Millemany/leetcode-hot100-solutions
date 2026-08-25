# leetcode 287 寻找重复数

把`nums`数组看成链表，`nums[i]`表示`i`号结点的下一个结点。

因为`nums`数组元素都在`[1, n]`内，并且有重复元素，那么这个数组对应的链表一定有环，并且重复数字就是环的入口。

可以这样证明：我们从 0 结点出发，不断前进：

```c++
x₀ = 0
x₁ = nums[x₀]
x₂ = nums[x₁]
x₃ = nums[x₂]
...
```

因为`nums`元素取值范围是`[1, n]`，而`[1, n]`中每一个结点都有一个`nums`值，所以这个链表可以一直走下去。

而又因为`nums`只有`n`个不同的取值，所以一定会存在两个位置$`x_i`$和$`x_j`$，满足$`x_i=x_j=y`$。

这就说明从$`y`$出发一定会再次访问到$`y`$。

因此一定有环。

---

所以本题可以使用 [leetcode 142 环形链表 II](./leetcode 142 环形链表 II) 的做法。

时间复杂度是$`O(n)`$。

```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = 0, fast = 0;
        
        do{
            slow = nums[slow];
            fast = nums[nums[fast]];
        }while(slow != fast);

        slow = 0;

        while(slow != fast){
            slow = nums[slow];
            fast = nums[fast];
        }

        return fast;
    }
};
```



