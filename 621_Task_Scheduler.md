You are given an array of CPU tasks, each represented by letters A to Z, and a cooling time, n.  
Each cycle or interval allows the completion of one task.  
Tasks can be completed in any order, but there's a constraint: identical tasks must be separated by at least n intervals due to cooling time.  

​Return the minimum number of intervals required to complete all tasks.  

Example 1:  
```
Input: tasks = ["A","A","A","B","B","B"], n = 2

Output: 8

Explanation: A possible sequence is: A -> B -> idle -> A -> B -> idle -> A -> B.

After completing task A, you must wait two cycles before doing A again. The same applies to task B. In the 3rd interval, neither A nor B can be done, so you idle. By the 4th cycle, you can do A again as 2 intervals have passed.

```

Example 2:  
```

Input: tasks = ["A","C","A","B","D","B"], n = 1

Output: 6

Explanation: A possible sequence is: A -> B -> C -> D -> A -> B.

With a cooling interval of 1, you can repeat a task after just one other task.
```

Example 3:  
```

Input: tasks = ["A","A","A", "B","B","B"], n = 3

Output: 10

Explanation: A possible sequence is: A -> B -> idle -> idle -> A -> B -> idle -> idle -> A -> B.

There are only two types of tasks, A and B, which need to be separated by 3 intervals. This leads to idling twice between repetitions of these tasks.
```

Code:  
```c++
class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
        vector<int> freq(26, 0);
        int i = 0;
        for(i = 0; i < tasks.size(); ++i) {
            ++ freq[tasks[i] - 'A'];
        }

        int max_freq = 0;
        int num_max_task = 0;
        for(i = 0; i < 26; ++i) {
            if(freq[i] > max_freq) max_freq = freq[i];
        }
        for(i = 0; i < 26; ++i) {
            if(freq[i] == max_freq) ++num_max_task;
        }

        int time = (n+1) * (max_freq-1) + num_max_task;

        return max(time, int(tasks.size()));
    }
};
```

Ideas:  
After a task is implemented, the CPU must wait for at least n iterations to implement the same task again, so we set the length of a cycle to n+1.  
If we take out the task that has the most frequency, for example, A, then we can put A in every cycle.  
That is, [A, ?], [A, ?]..., [A]. There are A.freq cycles, except for the last cycle, the former A.freq-1 cycles have some spaces (?) can fill in other tasks.  
Now, we consider the case that CPU needs idle time.  
If there are some "?" that have no other tasks to fill in, then there will be idle time. In this case, the total time will be ```(n+1)*(A.freq-1) + num of tasks that have the max freq```.  
If there are more other tasks than the positions of "?", then there will be no idle time, to the total time is the number of tasks.  
Hence, we only need to take the larger one of the result of our formula and the number of tasks, that will be the answer.  

Performance:  
44 ms, beats 92.52% of C++ users.  
38.04 MB, beats 64.29% of C++ users.  
