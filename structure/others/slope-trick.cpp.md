---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    document_title: Slope-Trick
    links:
    - https://maspypy.com/slope-trick-1-%E8%A7%A3%E8%AA%AC%E7%B7%A8
  bundledCode: "#line 1 \"structure/others/slope-trick.cpp\"\n/**\n * @brief Slope-Trick\n\
    \ * @see https://maspypy.com/slope-trick-1-%E8%A7%A3%E8%AA%AC%E7%B7%A8\n */\n\
    template< typename T >\nstruct SlopeTrick {\n\n  const T INF = numeric_limits<\
    \ T >::max() / 3;\n\n  T min_f;\n  priority_queue< T, vector< T >, less<> > L;\n\
    \  priority_queue< T, vector< T >, greater<> > R;\n\n\n  SlopeTrick() : min_f(0)\
    \ {\n    L.push(-INF);\n    R.push(INF);\n  }\n\n  struct Query {\n    T lx, rx,\
    \ min_f;\n  };\n\n  // return min f(x)\n  Query query() const {\n    return (Query)\
    \ {L.top(), R.top(), min_f};\n  }\n\n  // f(x) += a\n  void add_all(const T &a)\
    \ {\n    min_f += a;\n  }\n\n  // add \\_\n  // f(x) += max(a - x, 0)\n  void\
    \ add_a_minus_x(const T &a) {\n    min_f += max(T(0), a - R.top());\n    R.push(a);\n\
    \    L.push(R.top());\n    R.pop();\n  }\n\n  // add _/\n  // f(x) += max(x -\
    \ a, 0)\n  void add_x_minus_a(const T &a) {\n    min_f += max(T(0), L.top() -\
    \ a);\n    L.push(a);\n    R.push(L.top());\n    L.pop();\n  }\n\n  // add \\\
    /\n  // f(x) += abs(x - a)\n  void add_abs(const T &a) {\n    add_a_minus_x(a);\n\
    \    add_x_minus_a(a);\n  }\n\n  // \\/ -> \\_\n  // f_{new} (x) = min f(y) (y\
    \ <= x)\n  void clear_right() {\n    while(R.size() >= 2) R.pop();\n  }\n\n  //\
    \ \\/ -> _/\n  // f_{new} (x) = min f(y) (y >= x)\n  void clear_left() {\n   \
    \ while(L.size() >= 2) L.pop();\n  }\n};\n"
  code: "/**\n * @brief Slope-Trick\n * @see https://maspypy.com/slope-trick-1-%E8%A7%A3%E8%AA%AC%E7%B7%A8\n\
    \ */\ntemplate< typename T >\nstruct SlopeTrick {\n\n  const T INF = numeric_limits<\
    \ T >::max() / 3;\n\n  T min_f;\n  priority_queue< T, vector< T >, less<> > L;\n\
    \  priority_queue< T, vector< T >, greater<> > R;\n\n\n  SlopeTrick() : min_f(0)\
    \ {\n    L.push(-INF);\n    R.push(INF);\n  }\n\n  struct Query {\n    T lx, rx,\
    \ min_f;\n  };\n\n  // return min f(x)\n  Query query() const {\n    return (Query)\
    \ {L.top(), R.top(), min_f};\n  }\n\n  // f(x) += a\n  void add_all(const T &a)\
    \ {\n    min_f += a;\n  }\n\n  // add \\_\n  // f(x) += max(a - x, 0)\n  void\
    \ add_a_minus_x(const T &a) {\n    min_f += max(T(0), a - R.top());\n    R.push(a);\n\
    \    L.push(R.top());\n    R.pop();\n  }\n\n  // add _/\n  // f(x) += max(x -\
    \ a, 0)\n  void add_x_minus_a(const T &a) {\n    min_f += max(T(0), L.top() -\
    \ a);\n    L.push(a);\n    R.push(L.top());\n    L.pop();\n  }\n\n  // add \\\
    /\n  // f(x) += abs(x - a)\n  void add_abs(const T &a) {\n    add_a_minus_x(a);\n\
    \    add_x_minus_a(a);\n  }\n\n  // \\/ -> \\_\n  // f_{new} (x) = min f(y) (y\
    \ <= x)\n  void clear_right() {\n    while(R.size() >= 2) R.pop();\n  }\n\n  //\
    \ \\/ -> _/\n  // f_{new} (x) = min f(y) (y >= x)\n  void clear_left() {\n   \
    \ while(L.size() >= 2) L.pop();\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/others/slope-trick.cpp
  requiredBy: []
  timestamp: '2021-04-05 00:26:16+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/others/slope-trick.cpp
layout: document
redirect_from:
- /library/structure/others/slope-trick.cpp
- /library/structure/others/slope-trick.cpp.html
title: Slope-Trick
---
