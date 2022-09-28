Implement a first in first out (FIFO) queue using only two stacks.  
The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).  

Implement the MyQueue class:  
void push(int x) Pushes element x to the back of the queue.  
int pop() Removes the element from the front of the queue and returns it.  
int peek() Returns the element at the front of the queue.  
boolean empty() Returns true if the queue is empty, false otherwise.  

Code:  
```c
class MyQueue {
public:
    MyQueue() {
        
    }
    
    void push(int x) {
        st_in.push(x);
    }
    
    int pop() {
        int return_val;
        if(st_out.empty()) {
            while(st_in.size() > 1) {
                st_out.push(st_in.top());
                st_in.pop();
            }
            return_val = st_in.top();
            st_in.pop();
        }
        else {
            return_val = st_out.top();
            st_out.pop();
        }
        
        return return_val;
    }
    
    int peek() {
        if(st_out.empty()) {
            while(!st_in.empty()) {
                st_out.push(st_in.top());
                st_in.pop();
            }
        }
        return st_out.top();
    }
    
    bool empty() {
        return st_in.empty() && st_out.empty();
    }
private:
    stack<int> st_in, st_out;
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```
Runtime: 0 ms, faster than 100.00% of C++ online submissions for Implement Queue using Stacks.  
Memory Usage: 7.1 MB, less than 13.10% of C++ online submissions for Implement Queue using Stacks.  
