---
data:
  _extendedDependsOn: []
  _extendedRequiredBy:
  - icon: ':heavy_check_mark:'
    path: dp/knapsack-limitations-2.cpp
    title: "Knapsack Limitations(\u500B\u6570\u5236\u9650\u3064\u304D\u30CA\u30C3\u30D7\
      \u30B5\u30C3\u30AF\u554F\u984C) $O(N^2 \\max(v_i)^2)$"
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-1-g.test.cpp
    title: test/verify/aoj-dpl-1-g.test.cpp
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-1-i.test.cpp
    title: test/verify/aoj-dpl-1-i.test.cpp
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/knapsack-limitations.md
    document_title: "Knapsack Limitations(\u500B\u6570\u5236\u9650\u3064\u304D\u30CA\
      \u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C) $O(NW)$"
    links: []
  bundledCode: "#line 1 \"dp/knapsack-limitations.cpp\"\n/**\n * @brief Knapsack Limitations(\u500B\
    \u6570\u5236\u9650\u3064\u304D\u30CA\u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C\
    ) $O(NW)$\n * @docs docs/knapsack-limitations.md\n */\ntemplate< typename T, typename\
    \ Compare = greater< T > >\nvector< T > knapsack_limitations(const vector< int\
    \ > &w, const vector< int > &m, const vector< T > &v,\n                      \
    \           const int &W, const T &NG, const Compare &comp = Compare()) {\n  const\
    \ int N = (int) w.size();\n  vector< T > dp(W + 1, NG), deqv(W + 1);\n  dp[0]\
    \ = T();\n  vector< int > deq(W + 1);\n  for(int i = 0; i < N; i++) {\n    if(w[i]\
    \ == 0) {\n      for(int j = 0; j <= W; j++) {\n        if(dp[j] != NG && comp(dp[j]\
    \ + v[i] * m[i], dp[j])) {\n          dp[j] = dp[j] + v[i] * m[i];\n        }\n\
    \      }\n    } else {\n      for(int a = 0; a < w[i]; a++) {\n        int s =\
    \ 0, t = 0;\n        for(int j = 0; w[i] * j + a <= W; j++) {\n          if(dp[w[i]\
    \ * j + a] != NG) {\n            auto val = dp[w[i] * j + a] - j * v[i];\n   \
    \         while(s < t && comp(val, deqv[t - 1])) --t;\n            deq[t] = j;\n\
    \            deqv[t++] = val;\n          }\n          if(s < t) {\n          \
    \  dp[j * w[i] + a] = deqv[s] + j * v[i];\n            if(deq[s] == j - m[i])\
    \ ++s;\n          }\n        }\n      }\n    }\n  }\n  return dp;\n}\n"
  code: "/**\n * @brief Knapsack Limitations(\u500B\u6570\u5236\u9650\u3064\u304D\u30CA\
    \u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C) $O(NW)$\n * @docs docs/knapsack-limitations.md\n\
    \ */\ntemplate< typename T, typename Compare = greater< T > >\nvector< T > knapsack_limitations(const\
    \ vector< int > &w, const vector< int > &m, const vector< T > &v,\n          \
    \                       const int &W, const T &NG, const Compare &comp = Compare())\
    \ {\n  const int N = (int) w.size();\n  vector< T > dp(W + 1, NG), deqv(W + 1);\n\
    \  dp[0] = T();\n  vector< int > deq(W + 1);\n  for(int i = 0; i < N; i++) {\n\
    \    if(w[i] == 0) {\n      for(int j = 0; j <= W; j++) {\n        if(dp[j] !=\
    \ NG && comp(dp[j] + v[i] * m[i], dp[j])) {\n          dp[j] = dp[j] + v[i] *\
    \ m[i];\n        }\n      }\n    } else {\n      for(int a = 0; a < w[i]; a++)\
    \ {\n        int s = 0, t = 0;\n        for(int j = 0; w[i] * j + a <= W; j++)\
    \ {\n          if(dp[w[i] * j + a] != NG) {\n            auto val = dp[w[i] *\
    \ j + a] - j * v[i];\n            while(s < t && comp(val, deqv[t - 1])) --t;\n\
    \            deq[t] = j;\n            deqv[t++] = val;\n          }\n        \
    \  if(s < t) {\n            dp[j * w[i] + a] = deqv[s] + j * v[i];\n         \
    \   if(deq[s] == j - m[i]) ++s;\n          }\n        }\n      }\n    }\n  }\n\
    \  return dp;\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: dp/knapsack-limitations.cpp
  requiredBy:
  - dp/knapsack-limitations-2.cpp
  timestamp: '2021-08-25 15:39:13+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-1-g.test.cpp
  - test/verify/aoj-dpl-1-i.test.cpp
documentation_of: dp/knapsack-limitations.cpp
layout: document
redirect_from:
- /library/dp/knapsack-limitations.cpp
- /library/dp/knapsack-limitations.cpp.html
title: "Knapsack Limitations(\u500B\u6570\u5236\u9650\u3064\u304D\u30CA\u30C3\u30D7\
  \u30B5\u30C3\u30AF\u554F\u984C) $O(NW)$"
---
## 概要

個数制限つきナップサック問題を次に示す.

重さ $w_i$, 価値 $v_i$ であるような $N$ 種類の品物がある. $i$ 番目の品物は $m_i$ 個まで選ぶことができる. 重さの和が $W$ 以下となるように選ぶとき, 価値の最大値を求めよ.

スライド最大値を用いた動的計画法により効率的に計算可能.

* `knapsack_limitations(w, m, v, W, NG, comp)`: `W` 以下の範囲で, 各重さについて価値の最大値を求める. `NG` は到達ができない場合の値で, `comp` は比較演算子.

## 計算量

* $O(NW)$
