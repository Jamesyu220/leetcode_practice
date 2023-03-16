A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings.  
There are various applications of this data structure, such as autocomplete and spellchecker.  

Implement the Trie class:  

Trie() Initializes the trie object.  
void insert(String word) Inserts the string word into the trie.  
boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.  
boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.  
 
Example 1:    
```
Input
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output
[null, null, true, false, true, null, true]

Explanation
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
```

Code:  
```c++
class TrieNode {
public:
    int val;
    vector<TrieNode*> children;
    bool isLeaf;
    TrieNode() {
        val = 0;
        children = vector<TrieNode*>();
        isLeaf = false;
    }
    TrieNode(int _val) {
        val = _val;
        children = vector<TrieNode*>();
        isLeaf = false;
    }
    TrieNode(int _val, bool _isLeaf) {
        val = _val;
        children = vector<TrieNode*>();
        isLeaf = _isLeaf;
    }
};

class Trie {
public:
    Trie() {
        root = new TrieNode();
    }
    
    void insert(string word) {
        TrieNode* ptr = root;
        for(int i = 0; i < word.size(); ++i) {
            bool existed = false;
            for(int j = 0; j < ptr -> children.size(); ++j) {
                if(ptr -> children[j] -> val == word[i] - 'a') {
                    ptr = ptr -> children[j];
                    existed = true;
                    if(i == word.size() - 1) ptr -> isLeaf = true;
                    break;
                }
            }
            if(!existed) {
                TrieNode* newNode;
                if(i == word.size() - 1) newNode = new TrieNode(word[i] - 'a', true);
                else newNode = new TrieNode(word[i] - 'a');

                ptr -> children.push_back(newNode);
                ptr = ptr -> children.back();
            }
        }
        
    }
    
    bool search(string word) {
        TrieNode* ptr = root;
        for(int i = 0; i < word.size() - 1; ++i) {
            bool existed = false;
            for(int j = 0; j < ptr -> children.size(); ++j) {
                if(ptr -> children[j] -> val == word[i] - 'a') {
                    if(i == word.size() - 1) return ptr -> children[j] -> isLeaf;
                    ptr = ptr -> children[j];
                    existed = true;
                    break;
                }
            }
            if(!existed) return false;
        }
        for(int j = 0; j < ptr -> children.size(); ++j) {
            if(ptr -> children[j] -> val == word.back() - 'a') return ptr -> children[j] -> isLeaf;
        }
        return false;
    }
    
    bool startsWith(string prefix) {
        TrieNode* ptr = root;
        for(int i = 0; i < prefix.size() - 1; ++i) {
            bool existed = false;
            for(int j = 0; j < ptr -> children.size(); ++j) {
                if(ptr -> children[j] -> val == prefix[i] - 'a') {
                    if(i == prefix.size() - 1) return true;
                    ptr = ptr -> children[j];
                    existed = true;
                    break;
                }
            }
            if(!existed) return false;
        }
        for(int j = 0; j < ptr -> children.size(); ++j) {
            if(ptr -> children[j] -> val == prefix.back() - 'a') return true;
        }
        return false;
    }
private:
    TrieNode* root;
};


/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
 ```
Runtime: 72 ms, faster than 51.7% of C++ online submissions.  
Memory Usage: 29.7 MB, less than 97.9% of C++ online submissions.
