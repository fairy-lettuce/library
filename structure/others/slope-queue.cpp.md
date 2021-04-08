---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    _deprecated_at_docs: docs/slope-queue.md
    document_title: Slope-Queue
    links:
    - https://maspypy.com/slope-trick-1-%E8%A7%A3%E8%AA%AC%E7%B7%A8
  bundledCode: "#line 1 \"structure/others/slope-queue.cpp\"\n/**\n * @brief Slope-Queue\n\
    \ * @see https://maspypy.com/slope-trick-1-%E8%A7%A3%E8%AA%AC%E7%B7%A8\n * @docs\
    \ docs/slope-queue.md\n */\ntemplate< typename T >\nstruct SlopeQueue {\n\n  const\
    \ T INF = numeric_limits< T >::max() / 3;\n\n  T min_f;\n  priority_queue< T,\
    \ vector< T >, less<> > L;\n  priority_queue< T, vector< T >, greater<> > R;\n\
    \  T add_l, add_r;\n\nprivate:\n  void push_R(const T &a) {\n    R.push(a - add_r);\n\
    \  }\n\n  T top_R() const {\n    return R.top() + add_r;\n  }\n\n  T pop_R() {\n\
    \    T val = top_R();\n    R.pop();\n    return val;\n  }\n\n  void push_L(const\
    \ T &a) {\n    L.push(a - add_l);\n  }\n\n  T top_L() const {\n    return L.top()\
    \ + add_l;\n  }\n\n  T pop_L() {\n    T val = top_L();\n    L.pop();\n    return\
    \ val;\n  }\n\n  size_t size() {\n    return L.size() + R.size() - 2;\n  }\n\n\
    public:\n  SlopeQueue() : min_f(0), add_l(0), add_r(0) {\n    L.push(-INF);\n\
    \    R.push(INF);\n  }\n\n  struct Query {\n    T lx, rx, min_f;\n  };\n\n  //\
    \ return min f(x)\n  Query query() const {\n    return (Query) {top_L(), top_R(),\
    \ min_f};\n  }\n\n  // f(x) += a\n  void add_all(const T &a) {\n    min_f += a;\n\
    \  }\n\n  // add \\_\n  // f(x) += max(a - x, 0)\n  void add_a_minus_x(const T\
    \ &a) {\n    min_f += max(T(0), a - top_R());\n    push_R(a);\n    push_L(pop_R());\n\
    \  }\n\n  // add _/\n  // f(x) += max(x - a, 0)\n  void add_x_minus_a(const T\
    \ &a) {\n    min_f += max(T(0), top_L() - a);\n    push_L(a);\n    push_R(pop_L());\n\
    \  }\n\n  // add \\/\n  // f(x) += abs(x - a)\n  void add_abs(const T &a) {\n\
    \    add_a_minus_x(a);\n    add_x_minus_a(a);\n  }\n\n  // \\/ -> \\_\n  // f_{new}\
    \ (x) = min f(y) (y <= x)\n  void clear_right() {\n    while(R.size() >= 2) R.pop();\n\
    \  }\n\n  // \\/ -> _/\n  // f_{new} (x) = min f(y) (y >= x)\n  void clear_left()\
    \ {\n    while(L.size() >= 2) L.pop();\n  }\n\n  // \\/ -> \\_/\n  // f_{new}\
    \ (x) = min f(y) (x-b <= y <= x-a)\n  void shift(const T &a, const T &b) {\n \
    \   assert(a <= b);\n    add_l += a;\n    add_r += b;\n  }\n\n  // \\/. -> .\\\
    /\n  // f_{new} (x) = f(x - a)\n  void shift(const T &a) {\n    shift(a, a);\n\
    \  }\n\n  // return f(x) L, R \u3092\u7834\u58CA\u3059\u308B\n  T get(const T\
    \ &x) {\n    T ret = min_f;\n    while(L.size() >= 2) {\n      ret += max(T(0),\
    \ pop_L() - x);\n    }\n    while(R.size() >= 2) {\n      ret += max(T(0), x -\
    \ pop_R());\n    }\n    return ret;\n  }\n\n  // f(x) += g(x)\n  void merge(SlopeQueue\
    \ &g) {\n    if(g.size() > size()) {\n      swap(g.L, L);\n      swap(g.R, R);\n\
    \      swap(g.add_l, add_l);\n      swap(g.add_r, add_r);\n      swap(g.min_f,\
    \ min_f);\n    }\n    while(g.R.size() >= 2) {\n      push_R(g.pop_R());\n   \
    \ }\n    while(g.L.size() >= 2) {\n      push_L(g.pop_L());\n    }\n    min_f\
    \ += g.min_f;\n  }\n};\n"
  code: "/**\n * @brief Slope-Queue\n * @see https://maspypy.com/slope-trick-1-%E8%A7%A3%E8%AA%AC%E7%B7%A8\n\
    \ * @docs docs/slope-queue.md\n */\ntemplate< typename T >\nstruct SlopeQueue\
    \ {\n\n  const T INF = numeric_limits< T >::max() / 3;\n\n  T min_f;\n  priority_queue<\
    \ T, vector< T >, less<> > L;\n  priority_queue< T, vector< T >, greater<> > R;\n\
    \  T add_l, add_r;\n\nprivate:\n  void push_R(const T &a) {\n    R.push(a - add_r);\n\
    \  }\n\n  T top_R() const {\n    return R.top() + add_r;\n  }\n\n  T pop_R() {\n\
    \    T val = top_R();\n    R.pop();\n    return val;\n  }\n\n  void push_L(const\
    \ T &a) {\n    L.push(a - add_l);\n  }\n\n  T top_L() const {\n    return L.top()\
    \ + add_l;\n  }\n\n  T pop_L() {\n    T val = top_L();\n    L.pop();\n    return\
    \ val;\n  }\n\n  size_t size() {\n    return L.size() + R.size() - 2;\n  }\n\n\
    public:\n  SlopeQueue() : min_f(0), add_l(0), add_r(0) {\n    L.push(-INF);\n\
    \    R.push(INF);\n  }\n\n  struct Query {\n    T lx, rx, min_f;\n  };\n\n  //\
    \ return min f(x)\n  Query query() const {\n    return (Query) {top_L(), top_R(),\
    \ min_f};\n  }\n\n  // f(x) += a\n  void add_all(const T &a) {\n    min_f += a;\n\
    \  }\n\n  // add \\_\n  // f(x) += max(a - x, 0)\n  void add_a_minus_x(const T\
    \ &a) {\n    min_f += max(T(0), a - top_R());\n    push_R(a);\n    push_L(pop_R());\n\
    \  }\n\n  // add _/\n  // f(x) += max(x - a, 0)\n  void add_x_minus_a(const T\
    \ &a) {\n    min_f += max(T(0), top_L() - a);\n    push_L(a);\n    push_R(pop_L());\n\
    \  }\n\n  // add \\/\n  // f(x) += abs(x - a)\n  void add_abs(const T &a) {\n\
    \    add_a_minus_x(a);\n    add_x_minus_a(a);\n  }\n\n  // \\/ -> \\_\n  // f_{new}\
    \ (x) = min f(y) (y <= x)\n  void clear_right() {\n    while(R.size() >= 2) R.pop();\n\
    \  }\n\n  // \\/ -> _/\n  // f_{new} (x) = min f(y) (y >= x)\n  void clear_left()\
    \ {\n    while(L.size() >= 2) L.pop();\n  }\n\n  // \\/ -> \\_/\n  // f_{new}\
    \ (x) = min f(y) (x-b <= y <= x-a)\n  void shift(const T &a, const T &b) {\n \
    \   assert(a <= b);\n    add_l += a;\n    add_r += b;\n  }\n\n  // \\/. -> .\\\
    /\n  // f_{new} (x) = f(x - a)\n  void shift(const T &a) {\n    shift(a, a);\n\
    \  }\n\n  // return f(x) L, R \u3092\u7834\u58CA\u3059\u308B\n  T get(const T\
    \ &x) {\n    T ret = min_f;\n    while(L.size() >= 2) {\n      ret += max(T(0),\
    \ pop_L() - x);\n    }\n    while(R.size() >= 2) {\n      ret += max(T(0), x -\
    \ pop_R());\n    }\n    return ret;\n  }\n\n  // f(x) += g(x)\n  void merge(SlopeQueue\
    \ &g) {\n    if(g.size() > size()) {\n      swap(g.L, L);\n      swap(g.R, R);\n\
    \      swap(g.add_l, add_l);\n      swap(g.add_r, add_r);\n      swap(g.min_f,\
    \ min_f);\n    }\n    while(g.R.size() >= 2) {\n      push_R(g.pop_R());\n   \
    \ }\n    while(g.L.size() >= 2) {\n      push_L(g.pop_L());\n    }\n    min_f\
    \ += g.min_f;\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/others/slope-queue.cpp
  requiredBy: []
  timestamp: '2021-04-08 21:10:58+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/others/slope-queue.cpp
layout: document
redirect_from:
- /library/structure/others/slope-queue.cpp
- /library/structure/others/slope-queue.cpp.html
title: Slope-Queue
---
## 概要
区分線形凸関数 $f(x)$ を効率的に扱うためのデータ構造。

$f(x)$ の傾きが変化する点を優先度付きキューに持つことで, 特定の操作を簡潔に行うことが可能となる。傾きを $1$ ずつ変化させていく場合はこの実装で良いが, それ以外の場合は平衡二分探索木などの高度なデータ構造を用いる必要がある。

主にDPの高速化に用いられることが多い。


## 使い方

* `query()`: $f(x)$ の最小値とそれを満たす $x$ の最小値および最大値を返す。
* `add_all(a)`: $f(x)$ に $a$ を加算する。
* `add_a_minus_x(a)`: $f(x)$ に $\max(a - x, 0)$ を加算する。
* `add_x_minus_a(a)`: $f(x)$ に $\max(x - a, 0)$ を加算する。
* `add_abs(a)`: $f(x)$ に$abs(x-a)$ を加算する。
* `clear_right()`: $f(x) = \min_{y \le x} f(y)$ に置き換える。
* `clear_left()`: $f(x) = \min_{y \ge x} f(y)$ に置き換える。
* `shift(a, b)`: $f(x) = \min_{x-b \le y \le x-a} f(y)$ に置き換える。$a \leq b$ を満たす必要がある。
* `shift(a)`: $f(x) = f(x - a)$ に置き換える。
* `get(x)`: $f(x)$ を返す。ただし $f$ を破壊する。
* `merge(g)`: $f(x)$ に $g(x)$ を加算する. ただし $g$ を破壊する。

## 計算量

* `query()`, `add_all()`, `clear_right()`, `clear_left()`, `shift()`: $O(1)$
* `get()`: $O(Q)$
* `merge()`: $f, g$ の大きさをそれぞれ $N, M$ として $O(\min(N, M) \log \max(N, M))$
* それ以外の操作: $O(\log Q)$
