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


# :heavy_check_mark: test/verify/yosupo-maximum-independent-set.test.cpp

<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-maximum-independent-set.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-12 22:16:00+09:00


* see: <a href="https://judge.yosupo.jp/problem/maximum_independent_set">https://judge.yosupo.jp/problem/maximum_independent_set</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/graph/others/maximum-independent-set.cpp.html">graph/others/maximum-independent-set.cpp</a>
* :heavy_check_mark: <a href="../../../library/graph/template.cpp.html">graph/template.cpp</a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/maximum_independent_set"

#include "../../template/template.cpp"
#include "../../graph/template.cpp"

#include "../../graph/others/maximum-independent-set.cpp"

int main() {
  int N, M;
  cin >> N >> M;
  Matrix < int > mat(N, vector< int >(N));
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    mat[a][b] = true;
    mat[b][a] = true;
  }
  auto ret = maximum_independent_set(mat);
  cout << ret.size() << endl;
  cout << ret << endl;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-maximum-independent-set.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/maximum_independent_set"

#line 1 "test/verify/../../template/template.cpp"
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
#line 1 "test/verify/../../graph/template.cpp"
template< typename T >
struct edge {
  int src, to;
  T cost;

  edge(int to, T cost) : src(-1), to(to), cost(cost) {}

  edge(int src, int to, T cost) : src(src), to(to), cost(cost) {}

  edge &operator=(const int &x) {
    to = x;
    return *this;
  }

  operator int() const { return to; }
};

template< typename T >
using Edges = vector< edge< T > >;
template< typename T >
using WeightedGraph = vector< Edges< T > >;
using UnWeightedGraph = vector< vector< int > >;
template< typename T >
using Matrix = vector< vector< T > >;
#line 5 "test/verify/yosupo-maximum-independent-set.test.cpp"

#line 1 "test/verify/../../graph/others/maximum-independent-set.cpp"
template< typename T >
vector< int > maximum_independent_set(const Matrix< T > &g, int trial = 1000000) {

  int N = (int) g.size();
  vector< uint64_t > bit(N);

  assert(N <= 64);
  for(int i = 0; i < N; i++) {
    for(int j = 0; j < N; j++) {
      if(i != j) {
        assert(g[i][j] == g[j][i]);
        if(g[i][j]) bit[i] |= uint64_t(1) << j;
      }
    }
  }

  vector< int > ord(N);
  iota(begin(ord), end(ord), 0);
  mt19937 mt(chrono::steady_clock::now().time_since_epoch().count());
  int ret = 0;
  uint64_t ver;
  for(int i = 0; i < trial; i++) {
    shuffle(begin(ord), end(ord), mt);
    uint64_t used = 0;
    int add = 0;
    for(int j : ord) {
      if(used & bit[j]) continue;
      used |= uint64_t(1) << j;
      ++add;
    }
    if(ret < add) {
      ret = add;
      ver = used;
    }
  }
  vector< int > ans;
  for(int i = 0; i < N; i++) {
    if((ver >> i) & 1) ans.emplace_back(i);
  }
  return ans;
}
#line 7 "test/verify/yosupo-maximum-independent-set.test.cpp"

int main() {
  int N, M;
  cin >> N >> M;
  Matrix < int > mat(N, vector< int >(N));
  for(int i = 0; i < M; i++) {
    int a, b;
    cin >> a >> b;
    mat[a][b] = true;
    mat[b][a] = true;
  }
  auto ret = maximum_independent_set(mat);
  cout << ret.size() << endl;
  cout << ret << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

