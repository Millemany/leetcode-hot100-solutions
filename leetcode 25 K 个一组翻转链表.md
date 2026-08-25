# leetcode 25 K 个一组翻转链表

模拟。步骤如下：s

1. 分别确定`groupPrev`, `kth`和`groupNxt`三个结点。
   - `groupPrev`表示当前一组结点的前驱。
   - `kth`表示当前组<img src="./assets/formulas/formula-8254c329a928.svg" alt="k">个结点中的最后一个。从`groupPrev`开始向后找到第<img src="./assets/formulas/formula-8254c329a928.svg" alt="k">个结点，不足<img src="./assets/formulas/formula-8254c329a928.svg" alt="k">个就直接结束。
   - `groupNxt`表示当前一组结点的后继，也就是`kth->next`。
2. 让`prev = groupNxt`，`cur = groupPrev->next`（也就是<img src="./assets/formulas/formula-8254c329a928.svg" alt="k">组的第一个结点），不断翻转。
3. 重置`groupPrev->next = kth`，确定新的`groupPrev = 原groupPrev->next`。因为`groupPrev->next`会变化，所以需要暂存`原groupPrev->next`。

时间复杂度<img src="./assets/formulas/formula-387008096a41.svg" alt="O(n)">，空间复杂度<img src="./assets/formulas/formula-4a137b861e8d.svg" alt="O(1)">。

```c++
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* h = new ListNode();
        h->next = head;

        ListNode* groupPrev = h;

        while(true){
            ListNode* kth = groupPrev;
            for(int i = 0; i < k; i ++){
                kth = kth->next;
                if(kth == nullptr) return h->next;
            }

            ListNode* groupNxt = kth->next;
            ListNode* cur = groupPrev->next;
            ListNode* prev = groupNxt;

            while(cur != groupNxt){
                ListNode* nxt = cur->next;
                cur->next = prev;
                prev = cur;
                cur = nxt;
            }

            ListNode* tmp = groupPrev->next;
            groupPrev->next = kth;
            groupPrev = tmp;
        }

        return h->next;
    }
};
```
