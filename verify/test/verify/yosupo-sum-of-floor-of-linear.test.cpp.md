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


# :heavy_check_mark: test/verify/yosupo-sum-of-floor-of-linear.test.cpp

<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-sum-of-floor-of-linear.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-03 17:43:59+09:00


* see: <a href="https://judge.yosupo.jp/problem/sum_of_floor_of_linear">https://judge.yosupo.jp/problem/sum_of_floor_of_linear</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/math/number-theory/sum-of-floor-of-linear.cpp.html">Sum-Of-Floor-Of-Linear(一次関数の床関数の和)</a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/sum_of_floor_of_linear"

#include "../../template/template.cpp"

#include "../../math/number-theory/sum-of-floor-of-linear.cpp"

int main() {
  int T;
  cin >> T;
  while(T--) {
    int64 N, M, A, B;
    cin >> N >> M >> A >> B;
    cout << sum_of_floor_of_linear(N, M, A, B) << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-sum-of-floor-of-linear.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/sum_of_floor_of_linear"

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
#line 4 "test/verify/yosupo-sum-of-floor-of-linear.test.cpp"

#line 1 "test/verify/../../math/number-theory/sum-of-floor-of-linear.cpp"
/**
 * @title Sum-Of-Floor-Of-Linear(一次関数の床関数の和)
 * @brief $\sum_{i=0}^{n-1} floor(\frac {a \times i + b} m)$
 */
template< typename T >
T sum_of_floor_of_linear(const T &n, const T &m, T a, T b) {
  T ret = 0;
  if(a >= m) ret += (n - 1) * n * (a / m) / 2, a %= m;
  if(b >= m) ret += n * (b / m), b %= m;
  T y = (a * n + b) / m;
  if(y == 0) return ret;
  T x = y * m - b;
  ret += (n - (x + a - 1) / a) * y;
  ret += sum_of_floor_of_linear(y, a, m, (a - x % a) % a);
  return ret;
}
#line 6 "test/verify/yosupo-sum-of-floor-of-linear.test.cpp"

int main() {
  int T;
  cin >> T;
  while(T--) {
    int64 N, M, A, B;
    cin >> N >> M >> A >> B;
    cout << sum_of_floor_of_linear(N, M, A, B) << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

