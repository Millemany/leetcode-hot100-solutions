# leetcode 295 数据流的中位数

维护两个堆，分别存储较小的一半数据和较大的一般数据。较小的数据用大根堆`left_heap`维护，较大的数据用小根堆`right_heap`维护。始终保持大根堆数据量与小根堆数据量相等（偶数个元素）或者多一个（奇数个元素），这样中位数就是两个堆顶的平均值（偶数个元素），或者是大根堆堆顶（奇数个元素）。

下面的问题就是如何维护两个堆。比如现在两个堆是完好的。现在新来了一个数据。我们**默认先把这个数据插到`left_heap`**，那么会有四种情况：

1. 这是**第奇数个**数据，并且数据大小**不大于小根堆顶**。

   此时数据插入之后，就有`right_heap.size() == left_heap.size() + 1`，且满足`left_heap`元素不大于`right_heap`元素。因此不用额外处理。

2. 这是**第奇数个**数据，并且数据大小**大于小根堆顶**。

   此时虽然两个堆数据量满足要求，但是这个元素应该插入`right_heap`而非`left_heap`。

   又因为该元素一定在`left_heap`的堆顶，所以需要<u>把`left_heap`的堆顶元素放到`right_heap`里</u>。

   同时为了保证两个堆数据量不变，要<u>把`right_heap`的堆顶（即其最小值）放到`left_heap`里</u>。

3. 这是**第偶数个**数据，并且数据大小**不大于小根堆顶**。

   这是第偶数个数据，说明在该数据插入堆之前，有`left_heap.size() == right_heap.size() + 1`。

   所以该数据插入后，`left_heap`比`right_heap`多了两个元素。

   因此需要<u>把`left_heap`的堆顶元素放到`right_heap`里</u>。

4. 这是**第偶数个**数据，并且数据大小**大于小根堆顶**。

   此时插入的数据一定是`left_heap`的堆顶。<u>把`left_heap`的堆顶元素放到`right_heap`里</u>，就能同时满足数据大小的要求和数据量的要求。

因此添加数据的时间复杂度是$O(\log n)$，求中位数的时间复杂度是$O(1)$。

```c++
class MedianFinder {
    priority_queue<int> left_heap;
    priority_queue<int, vector<int>, greater<int>> right_heap;
public:
    MedianFinder() {
    }
    
    void addNum(int num) {
        left_heap.push(num);

        if(left_heap.size() > right_heap.size() + 1 || right_heap.size() && num > right_heap.top()){	
// left_heap.size() > right_heap.size() + 1 说明这是第偶数个元素
// right_heap.size() && num > right_heap.top() 说明插入的元素应该放在 right_heap 里
            right_heap.push(left_heap.top());
            left_heap.pop();
        }

        if(right_heap.size() > left_heap.size()){ 
            // 此时对应了上面说的第二种情况，要把 right_heap 的堆顶放到 left_heap
            left_heap.push(right_heap.top());
            right_heap.pop();
        }
    }
    
    double findMedian() {
        if(left_heap.size() > right_heap.size()) return left_heap.top();
        else return ((double)left_heap.top() + right_heap.top()) / 2;
    }
};
```

