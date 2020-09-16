---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: dp/knapsack-limitations.cpp
    title: "Knapsack-Limitations(\u500B\u6570\u5236\u9650\u3064\u304D\u30CA\u30C3\u30D7\
      \u30B5\u30C3\u30AF\u554F\u984C) $O(NW)$"
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-1-i.test.cpp
    title: test/verify/aoj-dpl-1-i.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    _deprecated_at_docs: docs/knapsack-limitations-2.md
    document_title: "Knapsack-Limitations(\u500B\u6570\u5236\u9650\u3064\u304D\u30CA\
      \u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C) $O(N^2 \\max(v_i)^2)$"
    links: []
  bundledCode: "#line 1 \"dp/knapsack-limitations.cpp\"\n/**\n * @brief Knapsack-Limitations(\u500B\
    \u6570\u5236\u9650\u3064\u304D\u30CA\u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C\
    ) $O(NW)$\n * @docs docs/knapsack-limitations.md\n */\ntemplate< typename T, typename\
    \ Compare = greater< T > >\nvector< T > knapsack_limitations(const vector< int\
    \ > &w, const vector< int > &m, const vector< T > &v,\n                      \
    \           const int &W, const T &NG, const Compare &comp = Compare()) {\n  const\
    \ int N = (int) w.size();\n  vector< T > dp(W + 1, NG), deqv(W + 1);\n  dp[0]\
    \ = T();\n  vector< int > deq(W + 1);\n  for(int i = 0; i < N; i++) {\n    for(int\
    \ a = 0; a < w[i]; a++) {\n      int s = 0, t = 0;\n      for(int j = 0; w[i]\
    \ * j + a <= W; j++) {\n        if(dp[w[i] * j + a] != NG) {\n          auto val\
    \ = dp[w[i] * j + a] - j * v[i];\n          while(s < t && comp(val, deqv[t -\
    \ 1])) --t;\n          deq[t] = j;\n          deqv[t++] = val;\n        }\n  \
    \      if(s < t) {\n          dp[j * w[i] + a] = deqv[s] + j * v[i];\n       \
    \   if(deq[s] == j - m[i]) ++s;\n        }\n      }\n    }\n  }\n  return dp;\n\
    }\n#line 2 \"dp/knapsack-limitations-2.cpp\"\n\n/**\n * @brief Knapsack-Limitations(\u500B\
    \u6570\u5236\u9650\u3064\u304D\u30CA\u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C\
    ) $O(N^2 \\max(v_i)^2)$\n * @docs docs/knapsack-limitations-2.md\n */\ntemplate<\
    \ typename T >\nT knapsack_limitations(const vector< T > &w, const vector< T >\
    \ &m, const vector< int > &v,\n                       const T &W) {\n  const int\
    \ N = (int) w.size();\n  auto v_max = *max_element(begin(v), end(v));\n  if(v_max\
    \ == 0) return 0;\n  vector< int > ma(N);\n  vector< T > mb(N);\n  for(int i =\
    \ 0; i < N; i++) {\n    ma[i] = min< T >(m[i], v_max - 1);\n    mb[i] = m[i] -\
    \ ma[i];\n  }\n  T sum = 0;\n  for(int i = 0; i < N; i++) sum += ma[i] * v[i];\n\
    \  auto dp = knapsack_limitations(v, ma, w, sum, T(-1), less<>());\n  vector<\
    \ int > ord(N);\n  iota(begin(ord), end(ord), 0);\n  sort(begin(ord), end(ord),\
    \ [&](int a, int b) {\n    return v[a] * w[b] > v[b] * w[a];\n  });\n  T ret =\
    \ T();\n  for(int i = 0; i < dp.size(); i++) {\n    if(dp[i] > W || dp[i] == -1)\
    \ continue;\n    T rest = W - dp[i], cost = i;\n    for(auto &p : ord) {\n   \
    \   auto get = min(mb[p], rest / w[p]);\n      if(get == 0) break;\n      cost\
    \ += get * v[p];\n      rest -= get * w[p];\n    }\n    ret = max(ret, cost);\n\
    \  }\n  return ret;\n}\n"
  code: "#include \"knapsack-limitations.cpp\"\n\n/**\n * @brief Knapsack-Limitations(\u500B\
    \u6570\u5236\u9650\u3064\u304D\u30CA\u30C3\u30D7\u30B5\u30C3\u30AF\u554F\u984C\
    ) $O(N^2 \\max(v_i)^2)$\n * @docs docs/knapsack-limitations-2.md\n */\ntemplate<\
    \ typename T >\nT knapsack_limitations(const vector< T > &w, const vector< T >\
    \ &m, const vector< int > &v,\n                       const T &W) {\n  const int\
    \ N = (int) w.size();\n  auto v_max = *max_element(begin(v), end(v));\n  if(v_max\
    \ == 0) return 0;\n  vector< int > ma(N);\n  vector< T > mb(N);\n  for(int i =\
    \ 0; i < N; i++) {\n    ma[i] = min< T >(m[i], v_max - 1);\n    mb[i] = m[i] -\
    \ ma[i];\n  }\n  T sum = 0;\n  for(int i = 0; i < N; i++) sum += ma[i] * v[i];\n\
    \  auto dp = knapsack_limitations(v, ma, w, sum, T(-1), less<>());\n  vector<\
    \ int > ord(N);\n  iota(begin(ord), end(ord), 0);\n  sort(begin(ord), end(ord),\
    \ [&](int a, int b) {\n    return v[a] * w[b] > v[b] * w[a];\n  });\n  T ret =\
    \ T();\n  for(int i = 0; i < dp.size(); i++) {\n    if(dp[i] > W || dp[i] == -1)\
    \ continue;\n    T rest = W - dp[i], cost = i;\n    for(auto &p : ord) {\n   \
    \   auto get = min(mb[p], rest / w[p]);\n      if(get == 0) break;\n      cost\
    \ += get * v[p];\n      rest -= get * w[p];\n    }\n    ret = max(ret, cost);\n\
    \  }\n  return ret;\n}\n"
  dependsOn:
  - dp/knapsack-limitations.cpp
  isVerificationFile: false
  path: dp/knapsack-limitations-2.cpp
  requiredBy: []
  timestamp: '2020-09-15 00:43:54+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-1-i.test.cpp
documentation_of: dp/knapsack-limitations-2.cpp
layout: document
redirect_from:
- /library/dp/knapsack-limitations-2.cpp
- /library/dp/knapsack-limitations-2.cpp.html
title: "Knapsack-Limitations(\u500B\u6570\u5236\u9650\u3064\u304D\u30CA\u30C3\u30D7\
  \u30B5\u30C3\u30AF\u554F\u984C) $O(N^2 \\max(v_i)^2)$"
---
## 概要

個数制限つきナップサック問題を次に示す.

重さ $w_i$, 価値 $v_i$ であるような $N$ 種類の品物がある. $i$ 番目の品物は $m_i$ 個まで選ぶことができる. 重さの和が $W$ 以下となるように選ぶとき, 価値の最大値を求めよ.

まず「dp[価値の和]:= 重さの和の最小値」をある程度の大きさ($N \max(v_i)^2$)まで求める。残りの分は, 効率が良い順(価値/重さが大きい順)に貪欲にとってもいいことが示せて, なんかできる(c).

* `knapsack_limitations(w, m, v, W)`: 価値の最大値を求める. 

## 計算量

* $O(N^2 \max(v_i)^2)$
