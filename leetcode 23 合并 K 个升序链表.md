# leetcode 23 合并 K 个升序链表

1. 小根堆

   把每个链表的头结点放入小根堆。每次取出值最小的结点接到答案后面，再把它的后继放入堆。

   设所有链表共有$`n`$个结点，链表数量为$`k`$。时间复杂度$`O(n\log k)`$，空间复杂度$`O(k)`$。

   ```c++
   struct Cmp{
       bool operator()(ListNode* a, ListNode* b){
           return a->val > b->val;
       } // 函数类，重载括号。c++ 对于非内置的数据类型创建小根堆，需要自己构建比较类。
   };

   class Solution {
   public:
       ListNode* mergeKLists(vector<ListNode*>& lists) {
           priority_queue<ListNode*, vector<ListNode*>, Cmp> heap;
           ListNode* res = new ListNode();
           ListNode* cur = res;

           for(auto t: lists){
               if(t) heap.push(t);
           }

           while(heap.size()){
               auto t = heap.top();
               heap.pop();

               cur->next = t;
               cur = t;

               if(t->next) heap.push(t->next);
           }

           return res->next;
       }
   };
   ```

2. 归并

   合并两个有序链表是经典的归并操作。使用分治，先分别合并左右两半链表，再合并两个结果。

   时间复杂度$`O(n\log k)`$，递归栈空间复杂度$`O(\log k)`$。

   ```c++
   class Solution {
       ListNode* mergeTwoLists(ListNode* a, ListNode* b){
           ListNode* res = new ListNode();
           ListNode* cur = res;

           while(a && b){
               if(a->val < b->val){
                   cur->next = a;
                   cur = a;
                   a = a->next;
               }
               else{
                   cur->next = b;
                   cur = b;
                   b = b->next;
               }
           }
           if(a) cur->next = a;
           if(b) cur->next = b;

           return res->next;
       }

       ListNode* merge(vector<ListNode*>& lists, int l, int r){
           if(l >= r) return lists[r];

           int mid = (l + r) >> 1;
           return mergeTwoLists(merge(lists, l, mid), merge(lists, mid + 1, r));
       }
   public:
       ListNode* mergeKLists(vector<ListNode*>& lists) {
           int n = lists.size();
           if(n == 0) return nullptr;
           return merge(lists, 0, n - 1);
       }
   };
   ```
