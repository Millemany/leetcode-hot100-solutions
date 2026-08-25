# leetcode 155 最小栈

1. 辅助栈

   单开一个栈，用来存储当前最小值。

   比如真正的栈是`stack`，单开的辅助栈叫做`min_stack`。

   - 压栈`5`

     ```txt
     stack: 		5
     min_stack: 	5
     ```

   - 压栈`7`。此时最小值还是`5`，所以：

     ```txt
     stack: 		5	7
     min_stack: 	5	5 
     ```

   - 压栈`3`。此时最小值是`3`，所以：

     ```txt
     stack: 		5	7	3
     min_stack: 	5	5	3 
     ```

   弹栈的时候两个栈同时弹出就行了。

   ```c++
   class MinStack {
       stack<int> st;
       stack<int> mst;
   public:
       MinStack() {
           st.push(INT_MAX), mst.push(INT_MAX);
       }
       
       void push(int value) {
           st.push(value);
           mst.push(min(value, mst.top()));
       }
       
       void pop() {
           st.pop(), mst.pop();
       }
       
       int top() {
           return st.top();
       }
       
       int getMin() {
           return mst.top();
       }
   };
   ```

   

2. 不用辅助栈

   辅助栈需要$`O(n)`$的额外空间。本题也可以只用$`O(1)`$空间解决问题，用一个变量`min_val`存储当前的最小值。

   但如果仅仅这样做，就无法确定`min_val`弹出之后的最小值。

   

   考虑到栈里面所有元素必然大于等于`min_val`，我们可以在更小的值`new_min_val`入栈的时候，巧妙地设置实际入栈的数据`value`，使得`value < new_min_val`，同时根据`value`和`new_min_val`能够复原出以前的最小值`min_val`。

   这样在弹栈的时候，就可以做出如下判断：

   - 如果维护的栈顶元素小于`min_val`，说明真正的栈顶元素是`min_val`，并且弹栈之后最小值要改变。
   - 否则，维护的栈顶元素就是真正的栈顶元素。

   那么`value`应该怎么求呢？

   

   `value`的值应该满足两点：

   - 小于新的最小值`new_min_val`；
   - 能够根据`new_min_val`和`value`复原出`min_val`。

   据此，`value`的一个比较好的取值是`value = 2 * new_min_val - min_val`。

   这样就有`value = new_min_val + (new_min_val - min_val)`，而`new_min_val < min_val`一定成立，所以`value < new_min_val`一定成立。

   同时，又有`min_val = 2 * new_min_val - value`。因此能够复原出`min_val`。

   ```c++
   class MinStack {
       stack<long long> st;
       long long min_val;
       // 注意这里都必须是 long long
       // 因为下面有把 int 类型的值乘以二的操作，只用 int 会越界
   public:
       MinStack() {
           min_val = LLONG_MAX; // 这里初始化成什么值都无所谓
       }
       
       void push(int value) {
           if(st.empty()){
               st.push(value);
               min_val = value;
           }
           else if(value < min_val){
               long long tmp = 2 * (long long)value - min_val;
               st.push(tmp);
               min_val = value;
           }
           else st.push(value);
       }
       
       void pop() {
           if(st.top() < min_val) min_val = 2 * min_val - st.top();
           st.pop();
       }
       
       int top() {
           if(st.top() < min_val) return min_val;
           else return st.top();
       }
       
       int getMin() {
           return min_val;
       }
   };
   ```

   
