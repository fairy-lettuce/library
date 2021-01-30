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
  bundledCode: "#line 1 \"test/verify/atcoder-agc-034-c.cpp\"\n#define IGNORE\n\n\
    int main() {\n  int N, X;\n  cin >> N >> X;\n  int64 loss = 0;\n  vector< int64\
    \ > A(N), B(N), C(N);\n  vector< int > ord;\n  for(int i = 0; i < N; i++) {\n\
    \    cin >> A[i] >> B[i] >> C[i];\n    loss += B[i] * A[i];\n    ord.emplace_back(i);\n\
    \  }\n  sort(begin(ord), end(ord), [&](int a, int b) {\n    return B[a] > B[b];\n\
    \  });\n \n  auto get_cost = [&](int idx, int64 sum) {\n    int64 add = 0;\n \
    \   add += B[idx] * min(sum, A[idx]);\n    add += C[idx] * max(0LL, sum - A[idx]);\n\
    \    return add;\n  };\n  MaximumSum< int64 > tap(0);\n  for(int i = 0; i < N;\
    \ i++) {\n    tap.insert(get_cost(i, X));\n  }\n  auto check = [&](int64 sum)\
    \ {\n    int64 need = sum / X;\n    tap.set_k(need);\n    for(int i : ord) {\n\
    \      tap.erase(get_cost(i, X));\n      bool f = tap.query() + get_cost(i, sum\
    \ % X) >= loss;\n      tap.insert(get_cost(i, X));\n      if(f) return true;\n\
    \    }\n    return false;\n  };\n  int64 ok = 1LL * N * X, ng = -1;\n  while(ok\
    \ - ng > 1) {\n    auto mid = (ok + ng) / 2;\n    if(check(mid)) ok = mid;\n \
    \   else ng = mid;\n  }\n  cout << ok << endl;\n}\n\n"
  code: "#define IGNORE\n\nint main() {\n  int N, X;\n  cin >> N >> X;\n  int64 loss\
    \ = 0;\n  vector< int64 > A(N), B(N), C(N);\n  vector< int > ord;\n  for(int i\
    \ = 0; i < N; i++) {\n    cin >> A[i] >> B[i] >> C[i];\n    loss += B[i] * A[i];\n\
    \    ord.emplace_back(i);\n  }\n  sort(begin(ord), end(ord), [&](int a, int b)\
    \ {\n    return B[a] > B[b];\n  });\n \n  auto get_cost = [&](int idx, int64 sum)\
    \ {\n    int64 add = 0;\n    add += B[idx] * min(sum, A[idx]);\n    add += C[idx]\
    \ * max(0LL, sum - A[idx]);\n    return add;\n  };\n  MaximumSum< int64 > tap(0);\n\
    \  for(int i = 0; i < N; i++) {\n    tap.insert(get_cost(i, X));\n  }\n  auto\
    \ check = [&](int64 sum) {\n    int64 need = sum / X;\n    tap.set_k(need);\n\
    \    for(int i : ord) {\n      tap.erase(get_cost(i, X));\n      bool f = tap.query()\
    \ + get_cost(i, sum % X) >= loss;\n      tap.insert(get_cost(i, X));\n      if(f)\
    \ return true;\n    }\n    return false;\n  };\n  int64 ok = 1LL * N * X, ng =\
    \ -1;\n  while(ok - ng > 1) {\n    auto mid = (ok + ng) / 2;\n    if(check(mid))\
    \ ok = mid;\n    else ng = mid;\n  }\n  cout << ok << endl;\n}\n\n"
  dependsOn: []
  isVerificationFile: false
  path: test/verify/atcoder-agc-034-c.cpp
  requiredBy: []
  timestamp: '2020-01-07 02:07:19+09:00'
  verificationStatus: LIBRARY_NO_TESTS
  verifiedWith: []
documentation_of: test/verify/atcoder-agc-034-c.cpp
layout: document
redirect_from:
- /library/test/verify/atcoder-agc-034-c.cpp
- /library/test/verify/atcoder-agc-034-c.cpp.html
title: test/verify/atcoder-agc-034-c.cpp
---
