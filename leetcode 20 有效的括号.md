# leetcode 20 有效的括号

用栈存左括号。遇到右括号时，栈顶必须是对应的左括号，否则直接返回`false`。

最后还要判断栈是否为空，防止存在多余的左括号。

时间复杂度$`O(n)`$，空间复杂度$`O(n)`$。

```c++
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;

        for(auto c: s){
            if(c == '(' || c == '[' || c == '{') st.push(c);
            else if(c == ')'){
                if(st.empty() || st.top() != '(') return false;
                st.pop();
            }
            else if(c == ']'){
                if(st.empty() || st.top() != '[') return false;
                st.pop();
            }
            else{
                if(st.empty() || st.top() != '{') return false;
                st.pop();
            }
        }
        return st.empty();
    }
};
```
