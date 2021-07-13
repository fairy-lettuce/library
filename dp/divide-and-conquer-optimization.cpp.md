---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: dp/monotone-minima.cpp
    title: Monotone Minima
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-2603.test.cpp
    title: test/verify/aoj-2603.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/divide-and-conquer-optimization.md
    document_title: Divide And Conquer Optimization
    links: []
  bundledCode: "#line 1 \"dp/monotone-minima.cpp\"\n/**\n * @brief Monotone Minima\n\
    \ * @docs docs/monotone-minima.md\n */\ntemplate< typename T, typename Compare\
    \ = less< T > >\nvector< pair< int, T > > monotone_minima(int H, int W, const\
    \ function< T(int, int) > &f, const Compare &comp = Compare()) {\n  vector< pair<\
    \ int, T > > dp(H);\n  function< void(int, int, int, int) > dfs = [&](int top,\
    \ int bottom, int left, int right) {\n    if(top > bottom) return;\n    int line\
    \ = (top + bottom) / 2;\n    T ma;\n    int mi = -1;\n    for(int i = left; i\
    \ <= right; i++) {\n      T cst = f(line, i);\n      if(mi == -1 || comp(cst,\
    \ ma)) {\n        ma = cst;\n        mi = i;\n      }\n    }\n    dp[line] = make_pair(mi,\
    \ ma);\n    dfs(top, line - 1, left, mi);\n    dfs(line + 1, bottom, mi, right);\n\
    \  };\n  dfs(0, H - 1, 0, W - 1);\n  return dp;\n}\n#line 2 \"dp/divide-and-conquer-optimization.cpp\"\
    \n\n/**\n * @brief Divide And Conquer Optimization\n * @docs docs/divide-and-conquer-optimization.md\n\
    \ */\ntemplate< typename T, typename Compare = less< T > >\nvector< vector< T\
    \ > > divide_and_conquer_optimization(int H, int W, T INF, const function< T(int,\
    \ int) > &f, const Compare &comp = Compare()) {\n  vector< vector< T > > dp(H\
    \ + 1, vector< T >(W + 1, INF));\n  dp[0][0] = 0;\n  for(int i = 1; i <= H; i++)\
    \ {\n    function< T(int, int) > get_cost = [&](int y, int x) {\n      if(x >=\
    \ y) return INF;\n      return dp[i - 1][x] + f(x, y);\n    };\n    auto ret =\
    \ monotone_minima(W + 1, W + 1, get_cost, comp);\n    for(int j = 0; j <= W; j++)\
    \ dp[i][j] = ret[j].second;\n  }\n  return dp;\n}\n"
  code: "#include \"monotone-minima.cpp\"\n\n/**\n * @brief Divide And Conquer Optimization\n\
    \ * @docs docs/divide-and-conquer-optimization.md\n */\ntemplate< typename T,\
    \ typename Compare = less< T > >\nvector< vector< T > > divide_and_conquer_optimization(int\
    \ H, int W, T INF, const function< T(int, int) > &f, const Compare &comp = Compare())\
    \ {\n  vector< vector< T > > dp(H + 1, vector< T >(W + 1, INF));\n  dp[0][0] =\
    \ 0;\n  for(int i = 1; i <= H; i++) {\n    function< T(int, int) > get_cost =\
    \ [&](int y, int x) {\n      if(x >= y) return INF;\n      return dp[i - 1][x]\
    \ + f(x, y);\n    };\n    auto ret = monotone_minima(W + 1, W + 1, get_cost, comp);\n\
    \    for(int j = 0; j <= W; j++) dp[i][j] = ret[j].second;\n  }\n  return dp;\n\
    }\n"
  dependsOn:
  - dp/monotone-minima.cpp
  isVerificationFile: false
  path: dp/divide-and-conquer-optimization.cpp
  requiredBy: []
  timestamp: '2021-07-13 19:53:12+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-2603.test.cpp
documentation_of: dp/divide-and-conquer-optimization.cpp
layout: document
redirect_from:
- /library/dp/divide-and-conquer-optimization.cpp
- /library/dp/divide-and-conquer-optimization.cpp.html
title: Divide And Conquer Optimization
---
## 概要

$dp[i][j] = \min_{0 \leq k \lt j}\\{dp[i-1][k]+f(k,j)\\}$ の形のDPを高速化するテク.

$f(k,j)$ は $0 \leq k \lt j \leq W$ で定義される $2$ 変数関数.

各行について Monotone-Minima を適用する.


* `divide_and_conquer_optimization(H, W, INF, f)`: dp 配列を返す.

## 計算量

* $O(HW \log W)$
