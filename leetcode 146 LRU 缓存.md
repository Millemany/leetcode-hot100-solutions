# leetcode 146 LRU 缓存

本题的意思是这样的：

你需要维护一个数据结构，其最大容量为`capacity`。要求：

1. 支持`get`方法，通过`key`访问`value`。
2. 支持`put`方法，插入一个`(key, value)`对。如果此时超过了最大容量，需要把**最久未使用**的`(key, value)`删去。

因此这个数据结构需要维护使用顺序。可以采用双向链表，**链表尾部是最近使用的元素，头部是最久未使用的元素。**哈希表记录`key`对应的链表迭代器。

c++ stl 里面的双向链表是`list`数据结构。本题中使用到了下面几个操作：

- `list.splice(list.end(), list, it)`。其中`it`是`list`里面某个元素的迭代器。

  这个函数的作用是把`it`对应的元素移动到`list`的结尾，其他元素相对顺序不变。

- `list.push_back()`。向`list`的结尾追加一个元素。

- `prev(it)`。获得`it`的前继结点。

- `list.earse(it)`。删除`it`对应的元素。

因为哈希表记录`key`对应的链表迭代器，所以哈希表里面存储的是`<int, list::iterator>`键值对。

----

`get`或更新已有元素时，用`splice`把结点移动到链表尾部。超过容量时删除链表头部。

`get`和`put`的平均时间复杂度都是$`O(1)`$。

```c++
class Node{
public:
    int key;
    int val;
    Node(int k, int v):key(k), val(v){}
};

class LRUCache {
    list<Node> cache;
    unordered_map<int, list<Node>::iterator> mp;
    int cap;
public:
    LRUCache(int capacity) {
        cap = capacity;
    }

    int get(int key) {
        if(mp.count(key) == 0) return -1;	// 没有这个元素

        auto it = mp[key];
        cache.splice(cache.end(), cache, it);	// it 变成最近使用的元素
        return it->val;
    }

    void put(int key, int value) {
        if(mp.count(key)){	// 覆盖已有元素
            auto it = mp[key];
            it->val = value;
            cache.splice(cache.end(), cache, it);
        }
        else{	// 插入新元素
            cache.push_back(Node(key, value));
            mp[key] = prev(cache.end());	// 插入的元素就是 end() 迭代器的前继
        }

        if(cache.size() > cap){
            int k = cache.begin()->key;	// 获得链表头元素，最久没使用的
            cache.erase(cache.begin());	// 从链表里删去
            mp.erase(k);	// 从哈希表里删去
        }
    }
};
```
