# leetcode 208 实现 Trie (前缀树)

Trie 树的实现。注意 N 是最大的可能结点数。

```c++
class Trie {
    static const int N = 2010 * 26;
    int son[N][26];
    int cnt[N];
    int idx;
public:
    Trie() {
        memset(son, 0, sizeof son), memset(cnt, 0, sizeof cnt);
        idx = 0;
    }
    
    void insert(string word) {
        int p = 0;
        for(auto t: word){
            int u = t - 'a';
            if(son[p][u] == 0) son[p][u] = ++ idx;
            p = son[p][u];
        }
        cnt[p] ++;
    }
    
    bool search(string word) {
        int p = 0;
        for(auto t:word){
            int u = t - 'a';
            if(son[p][u]) p = son[p][u];
            else return false;
        }
        return cnt[p];
    }
    
    bool startsWith(string prefix) {
        int p = 0;
        for(auto t: prefix){
            int u = t - 'a';
            if(son[p][u]) p = son[p][u];
            else return false;
        }
        return true;
    }
};
```

