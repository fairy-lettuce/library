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


# :heavy_check_mark: test/verify/yosupo-tetration-mod.test.cpp

<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-tetration-mod.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-03 18:28:13+09:00


* see: <a href="https://judge.yosupo.jp/problem/tetration_mod">https://judge.yosupo.jp/problem/tetration_mod</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/math/combinatorics/mod-pow.cpp.html">math/combinatorics/mod-pow.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/combinatorics/mod-tetration.cpp.html">Mod-Tetration <small>(math/combinatorics/mod-tetration.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/math/number-theory/euler-phi.cpp.html">Euler's-Phi-Function(オイラーのφ関数) <small>(math/number-theory/euler-phi.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/tetration_mod"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-pow.cpp"
#include "../../math/number-theory/euler-phi.cpp"

#include "../../math/combinatorics/mod-tetration.cpp"

int main() {
  int T;
  cin >> T;
  while(T--) {
    int a, b, m;
    cin >> a >> b >> m;
    cout << mod_tetration< int64_t >(a, b, m) % m << "\n";
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-tetration-mod.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/tetration_mod"

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
#line 4 "test/verify/yosupo-tetration-mod.test.cpp"

#line 1 "test/verify/../../math/combinatorics/mod-pow.cpp"
template< typename T >
T mod_pow(T x, T n, const T &p) {
  T ret = 1;
  while(n > 0) {
    if(n & 1) (ret *= x) %= p;
    (x *= x) %= p;
    n >>= 1;
  }
  return ret;
}

#line 1 "test/verify/../../math/number-theory/euler-phi.cpp"
/**
 * @brief Euler's-Phi-Function(オイラーのφ関数)
 * @docs docs/euler-phi.md
 */
template< typename T >
T euler_phi(T n) {
  T ret = n;
  for(T i = 2; i * i <= n; i++) {
    if(n % i == 0) {
      ret -= ret / i;
      while(n % i == 0) n /= i;
    }
  }
  if(n > 1) ret -= ret / n;
  return ret;
}
#line 7 "test/verify/yosupo-tetration-mod.test.cpp"

#line 1 "test/verify/../../math/combinatorics/mod-tetration.cpp"
/**
 * @brief Mod-Tetration
 */
template< typename T >
T mod_tetration(const T &a, const T &b, const T &m) {
  if(m == 1) return 0;
  if(a == 0) return !(b & 1);
  if(b == 0) return 1;
  if(b == 1) return a % m;
  if(b == 2) return mod_pow(a % m, a, m);
  auto phi = euler_phi(m);
  return mod_pow(a % m, mod_tetration(a, b - 1, phi) + phi, m);
}
#line 9 "test/verify/yosupo-tetration-mod.test.cpp"

int main() {
  int T;
  cin >> T;
  while(T--) {
    int a, b, m;
    cin >> a >> b >> m;
    cout << mod_tetration< int64_t >(a, b, m) % m << "\n";
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

