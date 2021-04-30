---
data:
  _extendedDependsOn:
  - icon: ':heavy_check_mark:'
    path: string/suffix-array.cpp
    title: string/suffix-array.cpp
  - icon: ':question:'
    path: template/template.cpp
    title: template/template.cpp
  _extendedRequiredBy: []
  _extendedVerifiedWith: []
  _isVerificationFailed: false
  _pathExtension: cpp
  _verificationStatusIcon: ':heavy_check_mark:'
  attributes:
    '*NOT_SPECIAL_COMMENTS*': ''
    PROBLEM: http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_14_D
    links:
    - http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_14_D
  bundledCode: "#line 1 \"test/verify/aoj-alds-1-14-d.test.cpp\"\n#define PROBLEM\
    \ \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_14_D\"\n\n\
    #line 1 \"template/template.cpp\"\n#include<bits/stdc++.h>\n\nusing namespace\
    \ std;\n\nusing int64 = long long;\nconst int mod = 1e9 + 7;\n\nconst int64 infll\
    \ = (1LL << 62) - 1;\nconst int inf = (1 << 30) - 1;\n\nstruct IoSetup {\n  IoSetup()\
    \ {\n    cin.tie(nullptr);\n    ios::sync_with_stdio(false);\n    cout << fixed\
    \ << setprecision(10);\n    cerr << fixed << setprecision(10);\n  }\n} iosetup;\n\
    \ntemplate< typename T1, typename T2 >\nostream &operator<<(ostream &os, const\
    \ pair< T1, T2 >& p) {\n  os << p.first << \" \" << p.second;\n  return os;\n\
    }\n\ntemplate< typename T1, typename T2 >\nistream &operator>>(istream &is, pair<\
    \ T1, T2 > &p) {\n  is >> p.first >> p.second;\n  return is;\n}\n\ntemplate< typename\
    \ T >\nostream &operator<<(ostream &os, const vector< T > &v) {\n  for(int i =\
    \ 0; i < (int) v.size(); i++) {\n    os << v[i] << (i + 1 != v.size() ? \" \"\
    \ : \"\");\n  }\n  return os;\n}\n\ntemplate< typename T >\nistream &operator>>(istream\
    \ &is, vector< T > &v) {\n  for(T &in : v) is >> in;\n  return is;\n}\n\ntemplate<\
    \ typename T1, typename T2 >\ninline bool chmax(T1 &a, T2 b) { return a < b &&\
    \ (a = b, true); }\n\ntemplate< typename T1, typename T2 >\ninline bool chmin(T1\
    \ &a, T2 b) { return a > b && (a = b, true); }\n\ntemplate< typename T = int64\
    \ >\nvector< T > make_v(size_t a) {\n  return vector< T >(a);\n}\n\ntemplate<\
    \ typename T, typename... Ts >\nauto make_v(size_t a, Ts... ts) {\n  return vector<\
    \ decltype(make_v< T >(ts...)) >(a, make_v< T >(ts...));\n}\n\ntemplate< typename\
    \ T, typename V >\ntypename enable_if< is_class< T >::value == 0 >::type fill_v(T\
    \ &t, const V &v) {\n  t = v;\n}\n\ntemplate< typename T, typename V >\ntypename\
    \ enable_if< is_class< T >::value != 0 >::type fill_v(T &t, const V &v) {\n  for(auto\
    \ &e : t) fill_v(e, v);\n}\n\ntemplate< typename F >\nstruct FixPoint : F {\n\
    \  explicit FixPoint(F &&f) : F(forward< F >(f)) {}\n\n  template< typename...\
    \ Args >\n  decltype(auto) operator()(Args &&... args) const {\n    return F::operator()(*this,\
    \ forward< Args >(args)...);\n  }\n};\n \ntemplate< typename F >\ninline decltype(auto)\
    \ MFP(F &&f) {\n  return FixPoint< F >{forward< F >(f)};\n}\n#line 4 \"test/verify/aoj-alds-1-14-d.test.cpp\"\
    \n\n#line 1 \"string/suffix-array.cpp\"\nstruct SuffixArray {\n  vector< int >\
    \ SA;\n  const string s;\n\n  SuffixArray(const string &str) : s(str) {\n    SA.resize(s.size());\n\
    \    iota(begin(SA), end(SA), 0);\n    sort(begin(SA), end(SA), [&](int a, int\
    \ b) {\n      return s[a] == s[b] ? a > b : s[a] < s[b];\n    });\n    vector<\
    \ int > classes(s.size()), c(s.begin(), s.end()), cnt(s.size());\n    for(int\
    \ len = 1; len < s.size(); len <<= 1) {\n      for(int i = 0; i < s.size(); i++)\
    \ {\n        if(i > 0 && c[SA[i - 1]] == c[SA[i]] && SA[i - 1] + len < s.size()\
    \ && c[SA[i - 1] + len / 2] == c[SA[i] + len / 2]) {\n          classes[SA[i]]\
    \ = classes[SA[i - 1]];\n        } else {\n          classes[SA[i]] = i;\n   \
    \     }\n      }\n      iota(begin(cnt), end(cnt), 0);\n      copy(begin(SA),\
    \ end(SA), begin(c));\n      for(int i = 0; i < s.size(); i++) {\n        int\
    \ s1 = c[i] - len;\n        if(s1 >= 0) SA[cnt[classes[s1]]++] = s1;\n      }\n\
    \      classes.swap(c);\n    }\n  }\n\n  int operator[](int k) const {\n    return\
    \ SA[k];\n  }\n\n  size_t size() const {\n    return s.size();\n  }\n\n  bool\
    \ lt_substr(const string &t, int si = 0, int ti = 0) {\n    int sn = (int) s.size(),\
    \ tn = (int) t.size();\n    while(si < sn && ti < tn) {\n      if(s[si] < t[ti])\
    \ return true;\n      if(s[si] > t[ti]) return false;\n      ++si, ++ti;\n   \
    \ }\n    return si >= sn && ti < tn;\n  }\n\n  int lower_bound(const string &t)\
    \ {\n    int low = -1, high = (int) SA.size();\n    while(high - low > 1) {\n\
    \      int mid = (low + high) / 2;\n      if(lt_substr(t, SA[mid])) low = mid;\n\
    \      else high = mid;\n    }\n    return high;\n  }\n\n  pair< int, int > lower_upper_bound(string\
    \ &t) {\n    int idx = lower_bound(t);\n    int low = idx - 1, high = (int) SA.size();\n\
    \    t.back()++;\n    while(high - low > 1) {\n      int mid = (low + high) /\
    \ 2;\n      if(lt_substr(t, SA[mid])) low = mid;\n      else high = mid;\n   \
    \ }\n    t.back()--;\n    return {idx, high};\n  }\n\n  void output() {\n    for(int\
    \ i = 0; i < size(); i++) {\n      cout << i << \": \" << s.substr(SA[i]) << endl;\n\
    \    }\n  }\n};\n#line 6 \"test/verify/aoj-alds-1-14-d.test.cpp\"\n\nint main()\
    \ {\n  string S;\n  int Q;\n\n  cin >> S;\n  SuffixArray sa(S);\n  cin >> Q;\n\
    \  while(Q--) {\n    string T;\n    cin >> T;\n    auto range = sa.lower_upper_bound(T);\n\
    \    cout << (range.first != range.second) << endl;\n  }\n}\n"
  code: "#define PROBLEM \"http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=ALDS1_14_D\"\
    \n\n#include \"../../template/template.cpp\"\n\n#include \"../../string/suffix-array.cpp\"\
    \n\nint main() {\n  string S;\n  int Q;\n\n  cin >> S;\n  SuffixArray sa(S);\n\
    \  cin >> Q;\n  while(Q--) {\n    string T;\n    cin >> T;\n    auto range = sa.lower_upper_bound(T);\n\
    \    cout << (range.first != range.second) << endl;\n  }\n}\n"
  dependsOn:
  - template/template.cpp
  - string/suffix-array.cpp
  isVerificationFile: true
  path: test/verify/aoj-alds-1-14-d.test.cpp
  requiredBy: []
  timestamp: '2021-05-01 00:06:55+09:00'
  verificationStatus: TEST_ACCEPTED
  verifiedWith: []
documentation_of: test/verify/aoj-alds-1-14-d.test.cpp
layout: document
redirect_from:
- /verify/test/verify/aoj-alds-1-14-d.test.cpp
- /verify/test/verify/aoj-alds-1-14-d.test.cpp.html
title: test/verify/aoj-alds-1-14-d.test.cpp
---
