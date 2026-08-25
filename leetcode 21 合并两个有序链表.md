# leetcode 21 合并两个有序链表

和归并排序很像。归并排序中拿到了前后两部分有序数组，需要把它们合并成一整个有序数组。这题也是类似的。

具体思路就是同时遍历两个链表，把值更小的一个作为下一个节点。

时间复杂度$`O(m+n)`$，空间复杂度$`O(1)`$。

```c++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode* a = list1, *b = list2;
        ListNode* head = new ListNode();
        ListNode* res = head;

        while(a != nullptr && b != nullptr){
            if(a->val < b->val){
                head->next = a;
                head = a;
                a = a->next;
            }
            else{
                head->next = b;
                head = b;
                b = b->next;
            }
        }
        if(a != nullptr) head->next = a;
        if(b != nullptr) head->next = b;
        
        return res->next;
    }
};
```

