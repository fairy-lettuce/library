---
layout: default
---

<!-- mathjax config similar to math.stackexchange -->
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: { equationNumbers: { autoNumber: "AMS" }},
    tex2jax: {
      inlineMath: [ ['$','$'] ],
      processEscapes: true
    },
    "HTML-CSS": { matchFontHeight: false },
    displayAlign: "left",
    displayIndent: "2em"
  });
</script>

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jquery-balloon-js@1.1.2/jquery.balloon.min.js" integrity="sha256-ZEYs9VrgAeNuPvs15E39OsyOJaIkXEEt10fzxJ20+2I=" crossorigin="anonymous"></script>
<script type="text/javascript" src="../../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../../assets/css/copy-button.css" />


# :warning: structure/trie/persistent-binary-trie.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#495454930b047da7eed81bd52d55784a">structure/trie</a>
* <a href="{{ site.github.repository_url }}/blob/master/structure/trie/persistent-binary-trie.cpp">View this file on GitHub</a>
    - Last commit date: 2019-11-30 22:41:48 +0900




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T >
struct BinaryTrieNode {
  using Node = BinaryTrieNode< T >;
 
  BinaryTrieNode< T > *nxt[2];
  int max_index;
 
  BinaryTrieNode() : max_index(-1) {
    nxt[0] = nxt[1] = nullptr;
  }
 
  void update_direct(int id) {
    max_index = max(max_index, id);
  }
 
  void update_child(Node *child, int id) {
    max_index = max(max_index, id);
  }
 
  Node *add(const T &bit, int bit_index, int id, bool need = true) {
    Node *node = need ? new Node(*this) : this;
    if(bit_index == -1) {
      node->update_direct(id);
    } else {
      const int c = (bit >> bit_index) & 1;
      if(node->nxt[c] == nullptr) node->nxt[c] = new Node(), need = false;
      node->nxt[c] = node->nxt[c]->add(bit, bit_index - 1, id, need);
      node->update_child(node->nxt[c], id);
    }
    return node;
  }
 
  inline T min_query(T bit, int bit_index, int bit2, int l) {
    if(bit_index == -1) return bit;
    int c = (bit2 >> bit_index) & 1;
    if(nxt[c] != nullptr && l <= nxt[c]->max_index) {
      return nxt[c]->min_query(bit, bit_index - 1, bit2, l);
    } else {
      return nxt[1 ^ c]->min_query(bit | (1LL << bit_index), bit_index - 1, bit2, l);
    }
  }
};
 
template< typename T, int MAX_LOG >
struct PersistentBinaryTrie {
  using Node = BinaryTrieNode< T >;
  Node *root;
 
  PersistentBinaryTrie(Node *root) : root(root) {}
 
  PersistentBinaryTrie() : root(new Node()) {}
 
  PersistentBinaryTrie add(const T &bit, int id) {
    return PersistentBinaryTrie(root->add(bit, MAX_LOG, id));
  }
 
  T min_query(int bit, int l) {
    return root->min_query(0, MAX_LOG, bit, l);
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "structure/trie/persistent-binary-trie.cpp"
template< typename T >
struct BinaryTrieNode {
  using Node = BinaryTrieNode< T >;
 
  BinaryTrieNode< T > *nxt[2];
  int max_index;
 
  BinaryTrieNode() : max_index(-1) {
    nxt[0] = nxt[1] = nullptr;
  }
 
  void update_direct(int id) {
    max_index = max(max_index, id);
  }
 
  void update_child(Node *child, int id) {
    max_index = max(max_index, id);
  }
 
  Node *add(const T &bit, int bit_index, int id, bool need = true) {
    Node *node = need ? new Node(*this) : this;
    if(bit_index == -1) {
      node->update_direct(id);
    } else {
      const int c = (bit >> bit_index) & 1;
      if(node->nxt[c] == nullptr) node->nxt[c] = new Node(), need = false;
      node->nxt[c] = node->nxt[c]->add(bit, bit_index - 1, id, need);
      node->update_child(node->nxt[c], id);
    }
    return node;
  }
 
  inline T min_query(T bit, int bit_index, int bit2, int l) {
    if(bit_index == -1) return bit;
    int c = (bit2 >> bit_index) & 1;
    if(nxt[c] != nullptr && l <= nxt[c]->max_index) {
      return nxt[c]->min_query(bit, bit_index - 1, bit2, l);
    } else {
      return nxt[1 ^ c]->min_query(bit | (1LL << bit_index), bit_index - 1, bit2, l);
    }
  }
};
 
template< typename T, int MAX_LOG >
struct PersistentBinaryTrie {
  using Node = BinaryTrieNode< T >;
  Node *root;
 
  PersistentBinaryTrie(Node *root) : root(root) {}
 
  PersistentBinaryTrie() : root(new Node()) {}
 
  PersistentBinaryTrie add(const T &bit, int id) {
    return PersistentBinaryTrie(root->add(bit, MAX_LOG, id));
  }
 
  T min_query(int bit, int l) {
    return root->min_query(0, MAX_LOG, bit, l);
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

