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


# :heavy_check_mark: test/verify/yukicoder-952.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yukicoder-952.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-08-20 03:24:24+09:00


* see: <a href="https://yukicoder.me/problems/no/952">https://yukicoder.me/problems/no/952</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/structure/convex-hull-trick/convex-hull-trick-add-monotone.cpp.html">Convex-Hull-Trick-Add-Monotone <small>(structure/convex-hull-trick/convex-hull-trick-add-monotone.cpp)</small></a>
* :heavy_check_mark: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://yukicoder.me/problems/no/952"

#include "../../template/template.cpp"

#include "../../structure/convex-hull-trick/convex-hull-trick-add-monotone.cpp"

int main() {
  int N;
  cin >> N;
  vector< int > A(N);
  cin >> A;
  vector< int64 > S(N + 2);
  for(int i = 0; i < N; i++) {
    S[i + 1] = S[i] + A[i];
  }

  auto dp = make_v< int64 >(N + 2, N + 1);
  auto dp2 = make_v< int64 >(N + 2, N + 1);
  fill_v(dp, infll);
  fill_v(dp2, infll);
  dp[0][0] = 0;

  vector< ConvexHullTrickAddMonotone< int64, true > > chts(2 * N + 10);
  const int Shift = N + 5;

  for(int i = 0; i <= N + 1; i++) {
    if(i <= N) {
      for(int j = 0; j <= N; j++) {
        int Q = j - i + Shift;
        if(!chts[Q].empty()) chmin(dp2[i + 1][j], S[i] * S[i] + chts[Q].query_monotone_dec(-2 * S[i]));
      }
    }
    for(int j = 0; j <= N; j++) {
      if(i) dp[i][j] = min(dp[i - 1][j], dp2[i][j]);
      if(dp[i][j] != infll) chts[j - i + Shift].add(S[i], dp[i][j] + S[i] * S[i]);
    }
  }

  for(int i = 1; i <= N; i++) {
    cout << dp[N + 1][i] << endl;
  }
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yukicoder-952.test.cpp"
#define PROBLEM "https://yukicoder.me/problems/no/952"

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
#line 4 "test/verify/yukicoder-952.test.cpp"

#line 1 "structure/convex-hull-trick/convex-hull-trick-add-monotone.cpp"
/**
 * @brief Convex-Hull-Trick-Add-Monotone
 * @docs docs/convex-hull-trick-add-monotone.md
*/
template< typename T, bool isMin >
struct ConvexHullTrickAddMonotone {
#define F first
#define S second
  using P = pair< T, T >;
  deque< P > H;

  ConvexHullTrickAddMonotone() = default;

  bool empty() const { return H.empty(); }

  void clear() { H.clear(); }

  inline int sgn(T x) { return x == 0 ? 0 : (x < 0 ? -1 : 1); }

  using D = long double;

  inline bool check(const P &a, const P &b, const P &c) {
    if(b.S == a.S || c.S == b.S)
      return sgn(b.F - a.F) * sgn(c.S - b.S) >= sgn(c.F - b.F) * sgn(b.S - a.S);

    //return (b.F-a.F)*(c.S-b.S) >= (b.S-a.S)*(c.F-b.F);
    return
        D(b.F - a.F) * sgn(c.S - b.S) / D(abs(b.S - a.S)) >=
        D(c.F - b.F) * sgn(b.S - a.S) / D(abs(c.S - b.S));
  }

  void add(T a, T b) {
    if(!isMin) a *= -1, b *= -1;
    P line(a, b);
    if(empty()) {
      H.emplace_front(line);
      return;
    }
    if(H.front().F <= a) {
      if(H.front().F == a) {
        if(H.front().S <= b) return;
        H.pop_front();
      }
      while(H.size() >= 2 && check(line, H.front(), H[1])) H.pop_front();
      H.emplace_front(line);
    } else {
      assert(a <= H.back().F);
      if(H.back().F == a) {
        if(H.back().S <= b) return;
        H.pop_back();
      }
      while(H.size() >= 2 && check(H[H.size() - 2], H.back(), line)) H.pop_back();
      H.emplace_back(line);
    }
  }

  inline T get_y(const P &a, const T &x) {
    return a.F * x + a.S;
  }

  T query(T x) {
    assert(!empty());
    int l = -1, r = H.size() - 1;
    while(l + 1 < r) {
      int m = (l + r) >> 1;
      if(get_y(H[m], x) >= get_y(H[m + 1], x)) l = m;
      else r = m;
    }
    if(isMin) return get_y(H[r], x);
    return -get_y(H[r], x);
  }

  T query_monotone_inc(T x) {
    assert(!empty());
    while(H.size() >= 2 && get_y(H.front(), x) >= get_y(H[1], x)) H.pop_front();
    if(isMin) return get_y(H.front(), x);
    return -get_y(H.front(), x);
  }

  T query_monotone_dec(T x) {
    assert(!empty());
    while(H.size() >= 2 && get_y(H.back(), x) >= get_y(H[H.size() - 2], x)) H.pop_back();
    if(isMin) return get_y(H.back(), x);
    return -get_y(H.back(), x);
  }

#undef F
#undef S
};
#line 6 "test/verify/yukicoder-952.test.cpp"

int main() {
  int N;
  cin >> N;
  vector< int > A(N);
  cin >> A;
  vector< int64 > S(N + 2);
  for(int i = 0; i < N; i++) {
    S[i + 1] = S[i] + A[i];
  }

  auto dp = make_v< int64 >(N + 2, N + 1);
  auto dp2 = make_v< int64 >(N + 2, N + 1);
  fill_v(dp, infll);
  fill_v(dp2, infll);
  dp[0][0] = 0;

  vector< ConvexHullTrickAddMonotone< int64, true > > chts(2 * N + 10);
  const int Shift = N + 5;

  for(int i = 0; i <= N + 1; i++) {
    if(i <= N) {
      for(int j = 0; j <= N; j++) {
        int Q = j - i + Shift;
        if(!chts[Q].empty()) chmin(dp2[i + 1][j], S[i] * S[i] + chts[Q].query_monotone_dec(-2 * S[i]));
      }
    }
    for(int j = 0; j <= N; j++) {
      if(i) dp[i][j] = min(dp[i - 1][j], dp2[i][j]);
      if(dp[i][j] != infll) chts[j - i + Shift].add(S[i], dp[i][j] + S[i] * S[i]);
    }
  }

  for(int i = 1; i <= N; i++) {
    cout << dp[N + 1][i] << endl;
  }
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

