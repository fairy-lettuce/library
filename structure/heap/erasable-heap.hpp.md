---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: hpp
  _verificationStatusIcon: ':warning:'
  attributes:
    links: []
  bundledCode: "#line 2 \"structure/heap/erasable-heap.hpp\"\n\n#include <cassert>\n\
    #include <queue>\n\ntemplate < typename T, class Container = std::vector< T >,\
    \ class Compare = std::less< typename Container::value_type > > \nclass erasable_heap\
    \ {\n  std::priority_queue< T, Container, Compare > base, erased;\n\n  void normalize()\
    \ {\n    while (true) {\n      if (base.empty()) break;\n      if (erased.empty())\
    \ break;\n      if (base.top() != erased.top()) break;\n      base.pop();\n  \
    \    erased.pop();\n    }\n  }\n\n  public:\n  bool empty() const { return base.empty();\
    \ }\n\n  const T &top() const {\n    assert( !empty() );\n    return base.top();\n\
    \  }\n\n  void push(T val) {\n    base.push(std::move(val));\n    normalize();\n\
    \  }\n\n  template < class... Args >\n    void emplace(Args... args) {\n     \
    \ base.emplace(args...);\n      normalize();\n    }\n\n  void pop() {\n    assert(\
    \ !empty() );\n    base.pop();\n    normalize();\n  }\n\n  void erase(T val) {\n\
    \    erased.push(std::move(val));\n    normalize();\n  }\n};\n"
  code: "#pragma once\n\n#include <cassert>\n#include <queue>\n\ntemplate < typename\
    \ T, class Container = std::vector< T >, class Compare = std::less< typename Container::value_type\
    \ > > \nclass erasable_heap {\n  std::priority_queue< T, Container, Compare >\
    \ base, erased;\n\n  void normalize() {\n    while (true) {\n      if (base.empty())\
    \ break;\n      if (erased.empty()) break;\n      if (base.top() != erased.top())\
    \ break;\n      base.pop();\n      erased.pop();\n    }\n  }\n\n  public:\n  bool\
    \ empty() const { return base.empty(); }\n\n  const T &top() const {\n    assert(\
    \ !empty() );\n    return base.top();\n  }\n\n  void push(T val) {\n    base.push(std::move(val));\n\
    \    normalize();\n  }\n\n  template < class... Args >\n    void emplace(Args...\
    \ args) {\n      base.emplace(args...);\n      normalize();\n    }\n\n  void pop()\
    \ {\n    assert( !empty() );\n    base.pop();\n    normalize();\n  }\n\n  void\
    \ erase(T val) {\n    erased.push(std::move(val));\n    normalize();\n  }\n};\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/heap/erasable-heap.hpp
  requiredBy: []
  timestamp: '2021-06-30 02:39:57+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/heap/erasable-heap.hpp
layout: document
redirect_from:
- /library/structure/heap/erasable-heap.hpp
- /library/structure/heap/erasable-heap.hpp.html
title: structure/heap/erasable-heap.hpp
---
