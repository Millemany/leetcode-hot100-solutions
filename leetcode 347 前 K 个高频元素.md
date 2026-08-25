# leetcode 347 前 K 个高频元素

1. 堆

   堆有两种做法，都需要用一个哈希表统计每个数字出现的个数。然后维护一个堆，里面放的是`pair<int, int>`，第一个值是数字出现的个数，第二个值是这个数字本身。

   一种做法是维护一个大小为 k 的小根堆，不断往小根堆里面放元素，如果小根堆里面元素个数超过 k，就弹出堆里最小的元素。最后剩下的一定是 k 个出现次数最大的元素。时间复杂度是<img src="./assets/formulas/formula-58f5e03c2339.svg" alt="O(m \log k)">，其中<img src="./assets/formulas/formula-62c66a7a5dd7.svg" alt="m">是不同的元素个数。

   另一种做法就是维护一个大根堆，不断往大根堆里放元素，全部放完之后从堆里弹出 k 个元素，就是出现次数最大的。这种写法更简单，但时间复杂度是<img src="./assets/formulas/formula-f444f15d4868.svg" alt="O(m \log m)">。

   这里只展示第一种写法。

   ```c++
   class Solution {
   public:
       vector<int> topKFrequent(vector<int>& nums, int k) {
           unordered_map<int, int> mp;
           for(auto t: nums) mp[t] ++;
   
           priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> heap;
   
           for(auto [s, t]: mp){
               heap.push({t, s});
               if(heap.size() > k) heap.pop();
           }
   
           vector<int> res;
           while(heap.size()){
               res.push_back(heap.top().second);
               heap.pop();
           }
   
           return res;
       }
   };
   ```

2. 快速排序的改进

   思路和 [leetcode 215 数组中的第K个最大元素](<./leetcode 215 数组中的第K个最大元素.md>) 类似。因为我只想知道最大的 k 的元素而不在乎其顺序。因此在划分（partition）之后，

   - 如果右半边元素数量小于 k，说明右半边一定都是答案，只要排序左边就可以了；

   - 反之如果右半边元素数量大于 k，那就可以完全排除左半边，继续处理右半边；

   - 如果右半边数量就是 k，那就直接退出就可以了。

   这样的平均复杂度是<img src="./assets/formulas/formula-4343234bc647.svg" alt="O(m)">。

   ```c++
   class Solution {
       void quick_sort(vector<pair<int, int>>& q, int l, int r, int k){
           if(l >= r) return;
           int x = q[(l + r) >> 1].first;
           
           int i = l - 1, j = r + 1;
           while(i < j){
               do i ++; while(q[i].first < x);
               do j --; while(q[j].first > x);
               if(i < j) swap(q[i], q[j]);
           }
           
           if(k > r - j) quick_sort(q, l, j, k - r + j);
           else if(k < r - j) quick_sort(q, j + 1, r, k);
           else return;
       }
   public:
       vector<int> topKFrequent(vector<int>& nums, int k) {
           unordered_map<int, int> mp;
           for(auto t: nums) mp[t] ++;
   
           int n = 0;
   
           vector<pair<int, int>> q;
           for(auto [s, t]: mp){
               q.push_back({t, s});
               n ++;
           }
   
           quick_sort(q, 0, n - 1, k);
   
           vector<int> res;
           for(int i = n - 1; i >= n - k; i --) res.push_back(q[i].second);
   
           return res;
       }
   };
   ```

   

