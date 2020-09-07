---
layout: default
---

<!-- mathjax config similar to math.stackexchange -->
<script type="text/javascript" async
  src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: { equationNumbers: { autoNumber: "AMS" }},
    tex2jax: {
      inlineMath: [ ['$','$'] ],
      processEscapes: true
    },
    "HTML-CSS": { matchFontHeight: false },
    displayAlign: "left",
    displayIndent: "2em"
  });
</script>

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/jquery-balloon-js@1.1.2/jquery.balloon.min.js" integrity="sha256-ZEYs9VrgAeNuPvs15E39OsyOJaIkXEEt10fzxJ20+2I=" crossorigin="anonymous"></script>
<script type="text/javascript" src="../../../assets/js/copy-button.js"></script>
<link rel="stylesheet" href="../../../assets/css/copy-button.css" />


# :heavy_check_mark: test/verify/yosupo-staticrmq-2.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-staticrmq-2.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-02-20 22:23:04+09:00


* see: <a href="https://judge.yosupo.jp/problem/staticrmq">https://judge.yosupo.jp/problem/staticrmq</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/structure/others/disjoint-sparse-table.cpp.html">Disjoint-Sparse-Table <small>(structure/others/disjoint-sparse-table.cpp)</small></a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/staticrmq"

#include "../../template/template.cpp"

#include "../../structure/others/disjoint-sparse-table.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< int > A(N);
  cin >> A;
  auto f = [](int a, int b) { return min(a, b); };
  DisjointSparseTable< int > st(A, f);
  while(Q--) {
    int l, r;
    cin >> l >> r;
    cout << st.query(l, r) << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-staticrmq-2.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/staticrmq"

#line 1 "template/template.cpp"
#include<bits/stdc++.h>

using namespace std;

using int64 = long long;
const int mod = 1e9 + 7;

const int64 infll = (1LL << 62) - 1;
const int inf = (1 << 30) - 1;

struct IoSetup {
  IoSetup() {
    cin.tie(nullptr);
    ios::sync_with_stdio(false);
    cout << fixed << setprecision(10);
    cerr << fixed << setprecision(10);
  }
} iosetup;


template< typename T1, typename T2 >
ostream &operator<<(ostream &os, const pair< T1, T2 >& p) {
  os << p.first << " " << p.second;
  return os;
}

template< typename T1, typename T2 >
istream &operator>>(istream &is, pair< T1, T2 > &p) {
  is >> p.first >> p.second;
  return is;
}

template< typename T >
ostream &operator<<(ostream &os, const vector< T > &v) {
  for(int i = 0; i < (int) v.size(); i++) {
    os << v[i] << (i + 1 != v.size() ? " " : "");
  }
  return os;
}

template< typename T >
istream &operator>>(istream &is, vector< T > &v) {
  for(T &in : v) is >> in;
  return is;
}

template< typename T1, typename T2 >
inline bool chmax(T1 &a, T2 b) { return a < b && (a = b, true); }

template< typename T1, typename T2 >
inline bool chmin(T1 &a, T2 b) { return a > b && (a = b, true); }

template< typename T = int64 >
vector< T > make_v(size_t a) {
  return vector< T >(a);
}

template< typename T, typename... Ts >
auto make_v(size_t a, Ts... ts) {
  return vector< decltype(make_v< T >(ts...)) >(a, make_v< T >(ts...));
}

template< typename T, typename V >
typename enable_if< is_class< T >::value == 0 >::type fill_v(T &t, const V &v) {
  t = v;
}

template< typename T, typename V >
typename enable_if< is_class< T >::value != 0 >::type fill_v(T &t, const V &v) {
  for(auto &e : t) fill_v(e, v);
}

template< typename F >
struct FixPoint : F {
  FixPoint(F &&f) : F(forward< F >(f)) {}
 
  template< typename... Args >
  decltype(auto) operator()(Args &&... args) const {
    return F::operator()(*this, forward< Args >(args)...);
  }
};
 
template< typename F >
inline decltype(auto) MFP(F &&f) {
  return FixPoint< F >{forward< F >(f)};
}
#line 4 "test/verify/yosupo-staticrmq-2.test.cpp"

#line 1 "structure/others/disjoint-sparse-table.cpp"
/**
 * @brief Disjoint-Sparse-Table
 * @docs docs/disjoint-sparse-table.md
 */
template< typename Semigroup >
struct DisjointSparseTable {
  using F = function< Semigroup(Semigroup, Semigroup) >;
  const F f;
  vector< vector< Semigroup > > st;
  vector< int > lookup;

  DisjointSparseTable(const vector< Semigroup > &v, const F &f) : f(f) {
    int b = 0;
    while((1 << b) <= v.size()) ++b;
    st.resize(b, vector< Semigroup >(v.size(), Semigroup()));
    for(int i = 0; i < v.size(); i++) st[0][i] = v[i];
    for(int i = 1; i < b; i++) {
      int shift = 1 << i;
      for(int j = 0; j < v.size(); j += shift << 1) {
        int t = min(j + shift, (int) v.size());
        st[i][t - 1] = v[t - 1];
        for(int k = t - 2; k >= j; k--) st[i][k] = f(v[k], st[i][k + 1]);
        if(v.size() <= t) break;
        st[i][t] = v[t];
        int r = min(t + shift, (int) v.size());
        for(int k = t + 1; k < r; k++) st[i][k] = f(st[i][k - 1], v[k]);
      }
    }
    lookup.resize(1 << b);
    for(int i = 2; i < lookup.size(); i++) {
      lookup[i] = lookup[i >> 1] + 1;
    }
  }

  Semigroup query(int l, int r) {
    if(l >= --r) return st[0][l];
    int p = lookup[l ^ r];
    return f(st[p][l], st[p][r]);
  }
};
#line 6 "test/verify/yosupo-staticrmq-2.test.cpp"

int main() {
  int N, Q;
  cin >> N >> Q;
  vector< int > A(N);
  cin >> A;
  auto f = [](int a, int b) { return min(a, b); };
  DisjointSparseTable< int > st(A, f);
  while(Q--) {
    int l, r;
    cin >> l >> r;
    cout << st.query(l, r) << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

