# leetcode 138 随机链表的复制

这题必须建立复制结点和原结点的关系，否则无法复制随机指针。

因此可以**把复制结点插入原结点后面**。这样原结点`p`对应的复制结点就是`p->next`，复制结点的随机指针就是`p->random->next`。

最后把交错的两条链表拆开。时间复杂度$`O(n)`$，额外空间复杂度$`O(1)`$。

```c++
class Solution {
public:
    Node* copyRandomList(Node* head) {
        // 1. 插入拷贝
        Node* p = head;
        while(p){
            Node* q = new Node(p->val);
            q->next = p->next;
            p->next = q;
            p = p->next->next;
        }

        // 2. 做random
        p = head;
        while(p){
            if(p->random){
                p->next->random = p->random->next;
            }
            p = p->next->next;
        }

        // 3. 拆分链表
        p = head;
        Node* res = head ? head->next : NULL;
        while(p){
            Node* q = p->next->next;
            if(q) p->next->next = q->next;
            p->next = q;
            p = p->next;
        }

        return res;
    }
};
```
