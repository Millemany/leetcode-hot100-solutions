# leetcode 160 相交链表

1. 哈希表。先扫描一遍链表A，把访问过的节点存到哈希表里，然后再扫描链表B。

   时间复杂度和空间复杂度都是$`O(m + n)`$。

   ```c++
   class Solution {
   public:
       ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
           unordered_map<ListNode*, bool> mp;
   
           for(ListNode* i = headA; i != NULL; i = i->next)
               mp[i] = true;
   
           for(ListNode* i = headB; i != NULL; i = i->next)
               if(mp[i]) return i;
   
           return NULL;
       }
   };
   ```

2. 双指针。

   让两个指针`pa`和`pb`分别从 A 链表和 B 链表的开头前进。如果`pa`变成了空指针，就让他变成`headB`遍历 B 链表。`pb`变成空同样让它遍历 A 链表。这样做的话，`pa`和`pb`最终一定会相同，并且第一次相同的指针就是答案。

   举个例子可以明白。比如 A 链表是`A->B->C->F->G`，B 链表是`D->E->F->G`。

   那么`pa`和`pb`的遍历过程就依次是：

   ```txt
   pa: A -> B -> C -> F -> G -> NULL -> D -> E -> F -> G（未遍历到）-> NULL（未遍历到）
   pb: D -> E -> F -> F -> NULL -> A -> B -> C -> F -> G（未遍历到）-> NULL（未遍历到）
   ```

   也就是说，`pa`和`pb`如果都走到底的话，那么就都是`NULL`。如果两个链表真有重复元素，那么从这个`NULL`往前推，`pa`和`pb`的值肯定也是一样的。所以他们第一次相等的值，就是这两个链表的第一个重复点。

   这也可以推知，如果两个链表没有重复点，那`pa`和`pb`相同的时候两者就都是`NULL`了。此时返回的就是`NULL`。

   时间复杂度$`O(m+n)`$，空间复杂度$`O(1)`$。

   ```c++
   class Solution {
   public:
       ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
           ListNode* pa = headA, *pb = headB;
           while(pa != pb){
               if(pa == NULL) pa = headB;
               else pa = pa -> next;
   
               if(pb == NULL) pb = headA;
               else pb = pb -> next;
           }
           return pa;
       }
   };
   ```

   

