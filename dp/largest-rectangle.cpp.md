---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith:
  - icon: ':heavy_check_mark:'
    path: test/verify/aoj-dpl-3-c.test.cpp
    title: test/verify/aoj-dpl-3-c.test.cpp
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    _deprecated_at_docs: docs/largest-rectangle.md
    document_title: "Largest-Rectangle(\u6700\u5927\u9577\u65B9\u5F62)"
    links: []
  bundledCode: "#line 1 \"dp/largest-rectangle.cpp\"\n/**\n * @brief Largest-Rectangle(\u6700\
    \u5927\u9577\u65B9\u5F62)\n * @docs docs/largest-rectangle.md\n */\t\ntemplate<\
    \ typename T >\nint64_t largest_rectangle(vector< T > height)\n{\n  stack< int\
    \ > st;\n  height.push_back(0);\n  vector< int > left(height.size());\n  int64_t\
    \ ret = 0;\n  for(int i = 0; i < height.size(); i++) {\n    while(!st.empty()\
    \ && height[st.top()] >= height[i]) {\n      ret = max(ret, (int64_t) (i - left[st.top()]\
    \ - 1) * height[st.top()]);\n      st.pop();\n    }\n    left[i] = st.empty()\
    \ ? -1 : st.top();\n    st.emplace(i);\n  }\n  return (ret);\n}\n"
  code: "/**\n * @brief Largest-Rectangle(\u6700\u5927\u9577\u65B9\u5F62)\n * @docs\
    \ docs/largest-rectangle.md\n */\t\ntemplate< typename T >\nint64_t largest_rectangle(vector<\
    \ T > height)\n{\n  stack< int > st;\n  height.push_back(0);\n  vector< int >\
    \ left(height.size());\n  int64_t ret = 0;\n  for(int i = 0; i < height.size();\
    \ i++) {\n    while(!st.empty() && height[st.top()] >= height[i]) {\n      ret\
    \ = max(ret, (int64_t) (i - left[st.top()] - 1) * height[st.top()]);\n      st.pop();\n\
    \    }\n    left[i] = st.empty() ? -1 : st.top();\n    st.emplace(i);\n  }\n \
    \ return (ret);\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: dp/largest-rectangle.cpp
  requiredBy: []
  timestamp: '2020-08-04 00:02:11+09:00'
  verificationStatus: LIBRARY_ALL_AC
  verifiedWith:
  - test/verify/aoj-dpl-3-c.test.cpp
documentation_of: dp/largest-rectangle.cpp
layout: document
redirect_from:
- /library/dp/largest-rectangle.cpp
- /library/dp/largest-rectangle.cpp.html
title: "Largest-Rectangle(\u6700\u5927\u9577\u65B9\u5F62)"
---
## 概要

ヒストグラム中の最大長方形の面積を求める.

ヒストグラムを左から見る. スタックに自分より左にあるヒストグラムの高さと位置を単調増加になるように管理すると効率的に解ける.

* `largest_rectangle(height)`: ヒストグラムが `height` のとき最大長方形の面積を返す.

## 計算量

* $O(N)$
