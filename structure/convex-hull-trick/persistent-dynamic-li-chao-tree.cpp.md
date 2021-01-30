---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 1 \"structure/convex-hull-trick/persistent-dynamic-li-chao-tree.cpp\"\
    \ntemplate< typename T, T x_low, T x_high, T id >\nstruct PersistentDynamicLiChaoTree\
    \ {\n\n  struct Line {\n    T a, b;\n\n    Line(T a, T b) : a(a), b(b) {}\n\n\
    \    inline T get(T x) const { return a * x + b; }\n  };\n\n  struct Node {\n\
    \    Line x;\n    Node *l, *r;\n\n    Node(const Line &x) : x{x}, l{nullptr},\
    \ r{nullptr} {}\n  };\n\n  Node *root;\n\n  PersistentDynamicLiChaoTree() : root{nullptr}\
    \ {}\n\n  Node *update(Node *t, Line &x, const T &l, const T &r, const T &x_l,\
    \ const T &x_r) {\n    if(!t) return new Node(x);\n    auto t_l = t->x.get(l),\
    \ t_r = t->x.get(r);\n    if(t_l <= x_l && t_r <= x_r) {\n      return t;\n  \
    \  } else if(t_l >= x_l && t_r >= x_r) {\n      t = new Node(*t);\n      t->x\
    \ = x;\n      return t;\n    } else {\n      T m = (l + r) / 2;\n      auto t_m\
    \ = t->x.get(m), x_m = x.get(m);\n      t = new Node(*t);\n      if(t_m > x_m)\
    \ {\n        swap(t->x, x);\n        if(x_l >= t_l) t->l = update(t->l, x, l,\
    \ m, t_l, t_m);\n        else t->r = update(t->r, x, m + 1, r, t_m + x.a, t_r);\n\
    \      } else {\n        if(t_l >= x_l) t->l = update(t->l, x, l, m, x_l, x_m);\n\
    \        else t->r = update(t->r, x, m + 1, r, x_m + x.a, x_r);\n      }\n   \
    \   return t;\n    }\n  }\n\n  void update(const T &a, const T &b) {\n    Line\
    \ x(a, b);\n    root = update(root, x, x_low, x_high, x.get(x_low), x.get(x_high));\n\
    \  }\n\n  T query(const Node *t, const T &l, const T &r, const T &x) const {\n\
    \    if(!t) return id;\n    if(l == r) return t->x.get(x);\n    T m = (l + r)\
    \ / 2;\n    if(x <= m) return min(t->x.get(x), query(t->l, l, m, x));\n    else\
    \ return min(t->x.get(x), query(t->r, m + 1, r, x));\n  }\n\n  T query(const T\
    \ &x) const {\n    return query(root, x_low, x_high, x);\n  }\n};\n"
  code: "template< typename T, T x_low, T x_high, T id >\nstruct PersistentDynamicLiChaoTree\
    \ {\n\n  struct Line {\n    T a, b;\n\n    Line(T a, T b) : a(a), b(b) {}\n\n\
    \    inline T get(T x) const { return a * x + b; }\n  };\n\n  struct Node {\n\
    \    Line x;\n    Node *l, *r;\n\n    Node(const Line &x) : x{x}, l{nullptr},\
    \ r{nullptr} {}\n  };\n\n  Node *root;\n\n  PersistentDynamicLiChaoTree() : root{nullptr}\
    \ {}\n\n  Node *update(Node *t, Line &x, const T &l, const T &r, const T &x_l,\
    \ const T &x_r) {\n    if(!t) return new Node(x);\n    auto t_l = t->x.get(l),\
    \ t_r = t->x.get(r);\n    if(t_l <= x_l && t_r <= x_r) {\n      return t;\n  \
    \  } else if(t_l >= x_l && t_r >= x_r) {\n      t = new Node(*t);\n      t->x\
    \ = x;\n      return t;\n    } else {\n      T m = (l + r) / 2;\n      auto t_m\
    \ = t->x.get(m), x_m = x.get(m);\n      t = new Node(*t);\n      if(t_m > x_m)\
    \ {\n        swap(t->x, x);\n        if(x_l >= t_l) t->l = update(t->l, x, l,\
    \ m, t_l, t_m);\n        else t->r = update(t->r, x, m + 1, r, t_m + x.a, t_r);\n\
    \      } else {\n        if(t_l >= x_l) t->l = update(t->l, x, l, m, x_l, x_m);\n\
    \        else t->r = update(t->r, x, m + 1, r, x_m + x.a, x_r);\n      }\n   \
    \   return t;\n    }\n  }\n\n  void update(const T &a, const T &b) {\n    Line\
    \ x(a, b);\n    root = update(root, x, x_low, x_high, x.get(x_low), x.get(x_high));\n\
    \  }\n\n  T query(const Node *t, const T &l, const T &r, const T &x) const {\n\
    \    if(!t) return id;\n    if(l == r) return t->x.get(x);\n    T m = (l + r)\
    \ / 2;\n    if(x <= m) return min(t->x.get(x), query(t->l, l, m, x));\n    else\
    \ return min(t->x.get(x), query(t->r, m + 1, r, x));\n  }\n\n  T query(const T\
    \ &x) const {\n    return query(root, x_low, x_high, x);\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/convex-hull-trick/persistent-dynamic-li-chao-tree.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/convex-hull-trick/persistent-dynamic-li-chao-tree.cpp
layout: document
redirect_from:
- /library/structure/convex-hull-trick/persistent-dynamic-li-chao-tree.cpp
- /library/structure/convex-hull-trick/persistent-dynamic-li-chao-tree.cpp.html
title: structure/convex-hull-trick/persistent-dynamic-li-chao-tree.cpp
---
