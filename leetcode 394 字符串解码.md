# leetcode 394 字符串解码

维护两个变量`num`和`str`，分别表示当前最新遇到的数字和字符串。

初始时`num = 0`, `str = ""`。

在维护两个栈`num_st`和`str_st`，分别存放数字和字符串。

遍历字符串：

- 如果遍历到数字字符，就更新`num`。

- 如果遍历到字母字符，就更新`str`。

- 如果遇到`[`，说明要新算一层。因此把`num`和`str`分别压栈`num_st`和`str_st`。然后`num`和`str`恢复初值。

- 如果遇到`]`，说明要结算。此时该`]`与其对应`[`之间的内容已经结算好并且存在`str`里了。

  `num_st.top()`放的是`str`要重复的次数；

  `str_st.top()`放的是`num_st.top()`前面，上一层`[`后面的字符串。

  要做的事情就是：

  ```c++
  str = str_st.top() + num_st.top() * str
  ```

  然后`num`恢复成`0`。否则后续会基于当前`num`继续更新`num`值。

时间复杂度与解码后字符串长度相关。

```c++
class Solution {
public:
    string decodeString(string s) {
        stack<int> num_st;
        stack<string> str_st;

        int num = 0;
        string str = "";

        for(auto c: s){
            if(isdigit(c)){
                num = num * 10 + c - '0';
            }
            else if(c >= 'a' && c <= 'z'){
                str += c;
            }
            else if(c == '['){
                num_st.push(num), str_st.push(str);
                num = 0, str = "";
            }
            else{
                num = num_st.top(); num_st.pop();	// 获得当前 str 重复次数
                string pro = str;	// 暂存当前 str

                str = str_st.top(); str_st.pop();	// str 赋值成目标字符串的开头
                for(int i = 0; i < num; i ++) str += pro;

                num = 0;
            }
        }

        return str;
    }
};
```
