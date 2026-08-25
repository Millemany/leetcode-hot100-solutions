# leetcode 148 排序链表

这题就是归并排序的链表版本。

1. 自顶向下排序。时间复杂度$O(n\log n)$，空间复杂度$O(\log n)$。代码好写。

2. 自底向上排序。时间复杂度$O(n\log n)$，空间复杂度$O(1)$。不用递归，代码较复杂。

   具体做法就是先把链表断成长度为1的小段，然后相邻两段之间按序合并。合并后相邻两端再按序合并，依次类推，直到整个链表有序。

   这个代码分成三部分：

   - `ListNode* merge(ListNode* a, ListNode* b)`。按序合并两个链表，其中`a`和`b`链表都是有序的。这里先创建一个空头指针，因为不知道`a`和`b`谁会做链表头。返回的是整个有序链表的头指针。
   - `ListNode* split(ListNode* left, int len)`。把`left`开头的链表拆出长度为`len`的一段，返回拆开后原链表的开头。注意`left`可能是`nullptr`。
   - `ListNode* sortList(ListNode* head)`。输入原链表，返回有序链表。这里和`merge`一样，需要一个空头指针，因为排序后的链表开头不一定是`head`的某个元素。

   ```c++
   class Solution {
       ListNode* merge(ListNode* a, ListNode* b){
           ListNode* h = new ListNode();
           ListNode* cur = h;
           while(a && b){
               if(a->val < b->val){
                   cur->next = a;
                   a = a->next;
               }
               else{
                   cur->next = b;
                   b = b->next;
               }
               cur = cur->next;
           }
           cur->next = a ? a : b;
           return h->next;
       }
       ListNode* split(ListNode* left, int len){
           if(left == nullptr) return nullptr;
   
           ListNode* cur = left;
           for(int i = 1; i < len && cur->next; i ++) cur = cur->next;
           
           ListNode* right = cur->next;
           cur->next = nullptr;
           return right;
       }
   public:
       ListNode* sortList(ListNode* head) {
           int n = 0;
           ListNode* p = head;
   
           while(p){
               n ++;
               p = p->next;
           }	// 先统计链表长度，这样后面好确定循环次数
   
           ListNode* h = new ListNode();	// 空头结点
           h->next = head;
           for(int len = 1; len < n; len = len << 1){	// 确定循环次数
               ListNode* prev = h, *cur = h->next;
               // prev 是尾结点，用来尾插法的
   
               while(cur){
                   ListNode* left = cur;
                   ListNode* right = split(left, len);	// 拆出第一段
                   cur = split(right, len);	// 拆出第二段
   
                   prev->next = merge(left, right);	// 合并，同时追加到已排序链表的尾巴后面
                   while(prev->next) prev = prev->next;
                   // 更新尾结点
               }
           }
           return h->next;
       }
   };
   ```

   