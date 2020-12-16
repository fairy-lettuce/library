---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: graph/mst/prim-fibonacchi-heap.cpp
    title: "Prim-Fibonacchi-Heap(\u6700\u5C0F\u5168\u57DF\u6728)"
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-1-a-2.test.cpp
    title: test/verify/aoj-grl-1-a-2.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-grl-2-a-4.test.cpp
    title: test/verify/aoj-grl-2-a-4.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    document_title: "Fibonacchi-Heap(\u30D5\u30A3\u30DC\u30CA\u30C3\u30C1\u30D2\u30FC\
      \u30D7)"
    links:
    - https://www.cs.princeton.edu/~wayne/teaching/fibonacci-heap.pdf
  bundledCode: "#line 1 \"structure/heap/fibonacchi-heap.cpp\"\n/**\n * @brief Fibonacchi-Heap(\u30D5\
    \u30A3\u30DC\u30CA\u30C3\u30C1\u30D2\u30FC\u30D7)\n * @see https://www.cs.princeton.edu/~wayne/teaching/fibonacci-heap.pdf\n\
    \ */\ntemplate< typename key_t, typename val_t >\nstruct FibonacchiHeap {\n  struct\
    \ Node {\n    key_t key;\n    val_t val;\n    Node *left, *right, *child, *par;\n\
    \    int sz;\n    bool mark;\n\n    Node(const key_t &key, const val_t &val)\n\
    \        : key(key), val(val), left(this), right(this), par(nullptr), child(nullptr),\
    \ sz(0), mark(false) {}\n  };\n\n  Node *root;\n  size_t sz;\n  vector< Node *\
    \ > rank;\n\n  FibonacchiHeap() : root(nullptr), sz(0) {}\n\n  size_t size() const\
    \ {\n    return sz;\n  }\n\n  bool empty() const {\n    return sz == 0;\n  }\n\
    \n  void update_min(Node *t) {\n    if(!root || t->key < root->key) {\n      root\
    \ = t;\n    }\n  }\n\n  void concat(Node *&r, Node *t) {\n    if(!r) {\n     \
    \ r = t;\n    } else {\n      t->left->right = r->right;\n      r->right->left\
    \ = t->left;\n      t->left = r;\n      r->right = t;\n    }\n  }\n\n  void delete_node(Node\
    \ *t) {\n    t->left->right = t->right;\n    t->right->left = t->left;\n    t->left\
    \ = t;\n    t->right = t;\n  }\n\n  Node *push(const key_t &key, const val_t &val)\
    \ {\n    ++sz;\n    auto node = new Node(key, val);\n    concat(root, node);\n\
    \    update_min(node);\n    return node;\n  }\n\n\n  Node *consolidate(Node *s,\
    \ Node *t) {\n    if(root == s || s->key < t->key) {\n      delete_node(t);\n\
    \      ++s->sz;\n      t->par = s;\n      concat(s->child, t);\n      return s;\n\
    \    } else {\n      delete_node(s);\n      ++t->sz;\n      s->par = t;\n    \
    \  concat(t->child, s);\n      return t;\n    }\n  }\n\n\n  pair< key_t, val_t\
    \ > pop() {\n    --sz;\n\n    Node *rem = root;\n\n\n    auto ret = make_pair(rem->key,\
    \ rem->val);\n\n    {\n      root = root->left == root ? nullptr : root->left;\n\
    \      delete_node(rem);\n    }\n\n\n    if(rem->child) {\n      concat(root,\
    \ rem->child);\n    }\n\n\n    if(root) {\n\n      {\n        Node *base = root,\
    \ *cur = base;\n        do {\n          cur->par = nullptr;\n          update_min(cur);\n\
    \          cur = cur->right;\n        } while(cur != base);\n      }\n\n\n   \
    \   {\n        Node *base = root;\n        int last = -1;\n        do {\n    \
    \      Node *nxt = base->right;\n          while(base->sz < rank.size() && rank[base->sz])\
    \ {\n            Node *u = rank[base->sz];\n            rank[base->sz] = nullptr;\n\
    \            base = consolidate(u, base);\n          }\n          if(base->sz\
    \ >= rank.size()) rank.resize(base->sz + 1);\n          last = max(last, base->sz);\n\
    \          rank[base->sz] = base;\n          base = nxt;\n        } while(base\
    \ != root);\n\n        for(int i = last; i >= 0; i--) rank[i] = nullptr;\n   \
    \   }\n    }\n\n    return ret;\n  }\n\n  inline void mark_dfs(Node *t) {\n  \
    \  if(!t->par) {\n      t->mark = false;\n    } else if(t->mark) {\n      mark_dfs(t->par);\n\
    \      t->par->child = t->left == t ? nullptr : t->left;\n      delete_node(t);\n\
    \      t->sz--;\n      t->mark = false;\n      t->par = nullptr;\n      concat(root,\
    \ t);\n    } else {\n      t->mark = true;\n      t->sz--;\n    }\n  }\n\n\n \
    \ void decrease_key(Node *t, const key_t &d) {\n    t->key -= d;\n\n    if(!t->par)\
    \ {\n      update_min(t);\n      return;\n    }\n\n    if(t->par->key <= t->key)\
    \ {\n      return;\n    }\n\n    t->sz++;\n    t->mark = true;\n    mark_dfs(t);\n\
    \    update_min(t);\n  }\n};\n"
  code: "/**\n * @brief Fibonacchi-Heap(\u30D5\u30A3\u30DC\u30CA\u30C3\u30C1\u30D2\
    \u30FC\u30D7)\n * @see https://www.cs.princeton.edu/~wayne/teaching/fibonacci-heap.pdf\n\
    \ */\ntemplate< typename key_t, typename val_t >\nstruct FibonacchiHeap {\n  struct\
    \ Node {\n    key_t key;\n    val_t val;\n    Node *left, *right, *child, *par;\n\
    \    int sz;\n    bool mark;\n\n    Node(const key_t &key, const val_t &val)\n\
    \        : key(key), val(val), left(this), right(this), par(nullptr), child(nullptr),\
    \ sz(0), mark(false) {}\n  };\n\n  Node *root;\n  size_t sz;\n  vector< Node *\
    \ > rank;\n\n  FibonacchiHeap() : root(nullptr), sz(0) {}\n\n  size_t size() const\
    \ {\n    return sz;\n  }\n\n  bool empty() const {\n    return sz == 0;\n  }\n\
    \n  void update_min(Node *t) {\n    if(!root || t->key < root->key) {\n      root\
    \ = t;\n    }\n  }\n\n  void concat(Node *&r, Node *t) {\n    if(!r) {\n     \
    \ r = t;\n    } else {\n      t->left->right = r->right;\n      r->right->left\
    \ = t->left;\n      t->left = r;\n      r->right = t;\n    }\n  }\n\n  void delete_node(Node\
    \ *t) {\n    t->left->right = t->right;\n    t->right->left = t->left;\n    t->left\
    \ = t;\n    t->right = t;\n  }\n\n  Node *push(const key_t &key, const val_t &val)\
    \ {\n    ++sz;\n    auto node = new Node(key, val);\n    concat(root, node);\n\
    \    update_min(node);\n    return node;\n  }\n\n\n  Node *consolidate(Node *s,\
    \ Node *t) {\n    if(root == s || s->key < t->key) {\n      delete_node(t);\n\
    \      ++s->sz;\n      t->par = s;\n      concat(s->child, t);\n      return s;\n\
    \    } else {\n      delete_node(s);\n      ++t->sz;\n      s->par = t;\n    \
    \  concat(t->child, s);\n      return t;\n    }\n  }\n\n\n  pair< key_t, val_t\
    \ > pop() {\n    --sz;\n\n    Node *rem = root;\n\n\n    auto ret = make_pair(rem->key,\
    \ rem->val);\n\n    {\n      root = root->left == root ? nullptr : root->left;\n\
    \      delete_node(rem);\n    }\n\n\n    if(rem->child) {\n      concat(root,\
    \ rem->child);\n    }\n\n\n    if(root) {\n\n      {\n        Node *base = root,\
    \ *cur = base;\n        do {\n          cur->par = nullptr;\n          update_min(cur);\n\
    \          cur = cur->right;\n        } while(cur != base);\n      }\n\n\n   \
    \   {\n        Node *base = root;\n        int last = -1;\n        do {\n    \
    \      Node *nxt = base->right;\n          while(base->sz < rank.size() && rank[base->sz])\
    \ {\n            Node *u = rank[base->sz];\n            rank[base->sz] = nullptr;\n\
    \            base = consolidate(u, base);\n          }\n          if(base->sz\
    \ >= rank.size()) rank.resize(base->sz + 1);\n          last = max(last, base->sz);\n\
    \          rank[base->sz] = base;\n          base = nxt;\n        } while(base\
    \ != root);\n\n        for(int i = last; i >= 0; i--) rank[i] = nullptr;\n   \
    \   }\n    }\n\n    return ret;\n  }\n\n  inline void mark_dfs(Node *t) {\n  \
    \  if(!t->par) {\n      t->mark = false;\n    } else if(t->mark) {\n      mark_dfs(t->par);\n\
    \      t->par->child = t->left == t ? nullptr : t->left;\n      delete_node(t);\n\
    \      t->sz--;\n      t->mark = false;\n      t->par = nullptr;\n      concat(root,\
    \ t);\n    } else {\n      t->mark = true;\n      t->sz--;\n    }\n  }\n\n\n \
    \ void decrease_key(Node *t, const key_t &d) {\n    t->key -= d;\n\n    if(!t->par)\
    \ {\n      update_min(t);\n      return;\n    }\n\n    if(t->par->key <= t->key)\
    \ {\n      return;\n    }\n\n    t->sz++;\n    t->mark = true;\n    mark_dfs(t);\n\
    \    update_min(t);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/heap/fibonacchi-heap.cpp
  requiredBy:
  - graph/mst/prim-fibonacchi-heap.cpp
  timestamp: '2020-08-20 17:25:40+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-grl-2-a-4.test.cpp
  - test/verify/aoj-grl-1-a-2.test.cpp
documentation_of: structure/heap/fibonacchi-heap.cpp
layout: document
redirect_from:
- /library/structure/heap/fibonacchi-heap.cpp
- /library/structure/heap/fibonacchi-heap.cpp.html
title: "Fibonacchi-Heap(\u30D5\u30A3\u30DC\u30CA\u30C3\u30C1\u30D2\u30FC\u30D7)"
---
