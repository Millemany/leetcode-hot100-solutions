# leetcode 24 两两交换链表中的节点

1. 递归。

   ```c++
class Solution {
   public:
    ListNode* swapPairs(ListNode* head) {
           if(head == nullptr || head->next == nullptr) return head;

           ListNode* p = swapPairs(head->next->next);
        ListNode* q = head->next;
           q->next = head, head->next = p;
           return q;
       }
   };
   ```
   
2. 模拟。

   ```c++
   class Solution {
   public:
       ListNode* swapPairs(ListNode* head) {
           if(head == nullptr || head->next == nullptr) return head;
   
           ListNode* a = head, *res=  a->next, *pre = nullptr;
           // pre 是上一轮的尾部指针。
           // 处理之前是 pre->next == a，处理之后要把它变成 pre->next == b。
           
           while(a != nullptr && a->next != nullptr){
               ListNode* b = a->next;
               ListNode* c = b->next;
   
               b->next = a, a->next = c;
               if(pre != nullptr) pre->next = b;
               pre = a;
               a = c;
           }
   
           return res;
       }
   };
   ```

   