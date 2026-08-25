# leetcode 19 删除链表的倒数第 N 个结点
还是快慢指针。先让一个快指针提前走 N 步，然后快慢指针一起走就可以了。

应当注意，删除头结点和删除其他结点不同。此外，最后应该定位到倒数第 N + 1 个结点，这样才能删掉第 N 个结点。

时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">，空间复杂度<img src="./assets/formulas/formula-4a137b861e8d.svg" alt="O(1)">。


```c++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* a = head, *b = head;

        for(int i = 0; i < n; i ++) a = a->next;
        if(a == nullptr) return head->next;

        while(a->next != nullptr){
            a = a->next, b = b->next;
        }
        b->next = b->next->next;
        return head;
    }
};
```

