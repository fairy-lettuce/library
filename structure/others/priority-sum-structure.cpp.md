---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    links: []
  bundledCode: "#line 1 \"structure/others/priority-sum-structure.cpp\"\ntemplate<\
    \ typename T, typename Compare = less< T >, typename RCompare = greater< T > >\n\
    struct PrioritySumStructure {\n\n  size_t k;\n  T sum;\n\n  priority_queue< T,\
    \ vector< T >, Compare > in, d_in;\n  priority_queue< T, vector< T >, RCompare\
    \ > out, d_out;\n\n  PrioritySumStructure(int k) : k(k), sum(0) {}\n\n  void modify()\
    \ {\n    while(in.size() - d_in.size() < k && !out.empty()) {\n      auto p =\
    \ out.top();\n      out.pop();\n      if(!d_out.empty() && p == d_out.top()) {\n\
    \        d_out.pop();\n      } else {\n        sum += p;\n        in.emplace(p);\n\
    \      }\n    }\n    while(in.size() - d_in.size() > k) {\n      auto p = in.top();\n\
    \      in.pop();\n      if(!d_in.empty() && p == d_in.top()) {\n        d_in.pop();\n\
    \      } else {\n        sum -= p;\n        out.emplace(p);\n      }\n    }\n\
    \    while(!d_in.empty() && in.top() == d_in.top()) {\n      in.pop();\n     \
    \ d_in.pop();\n    }\n  }\n\n  T query() const {\n    return sum;\n  }\n\n  void\
    \ insert(T x) {\n    in.emplace(x);\n    sum += x;\n    modify();\n  }\n\n  void\
    \ erase(T x) {\n    assert(size());\n    if(!in.empty() && in.top() == x) {\n\
    \      sum -= x;\n      in.pop();\n    } else if(!in.empty() && RCompare()(in.top(),\
    \ x)) {\n      sum -= x;\n      d_in.emplace(x);\n    } else {\n      d_out.emplace(x);\n\
    \    }\n    modify();\n  }\n\n  void set_k(size_t kk) {\n    k = kk;\n    modify();\n\
    \  }\n\n  size_t get_k() const {\n    return k;\n  }\n\n  size_t size() const\
    \ {\n    return in.size() + out.size() - d_in.size() - d_out.size();\n  }\n};\n\
    \ntemplate< typename T >\nusing MaximumSum = PrioritySumStructure< T, greater<\
    \ T >, less< T > >;\n\ntemplate< typename T >\nusing MinimumSum = PrioritySumStructure<\
    \ T, less< T >, greater< T > >;\n\n"
  code: "template< typename T, typename Compare = less< T >, typename RCompare = greater<\
    \ T > >\nstruct PrioritySumStructure {\n\n  size_t k;\n  T sum;\n\n  priority_queue<\
    \ T, vector< T >, Compare > in, d_in;\n  priority_queue< T, vector< T >, RCompare\
    \ > out, d_out;\n\n  PrioritySumStructure(int k) : k(k), sum(0) {}\n\n  void modify()\
    \ {\n    while(in.size() - d_in.size() < k && !out.empty()) {\n      auto p =\
    \ out.top();\n      out.pop();\n      if(!d_out.empty() && p == d_out.top()) {\n\
    \        d_out.pop();\n      } else {\n        sum += p;\n        in.emplace(p);\n\
    \      }\n    }\n    while(in.size() - d_in.size() > k) {\n      auto p = in.top();\n\
    \      in.pop();\n      if(!d_in.empty() && p == d_in.top()) {\n        d_in.pop();\n\
    \      } else {\n        sum -= p;\n        out.emplace(p);\n      }\n    }\n\
    \    while(!d_in.empty() && in.top() == d_in.top()) {\n      in.pop();\n     \
    \ d_in.pop();\n    }\n  }\n\n  T query() const {\n    return sum;\n  }\n\n  void\
    \ insert(T x) {\n    in.emplace(x);\n    sum += x;\n    modify();\n  }\n\n  void\
    \ erase(T x) {\n    assert(size());\n    if(!in.empty() && in.top() == x) {\n\
    \      sum -= x;\n      in.pop();\n    } else if(!in.empty() && RCompare()(in.top(),\
    \ x)) {\n      sum -= x;\n      d_in.emplace(x);\n    } else {\n      d_out.emplace(x);\n\
    \    }\n    modify();\n  }\n\n  void set_k(size_t kk) {\n    k = kk;\n    modify();\n\
    \  }\n\n  size_t get_k() const {\n    return k;\n  }\n\n  size_t size() const\
    \ {\n    return in.size() + out.size() - d_in.size() - d_out.size();\n  }\n};\n\
    \ntemplate< typename T >\nusing MaximumSum = PrioritySumStructure< T, greater<\
    \ T >, less< T > >;\n\ntemplate< typename T >\nusing MinimumSum = PrioritySumStructure<\
    \ T, less< T >, greater< T > >;\n\n"
  dependsOn: []
  isVerificationFile: false
  path: structure/others/priority-sum-structure.cpp
  requiredBy: []
  timestamp: '2019-11-30 22:41:48+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: structure/others/priority-sum-structure.cpp
layout: document
redirect_from:
- /library/structure/others/priority-sum-structure.cpp
- /library/structure/others/priority-sum-structure.cpp.html
title: structure/others/priority-sum-structure.cpp
---
