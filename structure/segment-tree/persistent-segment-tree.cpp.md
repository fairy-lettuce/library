---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    _deprecated_at_docs: docs/persistent-segment-tree.md
    document_title: "Persistent-Segment-Tree(\u6C38\u7D9A\u30BB\u30B0\u30E1\u30F3\u30C8\
      \u6728)"
    links: []
  bundledCode: "#line 1 \"structure/segment-tree/persistent-segment-tree.cpp\"\n/**\n\
    \ * @brief Persistent-Segment-Tree(\u6C38\u7D9A\u30BB\u30B0\u30E1\u30F3\u30C8\u6728\
    )\n * @docs docs/persistent-segment-tree.md\n */\ntemplate< typename Monoid >\n\
    struct PersistentSegmentTree {\n  using F = function< Monoid(Monoid, Monoid) >;\n\
    \n  struct Node {\n    Monoid data;\n    Node *l, *r;\n\n    Node(const Monoid\
    \ &data) : data(data), l(nullptr), r(nullptr) {}\n  };\n\n  int sz;\n  const F\
    \ f;\n  const Monoid M1;\n\n  PersistentSegmentTree(const F f, const Monoid &M1)\
    \ : f(f), M1(M1) {}\n\n  Node *build(vector< Monoid > &v) {\n    sz = (int) v.size();\n\
    \    return build(0, (int) v.size(), v);\n  }\n\n  Node *merge(Node *l, Node *r)\
    \ {\n    auto t = new Node(f(l->data, r->data));\n    t->l = l;\n    t->r = r;\n\
    \    return t;\n  }\n\n  Node *build(int l, int r, vector< Monoid > &v) {\n  \
    \  if(l + 1 >= r) return new Node(v[l]);\n    return merge(build(l, (l + r) >>\
    \ 1, v), build((l + r) >> 1, r, v));\n  }\n\n  Node *update(int a, const Monoid\
    \ &x, Node *k, int l, int r) {\n    if(r <= a || a + 1 <= l) {\n      return k;\n\
    \    } else if(a <= l && r <= a + 1) {\n      return new Node(x);\n    } else\
    \ {\n      return merge(update(a, x, k->l, l, (l + r) >> 1), update(a, x, k->r,\
    \ (l + r) >> 1, r));\n    }\n  }\n\n  Node *update(Node *t, int k, const Monoid\
    \ &x) {\n    return update(k, x, t, 0, sz);\n  }\n\n  Monoid query(int a, int\
    \ b, Node *k, int l, int r) {\n    if(r <= a || b <= l) {\n      return M1;\n\
    \    } else if(a <= l && r <= b) {\n      return k->data;\n    } else {\n    \
    \  return f(query(a, b, k->l, l, (l + r) >> 1),\n               query(a, b, k->r,\
    \ (l + r) >> 1, r));\n    }\n  }\n\n  Monoid query(Node *t, int a, int b) {\n\
    \    return query(a, b, t, 0, sz);\n  }\n};\n"
  code: "/**\n * @brief Persistent-Segment-Tree(\u6C38\u7D9A\u30BB\u30B0\u30E1\u30F3\
    \u30C8\u6728)\n * @docs docs/persistent-segment-tree.md\n */\ntemplate< typename\
    \ Monoid >\nstruct PersistentSegmentTree {\n  using F = function< Monoid(Monoid,\
    \ Monoid) >;\n\n  struct Node {\n    Monoid data;\n    Node *l, *r;\n\n    Node(const\
    \ Monoid &data) : data(data), l(nullptr), r(nullptr) {}\n  };\n\n  int sz;\n \
    \ const F f;\n  const Monoid M1;\n\n  PersistentSegmentTree(const F f, const Monoid\
    \ &M1) : f(f), M1(M1) {}\n\n  Node *build(vector< Monoid > &v) {\n    sz = (int)\
    \ v.size();\n    return build(0, (int) v.size(), v);\n  }\n\n  Node *merge(Node\
    \ *l, Node *r) {\n    auto t = new Node(f(l->data, r->data));\n    t->l = l;\n\
    \    t->r = r;\n    return t;\n  }\n\n  Node *build(int l, int r, vector< Monoid\
    \ > &v) {\n    if(l + 1 >= r) return new Node(v[l]);\n    return merge(build(l,\
    \ (l + r) >> 1, v), build((l + r) >> 1, r, v));\n  }\n\n  Node *update(int a,\
    \ const Monoid &x, Node *k, int l, int r) {\n    if(r <= a || a + 1 <= l) {\n\
    \      return k;\n    } else if(a <= l && r <= a + 1) {\n      return new Node(x);\n\
    \    } else {\n      return merge(update(a, x, k->l, l, (l + r) >> 1), update(a,\
    \ x, k->r, (l + r) >> 1, r));\n    }\n  }\n\n  Node *update(Node *t, int k, const\
    \ Monoid &x) {\n    return update(k, x, t, 0, sz);\n  }\n\n  Monoid query(int\
    \ a, int b, Node *k, int l, int r) {\n    if(r <= a || b <= l) {\n      return\
    \ M1;\n    } else if(a <= l && r <= b) {\n      return k->data;\n    } else {\n\
    \      return f(query(a, b, k->l, l, (l + r) >> 1),\n               query(a, b,\
    \ k->r, (l + r) >> 1, r));\n    }\n  }\n\n  Monoid query(Node *t, int a, int b)\
    \ {\n    return query(a, b, t, 0, sz);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/segment-tree/persistent-segment-tree.cpp
  requiredBy: []
  timestamp: '2020-02-20 22:23:04+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/segment-tree/persistent-segment-tree.cpp
layout: document
redirect_from:
- /library/structure/segment-tree/persistent-segment-tree.cpp
- /library/structure/segment-tree/persistent-segment-tree.cpp.html
title: "Persistent-Segment-Tree(\u6C38\u7D9A\u30BB\u30B0\u30E1\u30F3\u30C8\u6728)"
---
## 概要

セグメント木のある要素に対して何らかの更新を行うとする. ここで更新後のセグメント木をすべてコピーして残しておくことが永続であるが, これを単純に実装すると, $1$ 回のコピーに $O(N)$ かかってこわれてしまう. $1$ 回の更新によって $O(\log N)$ 個のノードの情報しか変化しないので, 変化したノードの情報だけ新しくノードを生成してその部分のみ張り替えるする操作を行えば $O(\log N)$ でのコピーが可能になり, これは一般のセグメント木の計算量と変わらない.

* `PersistentSegmentTree(f, M1)`: `f` は2つの区間の要素をマージする二項演算, `M1` はモノイドの単位元である.
* `build(v)`: 配列 `v` を各要素としたセグメント木を構築し, その根を返す.
* `update(t, k, x)`: `t` を根とするセグメント木に対し `k` 番目の要素を `x` に更新し, 更新後の根を返す.
* `query(t, a, b)`: `t` を根とするセグメント木に対し, 区間 $[a, b)$ の要素を二項演算した結果を返す.

## 計算量

* `build(v)`: $O(N)$
* クエリ: $O(\log N)$ 
