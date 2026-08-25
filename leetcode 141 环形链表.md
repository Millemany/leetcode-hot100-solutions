# leetcode 141 环形链表

可以用哈希。时空复杂度都是$O(n)$。

更好的办法是快慢指针。快指针和慢指针都从开头出发，快指针一次走两步，慢指针一次走一步。只要有环，两个指针最终一定会重合。

可以这样证明。假如存在环，且某一时刻慢指针在快指针前面 d 步（因为是一个环，所以不管两个指针的相对位置如何，一定可以看成快指针在慢指针后面）。那么操作一次之后，快慢指针之间的差距只有 d - 1 步了。再操作一次，差距就是 d - 2 步。以此类推，最终两个指针一定会重合。

时间复杂度是$O(n)$，空间复杂度是$O(1)$。

```c++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        ListNode* fast = head, *slow = head;

        while(fast != nullptr && fast->next != nullptr){
            fast = fast->next->next;
            slow = slow->next;

            if(fast == slow) return true;
        }
        return false;
    }
};
```



