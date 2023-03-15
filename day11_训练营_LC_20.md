## LC_[20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/)
给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串 `s` ，判断字符串是否有效。
思路：将所有(，{，[ 都转换为)，]，} 后压入栈中，然后再判断右括号是否一致，一致则弹出，不一致则返回false，栈全部弹出后返回true。
![enter image description here](https://code-thinking.cdn.bcebos.com/gifs/20.%E6%9C%89%E6%95%88%E6%8B%AC%E5%8F%B7.gif)

```
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        if(s.size() % 2 != 0){
            return false;
        }
        for(int i = 0; i < s.size(); i++){
            if(s[i] == '('){
                st.push(')');
            }
            else if(s[i] == '['){
                st.push(']');
            }
            else if(s[i] == '{'){
                st.push('}');
            }
            //遍历字符串右括号找匹配时，栈已经空了，说明右括号没有找到对应的左括号
            //遍历字符串右括号匹配，栈里面没有对应的左括号
            else if(st.empty() || s[i] != st.top()){
                return false;
            }
            else{
                st.pop();
            }
        }
        //已经遍历完字符串，但是栈不空，说明还有未匹配的，则return false；
        return st.empty();
    }
};
```
