# leetcode 206 反转链表

1. 迭代法。一次保存两个指针。反转之后向前进。时间复杂度$O(n)$。

   ```c++
class Solution {
   public:
    ListNode* reverseList(ListNode* head) {
           ListNode* a = nullptr, *b = head;

           while(b != nullptr){
            ListNode* bn = b->next;
               b->next = a;
               a = b;
               b = bn;
           }
   
           return a;
       }
   };
   ```
   
2. 递归法。时间复杂度$O(n)$。空间复杂度因为递归，所以会高。

   ```c++
   class Solution {
   public:
       ListNode* reverseList(ListNode* head) {
           if(head == nullptr || head->next == nullptr) return head;
           
           ListNode* res = reverseList(head->next);
           head->next->next = head;
           head->next = nullptr;
           return res;
       }
   };
   ```

   

   