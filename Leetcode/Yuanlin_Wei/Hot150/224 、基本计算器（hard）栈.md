#### 224 、基本计算器（hard）栈

```
class Solution {
public:
    int calculate(string s) {
        stack<int> data;
        stack<char> ops;
        int m = s.size();
        string str;
        for(int i = 0; i < m; ++i) {
            if(s[i] != ' '){
                str += s[i];
            }
        }
        m = str.size();
        string te;
        for(int i = 0; i < m; ++i) {
            if(str[i] == '-' ){
                if(i == 0 || str[i-1] == '(')
                    te += '0';
                    te += '-';
            } else {
                te += str[i];
            }
        }
        s = te;
        m = s.size();
        //消去所有的空格
        for(int i = 0; i < m; i++) {
            if(s[i] == '(') {
                ops.push('(');
            } else if(s[i] == ')') {
                while(!ops.empty()) {
                    if(ops.top() == '('){
                        ops.pop();
                        break;
                    }
                    int a = data.top();
                    data.pop();
                    int b = data.top();
                    data.pop();
                    if(ops.top() == '+'){
                        data.push(a+b);
                    }else{
                        data.push(b-a);
                    }
                    ops.pop();
                }
            } else if(s[i] == '+' || s[i] == '-'){
                if(!ops.empty()){
                    char cu = ops.top();
                    if(cu == '+' || cu == '-') {
                        ops.pop();
                        int a = data.top();
                        data.pop();
                        int b = data.top();
                        data.pop();
                        if(cu == '+'){
                            data.push(a+b);
                        }else{
                            data.push(b-a);
                        }
                    ops.push(s[i]);
                    }else if(cu =='('){
                        ops.push(s[i]);
                    }
                } else {
                    ops.push(s[i]);
                }
            }else{
                int temp = 0;
                while(s[i]>='0' && s[i] <='9'){
                    temp = temp * 10;
                    temp += s[i] - '0';
                    i++;
                }
                i--;
                data.push(temp);
            }
        }
        while(!ops.empty()){
            int a = data.top();
            data.pop();
            int b = data.top();
            data.pop();
            if(ops.top() == '+'){
                data.push(a+b);
            } else{
                data.push(b-a);
            }
            ops.pop();
        }
        return data.top();
    }
};
```

先预处理，去掉所有的空格

对可做一元运算也可二元运算的负号进行处理。所有用于一元运算的负号在其前方加个0转化为同一的二元运算。

设两个栈分别进行运算。