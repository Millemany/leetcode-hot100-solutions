# leetcode 234 回文链表

模拟。

先用快慢指针找到链表的中点，然后翻转后半部链表。最后从前半部和翻转后的后半部同时开始比较。

奇数个结点时，后半部会包含中间结点，但不影响比较。

时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">，空间复杂度<img src="./assets/formulas/formula-4a137b861e8d.svg" alt="O(1)">。

```c++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        ListNode* slow = head, *fast = head;
        while(fast && fast->next){
            slow = slow->next;
            fast = fast->next->next;
        }	// slow 是链表中间结点
        // 如果有奇数个元素，slow 就是正中间
        // 如果有偶数个元素，slow 就是中间偏右那个

        ListNode* prev = nullptr;
        while(slow){	// 翻转链表后半部分
            ListNode* nxt = slow->next;
            slow->next = prev;
            prev = slow;
            slow = nxt;
        }

        ListNode* l = head, *r = prev;	// 此时 slow 已经是 nullptr 了，prev是最后一个结点
        while(r){
            if(l->val != r->val) return false;
            l = l->next, r = r->next;
        }

        return true;
    }
};
```
