# Phone directory

[![Problem Link](https://img.shields.io/badge/GeeksforGeeks-298D46?style=for-the-badge&logo=geeksforgeeks&logoColor=white)](https://practice.geeksforgeeks.org/problems/phone-directory4628/1/#)

Given a list of contacts contact[] of length n where each contact is a string which exist in a phone directory and a query string s. The task is to implement a search query for the phone directory. Run a search query for each prefix p of the query string s (i.e. from  index 1 to |s|) that prints all the distinct contacts which have the same prefix as p in lexicographical increasing order. Please refer the explanation part for better understanding.

**Note:** If there is no match between query and contacts, print "0".

### Sample Input
```
3
geeikistest geeksforgeeks geeksfortest
geeips
```

### Sample Output
```
geeikistest geeksforgeeks geeksfortest 
geeikistest geeksforgeeks geeksfortest 
geeikistest geeksforgeeks geeksfortest 
geeikistest 
0 
0 
```

### Solution
```cpp

class TrieNode {
    public:

    TrieNode* child[26];
    char value;
    int ends, depth;

    TrieNode(char letter, int d) {
        value = letter;
        ends = 0;
        depth = d;

        for(int i = 0; i < 26; ++i) {
            child[i] = NULL;
        }
    }
};

class Trie {
    public:

    TrieNode* root;

    Trie() {
        root = new TrieNode('/', 0);
    }

    void insert(string& word) {
        TrieNode* node = root;

        for(int i = 0; i < word.size(); ++i) {
            int index = word[i] - 'a';

            if(node->child[index] == NULL)
                node->child[index] = new TrieNode(word[i], i + 1);

            node = node->child[index];
        }

        node->ends += 1;
    }
    
    vector<string> wordsWithPrefix(string prefix) {
        TrieNode* node = root;
        vector<string> results;
    
        int N = prefix.length();
        for(int i = 0; i < N; ++i) {
            node = node->child[prefix[i] - 'a'];
            if(node == NULL) return results;
        }
        TrieNode* prefix_end = node;

        stack<TrieNode*> nodes;
        nodes.push(node);
        string stream = "";
        
        while(!nodes.empty()) {
            node = nodes.top();
            nodes.pop();
        
            if(stream.size() > node->depth - prefix_end->depth) {
                stream = stream.substr(0, node->depth - prefix_end->depth);
            }
            
            stream += node->value;
            for(int i = 25; i >= 0; --i) {
                if(node->child[i] != NULL) {
                    nodes.push(node->child[i]);
                }
            }
            
            if(node->ends) {
                results.push_back(prefix + stream.substr(1));
            }
        }

        return results;
    }
};

class Solution{
public:
    vector<vector<string>> displayContacts(int n, string contact[], string s)
    {
        Trie* dict = new Trie();
        for(int i = 0; i < n; ++i) {
            dict->insert(contact[i]);
        }

        vector<vector<string>> ans(s.size());
        
        for(int i = 0; i < s.size(); ++i) {
            vector<string> res = dict->wordsWithPrefix(s.substr(0, i + 1));
            if(res.empty()) {
                ans[i] = {"0"};
            }
            else {
                ans[i] = res;
            }
        }
        return ans;
    }
};
```

### Accepted
[![image](https://user-images.githubusercontent.com/44930179/148439620-cfd6d275-3746-4b1d-90b7-63e49c3e7115.png)](#)
