Given a list of accounts where each element accounts[i] is a list of strings, where the first element accounts[i][0] is a name, and the rest of the elements are emails representing emails of the account.  

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some common email to both accounts. Note that even if two accounts have the same name,  
they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.  

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails in sorted order. The accounts themselves can be returned in any order.   

Example 1:  
```
Input: accounts = [["John","johnsmith@mail.com","john_newyork@mail.com"],["John","johnsmith@mail.com","john00@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]
Output: [["John","john00@mail.com","john_newyork@mail.com","johnsmith@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]
Explanation:
The first and second John's are the same person as they have the common email "johnsmith@mail.com".
The third John and Mary are different people as none of their email addresses are used by other accounts.
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], 
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
```

Example 2:  
```
Input: accounts = [["Gabe","Gabe0@m.co","Gabe3@m.co","Gabe1@m.co"],["Kevin","Kevin3@m.co","Kevin5@m.co","Kevin0@m.co"],["Ethan","Ethan5@m.co","Ethan4@m.co","Ethan0@m.co"],["Hanzo","Hanzo3@m.co","Hanzo1@m.co","Hanzo0@m.co"],["Fern","Fern5@m.co","Fern1@m.co","Fern0@m.co"]]
Output: [["Ethan","Ethan0@m.co","Ethan4@m.co","Ethan5@m.co"],["Gabe","Gabe0@m.co","Gabe1@m.co","Gabe3@m.co"],["Hanzo","Hanzo0@m.co","Hanzo1@m.co","Hanzo3@m.co"],["Kevin","Kevin0@m.co","Kevin3@m.co","Kevin5@m.co"],["Fern","Fern0@m.co","Fern1@m.co","Fern5@m.co"]]
```

Code:  
```c++
struct node {
    string owner;
    string key;
    vector<node*> neighbors;
    int visited;    // 0: not visited; 1: visited; 2: complete
};
class Solution {
public:
    vector<vector<string>> accountsMerge(vector<vector<string>>& accounts) {
        // construct the round linked list
        for(int i = 0; i < accounts.size(); ++i) {
            if(account.find(accounts[i].back()) == account.end()) account[accounts[i].back()] = make_node(accounts[i][0], accounts[i].back());
            for(int j = accounts[i].size() - 2; j >= 1; --j) {
                if(account.find(accounts[i][j]) == account.end()) account[accounts[i][j]] = make_node(accounts[i][0], accounts[i][j], &account[accounts[i][j+1]]);
                else account[accounts[i][j]].neighbors.push_back(&account[accounts[i][j+1]]);
            }
            account[accounts[i].back()].neighbors.push_back(&account[accounts[i][1]]);
        }
        vector<vector<string>> mergedAccounts;
        for(auto& a : account) {
            if(a.second.visited) continue;
            vector<string> oneAccount = {a.second.owner};
            dfs(&a.second, oneAccount);
            sort(oneAccount.begin()+1, oneAccount.end());
            mergedAccounts.push_back(oneAccount);
        }
        return mergedAccounts;
    }
private:
    node make_node(string _owner, string _key) {
        node n = {
            .owner = _owner,
            .key = _key,
            .visited = 0
        };
        return n;
    }
    node make_node(string _owner, string _key, node* _n0) {
        node n = {
            .owner = _owner,
            .key = _key,
            .neighbors = {_n0},
            .visited = 0
        };
        return n;
    }
    map<string, node> account;
    void dfs(node* n, vector<string>& oneAccount) {
        n -> visited = 1;
        oneAccount.push_back(n -> key);
        for(int i = 0; i < n -> neighbors.size(); ++i) {
            if(!n -> neighbors[i] -> visited) dfs(n -> neighbors[i], oneAccount);
        }
        n -> visited = 2;
    }
};
```

Runtime: 159 ms, faster than 15.8% of C++ online submissions.  
Memory Usage: 37.3 MB, less than 24.68% of C++ online submissions.
