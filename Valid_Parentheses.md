code
c++:
class Solution {
public:
    bool isValid(string s) {
        vector<char> stack;
        for(int i = 0; i < s.length(); ++i) {
            if(s[i] == ')') {
                if(stack.empty()) return false;
                if(stack.back() == '(') stack.pop_back();
                else return false;
            }
            else if(s[i] == ']') {
                if(stack.empty()) return false;
                if(stack.back() == '[') stack.pop_back();
                else return false;
            }
            else if(s[i] == '}') {
                if(stack.empty()) return false;
                if(stack.back() == '{') stack.pop_back();
                else return false;
            }
            else stack.push_back(s[i]);
        }
        cout << "hello" << endl;
        if(stack.empty()) return true;
        else return false;
    }
};
