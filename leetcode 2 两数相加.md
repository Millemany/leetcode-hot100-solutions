# leetcode 2 两数相加

链表版本的模拟加法。稍微麻烦的一点在于不方便预先知道两个数字谁大谁小，只能一步一步走。

时间复杂度$O(n)$，空间复杂度$O(1)$。

```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* a = l1, *b = l2;
        int t = 0;

        while(a != nullptr){
            t += a->val;
            if(b != nullptr && a != b) t += b->val;
            a->val = t % 10;
            t /= 10;

            if(a->next == nullptr){
                if(b != nullptr && b->next != nullptr){ 
                    // 说明 l1 的长度小于 l2
                    // 要把 b 接到 a 的屁股后面
                    a->next = b->next;
                }
                else if(t){ // 说明要算完了，看看是否进位
                    ListNode* c = new ListNode(t);
                    a->next = c;
                    a = c;
                }
            }
            a = a->next;
            if(b != nullptr) b = b->next;
        }
        return l1;
    }
};
```

