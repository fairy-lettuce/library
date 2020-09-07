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


# :heavy_check_mark: test/verify/yukicoder-703.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yukicoder-703.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-26 01:18:25+09:00


* see: <a href="https://yukicoder.me/problems/no/703">https://yukicoder.me/problems/no/703</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/dp/monotone-minima.cpp.html">Monotone-Minima <small>(dp/monotone-minima.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/dp/online-offline-dp.cpp.html">Online-Offline-DP(オンライン・オフライン変換) <small>(dp/online-offline-dp.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://yukicoder.me/problems/no/703"

#include "../../template/template.cpp"

#include "../../dp/monotone-minima.cpp"
#include "../../dp/online-offline-dp.cpp"

int main() {
  int n;
  cin >> n;
  vector< int > a(n), x(n), y(n);
  for(int i = 0; i < n; i++) cin >> a[i];
  for(int i = 0; i < n; i++) cin >> x[i];
  for(int i = 0; i < n; i++) cin >> y[i];
  function< int64_t(int, int) > dist = [&](int i, int j) {
    assert(0 <= i && i < j && j <= n);
    int s = abs(a[j - 1] - x[i]);
    int t = abs(y[i]);
    return 1LL * s * s + 1LL * t * t;
  };
  cout << online_offline_dp(n, dist).back() << endl;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yukicoder-703.test.cpp"
#define PROBLEM "https://yukicoder.me/problems/no/703"

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
#line 4 "test/verify/yukicoder-703.test.cpp"

#line 1 "dp/monotone-minima.cpp"
/**
 * @brief Monotone-Minima
 * @docs docs/monotone-minima.md
 */
template< typename T, typename Compare = less< T > >
vector< pair< int, T > > monotone_minima(int H, int W, const function< T(int, int) > &f, const Compare &comp = Compare()) {
  vector< pair< int, T > > dp(H);
  function< void(int, int, int, int) > dfs = [&](int top, int bottom, int left, int right) {
    if(top > bottom) return;
    int line = (top + bottom) / 2;
    T ma;
    int mi = -1;
    for(int i = left; i <= right; i++) {
      T cst = f(line, i);
      if(mi == -1 || comp(cst, ma)) {
        ma = cst;
        mi = i;
      }
    }
    dp[line] = make_pair(mi, ma);
    dfs(top, line - 1, left, mi);
    dfs(line + 1, bottom, mi, right);
  };
  dfs(0, H - 1, 0, W - 1);
  return dp;
}
#line 1 "dp/online-offline-dp.cpp"
/**
 * @brief  Online-Offline-DP(オンライン・オフライン変換)
 * @docs docs/online-offline-dp.md
 */
template< typename T, typename Compare = less< T > >
vector< T > online_offline_dp(int W, const function< T(int, int) > &f, const Compare &comp = Compare()) {
  vector< T > dp(W + 1);
  vector< int > isset(W + 1);
  int y_base = -1, x_base = -1;
  function< T(int, int) > get_cost = [&](int y, int x) { // return dp[0, x+x_base)+f[x+x_base, y+y_base)
    return dp[x + x_base] + f(x + x_base, y + y_base);
  };
  function< void(int, int, int) > induce = [&](int l, int m, int r) { // dp[l, m) -> dp[m, r)
    x_base = l, y_base = m;
    auto ret = monotone_minima(r - m, m - l, get_cost, comp);
    for(int i = 0; i < ret.size(); i++) {
      if(!isset[m + i] || comp(ret[i].second, dp[m + i])) {
        isset[m + i] = true;
        dp[m + i] = ret[i].second;
      }
    }
  };
  function< void(int, int) > dfs = [&](int l, int r) {
    if(l + 1 == r) {
      x_base = l, y_base = l;
      T cst = l ? get_cost(0, -1) : 0;
      if(!isset[l] || comp(cst, dp[l])) {
        isset[l] = true;
        dp[l] = cst;
      }
    } else {
      int mid = (l + r) / 2;
      dfs(l, mid);
      induce(l, mid, r);
      dfs(mid, r);
    }
  };
  dfs(0, W + 1);
  return dp;
};
#line 7 "test/verify/yukicoder-703.test.cpp"

int main() {
  int n;
  cin >> n;
  vector< int > a(n), x(n), y(n);
  for(int i = 0; i < n; i++) cin >> a[i];
  for(int i = 0; i < n; i++) cin >> x[i];
  for(int i = 0; i < n; i++) cin >> y[i];
  function< int64_t(int, int) > dist = [&](int i, int j) {
    assert(0 <= i && i < j && j <= n);
    int s = abs(a[j - 1] - x[i]);
    int t = abs(y[i]);
    return 1LL * s * s + 1LL * t * t;
  };
  cout << online_offline_dp(n, dist).back() << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

