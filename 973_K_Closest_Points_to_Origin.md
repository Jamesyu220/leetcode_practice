Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0).  

The distance between two points on the X-Y plane is the Euclidean distance (i.e., √(x1 - x2)2 + (y1 - y2)2).  

You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).  

code:  
```c
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        cal_distance(points);
        for(int i = 0; i < points.size(); ++i) {
            if(maxHeap.size() < k) insert(i);
            else if(distance[i] < max_dis) {
                maxHeap[0] = i;
                max_heaplify(0);
            }
        }
        vector<vector<int>> closest(k);
        for(int i = 0; i < k; ++i) {
            closest[i] = points[maxHeap[i]];
        }
        return closest;
    }
private:
    int max_dis = -1;
    vector<int> maxHeap;
    vector<int> distance;
    void cal_distance(vector<vector<int>>& points) {
        int p_size = points.size();
        distance.resize(p_size);
        for(int i = 0; i < p_size; ++i) {
            distance[i] = points[i][0] * points[i][0] + points[i][1] * points[i][1];
        }
    }
    void max_heaplify(int k) {
        int self = maxHeap[k];
        // left, right child
        int left = (k*2+1 < maxHeap.size())? maxHeap[k*2+1]: -1; 
        int right = (k*2+2 < maxHeap.size())? maxHeap[k*2+2]: -1;
        if(left != -1) {
            if(right == -1) {
                if(distance[self] < distance[left]) {
                    maxHeap[k] = left;
                    maxHeap[k*2+1] = self;
                    max_heaplify(k*2+1);
                    if(k == 0) max_dis = distance[left];
                    return;
                }
            }
            else if(distance[self] < distance[left]) {
                if(distance[right] <= distance[left]) {
                    maxHeap[k] = left;
                    maxHeap[k*2+1] = self;
                    max_heaplify(k*2+1);
                    if(k == 0) max_dis = distance[left];
                    return;
                }
                else {
                    maxHeap[k] = right;
                    maxHeap[k*2+2] = self;
                    max_heaplify(k*2+2);
                    if(k == 0) max_dis = distance[right];
                    return;
                }
            }
            else if(distance[self] < distance[right]) {
                maxHeap[k] = right;
                maxHeap[k*2+2] = self;
                max_heaplify(k*2+2);
                if(k == 0) max_dis = distance[right];
                return;
            }
        }
        // parent
        if(k == 0) return;
        int parent = maxHeap[(k-1)/2];
        // > parent, then swap
        if(distance[self] > distance[parent]) {
            maxHeap[k] = parent;
            maxHeap[(k-1)/2] = self;
            max_heaplify((k-1)/2);
        }
        
    }
    void insert(int p) {
        maxHeap.push_back(p);
        max_heaplify(maxHeap.size() - 1);
        if(distance[p] > max_dis) max_dis = distance[p];
    }
};
```
Time: 327 ms, faster than 69.88% of C++ online submissions for K Closest Points to Origin.  
Memory: 58.8 MB, less than 88.44% of C++ online submissions for K Closest Points to Origin.  

Discussion:  
Using a max heap to store the k closest points.   
When there are less than k elements in the heap, we can still insert new node to the heap.  
When the heap is full of k nodes, we compare the distance of the new node to the max distance in the heap.  
If the new node has smaller distance, then we substitute the new node for the node with max distance.  
In this case, the size of the heap will remain k.  
In the end, the heap will keep k closest points.  
