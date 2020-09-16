---
data:
  _extendedDependsOn: []
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _pathExtension: cpp
  _verificationStatusIcon: ':warning:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    IGNORE: ''
    IGNORE_IF_CLANG: ''
    IGNORE_IF_GCC: ''
    links: []
  bundledCode: "#line 1 \"test/verify/atcoder-tkppc-2015-j.cpp\"\n#define IGNORE\n\
    \ntemplate< typename T, typename Compare = less< T > >\nstruct PQ {\n  priority_queue<\
    \ T, vector< T >, Compare > que1, que2;\n \n  PQ() = default;\n \n  void push(T\
    \ k) {\n    que1.emplace(k);\n  }\n \n  void pop(T k) {\n    que2.emplace(k);\n\
    \  }\n \n  inline void modify() {\n    while(que2.size() && que2.top() == que1.top())\
    \ {\n      que2.pop();\n      que1.pop();\n    }\n  }\n \n  bool empty() {\n \
    \   modify();\n    return que1.empty();\n  }\n \n  T top() {\n    modify();\n\
    \    return que1.top();\n  }\n};\n \nint main() {\n \n  struct Farthest {\n  \
    \  PQ< int64 > pq;\n    int64 c_max, p_max, length;\n \n    Farthest() : c_max(-infll),\
    \ p_max(-infll), length(0) {}\n \n    void merge(int64 key, const Farthest &parent,\
    \ const Farthest &child) {\n      p_max = max(child.p_max, child.length + key\
    \ + max(pq.empty() ? 0 : pq.top(), parent.p_max));\n      c_max = max(parent.c_max,\
    \ parent.length + key + max(pq.empty() ? 0 : pq.top(), child.c_max));\n      length\
    \ = parent.length + key + child.length;\n    }\n \n    void toggle() {\n     \
    \ swap(c_max, p_max);\n    }\n \n    void add(const Farthest &child) {\n     \
    \ pq.push(child.c_max);\n    }\n \n    void erase(const Farthest &child) {\n \
    \     pq.pop(child.c_max);\n    }\n  } e;\n \n  int Q;\n  cin >> Q;\n \n  using\
    \ LCT = LinkCutTreeSubtree< Farthest, int64 >;\n  LCT lct(e);\n  vector< LCT::Node\
    \ * > ev(500001), ee(500001);\n  ev[0] = lct.make_node(0);\n \n  int num = 1;\n\
    \  for(int i = 0; i < Q; i++) {\n    int t, a, b;\n    cin >> t >> a >> b;\n \
    \   if(t == 1) {\n      ev[num] = lct.make_node(0);\n      ee[num] = lct.make_node(b);\n\
    \      lct.link(ee[num], ev[a]);\n      lct.link(ev[num], ee[num]);\n      ++num;\n\
    \    } else if(t == 2) {\n      lct.set_key(ee[a], b);\n    } else {\n      lct.evert(ev[a]);\n\
    \      cout << ev[a]->sum.c_max << \"\\n\";\n    }\n  }\n}\n"
  code: "#define IGNORE\n\ntemplate< typename T, typename Compare = less< T > >\n\
    struct PQ {\n  priority_queue< T, vector< T >, Compare > que1, que2;\n \n  PQ()\
    \ = default;\n \n  void push(T k) {\n    que1.emplace(k);\n  }\n \n  void pop(T\
    \ k) {\n    que2.emplace(k);\n  }\n \n  inline void modify() {\n    while(que2.size()\
    \ && que2.top() == que1.top()) {\n      que2.pop();\n      que1.pop();\n    }\n\
    \  }\n \n  bool empty() {\n    modify();\n    return que1.empty();\n  }\n \n \
    \ T top() {\n    modify();\n    return que1.top();\n  }\n};\n \nint main() {\n\
    \ \n  struct Farthest {\n    PQ< int64 > pq;\n    int64 c_max, p_max, length;\n\
    \ \n    Farthest() : c_max(-infll), p_max(-infll), length(0) {}\n \n    void merge(int64\
    \ key, const Farthest &parent, const Farthest &child) {\n      p_max = max(child.p_max,\
    \ child.length + key + max(pq.empty() ? 0 : pq.top(), parent.p_max));\n      c_max\
    \ = max(parent.c_max, parent.length + key + max(pq.empty() ? 0 : pq.top(), child.c_max));\n\
    \      length = parent.length + key + child.length;\n    }\n \n    void toggle()\
    \ {\n      swap(c_max, p_max);\n    }\n \n    void add(const Farthest &child)\
    \ {\n      pq.push(child.c_max);\n    }\n \n    void erase(const Farthest &child)\
    \ {\n      pq.pop(child.c_max);\n    }\n  } e;\n \n  int Q;\n  cin >> Q;\n \n\
    \  using LCT = LinkCutTreeSubtree< Farthest, int64 >;\n  LCT lct(e);\n  vector<\
    \ LCT::Node * > ev(500001), ee(500001);\n  ev[0] = lct.make_node(0);\n \n  int\
    \ num = 1;\n  for(int i = 0; i < Q; i++) {\n    int t, a, b;\n    cin >> t >>\
    \ a >> b;\n    if(t == 1) {\n      ev[num] = lct.make_node(0);\n      ee[num]\
    \ = lct.make_node(b);\n      lct.link(ee[num], ev[a]);\n      lct.link(ev[num],\
    \ ee[num]);\n      ++num;\n    } else if(t == 2) {\n      lct.set_key(ee[a], b);\n\
    \    } else {\n      lct.evert(ev[a]);\n      cout << ev[a]->sum.c_max << \"\\\
    n\";\n    }\n  }\n}\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-tkppc-2015-j.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-tkppc-2015-j.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-tkppc-2015-j.cpp
- /library/test/verify/atcoder-tkppc-2015-j.cpp.html
title: test/verify/atcoder-tkppc-2015-j.cpp
---
