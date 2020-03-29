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


# :heavy_check_mark: test/verify/yosupo-find-linear-recurrence.test.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#5a4423c79a88aeb6104a40a645f9430c">test/verify</a>
* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-find-linear-recurrence.test.cpp">View this file on GitHub</a>
    - Last commit date: 2020-03-03 17:43:59+09:00


* see: <a href="https://judge.yosupo.jp/problem/find_linear_recurrence">https://judge.yosupo.jp/problem/find_linear_recurrence</a>


## Depends on

* :heavy_check_mark: <a href="../../../library/math/combinatorics/mod-int.cpp.html">math/combinatorics/mod-int.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/fps/berlekamp-massey.cpp.html">math/fps/berlekamp-massey.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/fps/formal-power-series.cpp.html">math/fps/formal-power-series.cpp</a>
* :question: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/find_linear_recurrence"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-int.cpp"

#include "../../math/fps/formal-power-series.cpp"

#include "../../math/fps/berlekamp-massey.cpp"

const int MOD = 998244353;
using mint = ModInt< MOD >;

int main() {
  int N;
  cin >> N;
  FormalPowerSeries< mint > A(N);
  cin >> A;
  auto C = berlekamp_massey(A);
  const int d = (int) C.size() - 1;
  cout << d << endl;
  for(int j = 1; j <= d; j++) cout << C[d - j] << " ";
  cout << endl;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-find-linear-recurrence.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/find_linear_recurrence"

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
#line 4 "test/verify/yosupo-find-linear-recurrence.test.cpp"

#line 1 "math/combinatorics/mod-int.cpp"
template< int mod >
struct ModInt {
  int x;

  ModInt() : x(0) {}

  ModInt(int64_t y) : x(y >= 0 ? y % mod : (mod - (-y) % mod) % mod) {}

  ModInt &operator+=(const ModInt &p) {
    if((x += p.x) >= mod) x -= mod;
    return *this;
  }

  ModInt &operator-=(const ModInt &p) {
    if((x += mod - p.x) >= mod) x -= mod;
    return *this;
  }

  ModInt &operator*=(const ModInt &p) {
    x = (int) (1LL * x * p.x % mod);
    return *this;
  }

  ModInt &operator/=(const ModInt &p) {
    *this *= p.inverse();
    return *this;
  }

  ModInt operator-() const { return ModInt(-x); }

  ModInt operator+(const ModInt &p) const { return ModInt(*this) += p; }

  ModInt operator-(const ModInt &p) const { return ModInt(*this) -= p; }

  ModInt operator*(const ModInt &p) const { return ModInt(*this) *= p; }

  ModInt operator/(const ModInt &p) const { return ModInt(*this) /= p; }

  bool operator==(const ModInt &p) const { return x == p.x; }

  bool operator!=(const ModInt &p) const { return x != p.x; }

  ModInt inverse() const {
    int a = x, b = mod, u = 1, v = 0, t;
    while(b > 0) {
      t = a / b;
      swap(a -= t * b, b);
      swap(u -= t * v, v);
    }
    return ModInt(u);
  }

  ModInt pow(int64_t n) const {
    ModInt ret(1), mul(x);
    while(n > 0) {
      if(n & 1) ret *= mul;
      mul *= mul;
      n >>= 1;
    }
    return ret;
  }

  friend ostream &operator<<(ostream &os, const ModInt &p) {
    return os << p.x;
  }

  friend istream &operator>>(istream &is, ModInt &a) {
    int64_t t;
    is >> t;
    a = ModInt< mod >(t);
    return (is);
  }

  static int get_mod() { return mod; }
};

using modint = ModInt< mod >;
#line 6 "test/verify/yosupo-find-linear-recurrence.test.cpp"

#line 1 "math/fps/formal-power-series.cpp"
template< typename T >
struct FormalPowerSeries : vector< T > {
  using vector< T >::vector;
  using P = FormalPowerSeries;

  using MULT = function< P(P, P) >;
  using FFT = function< void(P &) >;
  using SQRT = function< T(T) >;

  static MULT &get_mult() {
    static MULT mult = nullptr;
    return mult;
  }

  static void set_mult(MULT f) {
    get_mult() = f;
  }

  static FFT &get_fft() {
    static FFT fft = nullptr;
    return fft;
  }

  static FFT &get_ifft() {
    static FFT ifft = nullptr;
    return ifft;
  }

  static void set_fft(FFT f, FFT g) {
    get_fft() = f;
    get_ifft() = g;
  }

  static SQRT &get_sqrt() {
    static SQRT sqr = nullptr;
    return sqr;
  }

  static void set_sqrt(SQRT sqr) {
    get_sqrt() = sqr;
  }

  void shrink() {
    while(this->size() && this->back() == T(0)) this->pop_back();
  }

  P operator+(const P &r) const { return P(*this) += r; }

  P operator+(const T &v) const { return P(*this) += v; }

  P operator-(const P &r) const { return P(*this) -= r; }

  P operator-(const T &v) const { return P(*this) -= v; }

  P operator*(const P &r) const { return P(*this) *= r; }

  P operator*(const T &v) const { return P(*this) *= v; }

  P operator/(const P &r) const { return P(*this) /= r; }

  P operator%(const P &r) const { return P(*this) %= r; }

  P &operator+=(const P &r) {
    if(r.size() > this->size()) this->resize(r.size());
    for(int i = 0; i < r.size(); i++) (*this)[i] += r[i];
    return *this;
  }

  P &operator+=(const T &r) {
    if(this->empty()) this->resize(1);
    (*this)[0] += r;
    return *this;
  }

  P &operator-=(const P &r) {
    if(r.size() > this->size()) this->resize(r.size());
    for(int i = 0; i < r.size(); i++) (*this)[i] -= r[i];
    shrink();
    return *this;
  }

  P &operator-=(const T &r) {
    if(this->empty()) this->resize(1);
    (*this)[0] -= r;
    shrink();
    return *this;
  }

  P &operator*=(const T &v) {
    const int n = (int) this->size();
    for(int k = 0; k < n; k++) (*this)[k] *= v;
    return *this;
  }

  P &operator*=(const P &r) {
    if(this->empty() || r.empty()) {
      this->clear();
      return *this;
    }
    assert(get_mult() != nullptr);
    return *this = get_mult()(*this, r);
  }

  P &operator%=(const P &r) { return *this -= *this / r * r; }

  P operator-() const {
    P ret(this->size());
    for(int i = 0; i < this->size(); i++) ret[i] = -(*this)[i];
    return ret;
  }

  P &operator/=(const P &r) {
    if(this->size() < r.size()) {
      this->clear();
      return *this;
    }
    int n = this->size() - r.size() + 1;
    return *this = (rev().pre(n) * r.rev().inv(n)).pre(n).rev(n);
  }

  P dot(P r) const {
    P ret(min(this->size(), r.size()));
    for(int i = 0; i < ret.size(); i++) ret[i] = (*this)[i] * r[i];
    return ret;
  }

  P pre(int sz) const { return P(begin(*this), begin(*this) + min((int) this->size(), sz)); }

  P operator>>(int sz) const {
    if(this->size() <= sz) return {};
    P ret(*this);
    ret.erase(ret.begin(), ret.begin() + sz);
    return ret;
  }

  P operator<<(int sz) const {
    P ret(*this);
    ret.insert(ret.begin(), sz, T(0));
    return ret;
  }

  P rev(int deg = -1) const {
    P ret(*this);
    if(deg != -1) ret.resize(deg, T(0));
    reverse(begin(ret), end(ret));
    return ret;
  }

  P diff() const {
    const int n = (int) this->size();
    P ret(max(0, n - 1));
    for(int i = 1; i < n; i++) ret[i - 1] = (*this)[i] * T(i);
    return ret;
  }

  P integral() const {
    const int n = (int) this->size();
    P ret(n + 1);
    ret[0] = T(0);
    for(int i = 0; i < n; i++) ret[i + 1] = (*this)[i] / T(i + 1);
    return ret;
  }

  // F(0) must not be 0
  P inv(int deg = -1) const {
    assert(((*this)[0]) != T(0));
    const int n = (int) this->size();
    if(deg == -1) deg = n;
    if(get_fft() != nullptr) {
      P ret(*this);
      ret.resize(deg, T(0));
      return ret.inv_fast();
    }
    P ret({T(1) / (*this)[0]});
    for(int i = 1; i < deg; i <<= 1) {
      ret = (ret + ret - ret * ret * pre(i << 1)).pre(i << 1);
    }
    return ret.pre(deg);
  }

  // F(0) must be 1
  P log(int deg = -1) const {
    assert((*this)[0] == 1);
    const int n = (int) this->size();
    if(deg == -1) deg = n;
    return (this->diff() * this->inv(deg)).pre(deg - 1).integral();
  }

  P sqrt(int deg = -1) const {
    const int n = (int) this->size();
    if(deg == -1) deg = n;
    if((*this)[0] == T(0)) {
      for(int i = 1; i < n; i++) {
        if((*this)[i] != T(0)) {
          if(i & 1) return {};
          if(deg - i / 2 <= 0) break;
          auto ret = (*this >> i).sqrt(deg - i / 2);
          if(ret.empty()) return {};
          ret = ret << (i / 2);
          if(ret.size() < deg) ret.resize(deg, T(0));
          return ret;
        }
      }
      return P(deg, 0);
    }

    P ret;
    if(get_sqrt() == nullptr) {
      assert((*this)[0] == T(1));
      ret = {T(1)};
    } else {
      auto sqr = get_sqrt()((*this)[0]);
      if(sqr * sqr != (*this)[0]) return {};
      ret = {T(sqr)};
    }

    T inv2 = T(1) / T(2);
    for(int i = 1; i < deg; i <<= 1) {
      ret = (ret + pre(i << 1) * ret.inv(i << 1)) * inv2;
    }
    return ret.pre(deg);
  }

  // F(0) must be 0
  P exp(int deg = -1) const {
    assert((*this)[0] == T(0));
    const int n = (int) this->size();
    if(deg == -1) deg = n;
    if(get_fft() != nullptr) {
      P ret(*this);
      ret.resize(deg, T(0));
      return ret.exp_rec();
    }
    P ret({T(1)});
    for(int i = 1; i < deg; i <<= 1) {
      ret = (ret * (pre(i << 1) + T(1) - ret.log(i << 1))).pre(i << 1);
    }
    return ret.pre(deg);
  }


  P online_convolution_exp(const P &conv_coeff) const {
    const int n = (int) conv_coeff.size();
    assert((n & (n - 1)) == 0);
    vector< P > conv_ntt_coeff;
    auto& fft = get_fft();
    auto& ifft = get_ifft();
    for(int i = n; i >= 1; i >>= 1) {
      P g(conv_coeff.pre(i));
      fft(g);
      conv_ntt_coeff.emplace_back(g);
    }
    P conv_arg(n), conv_ret(n);
    auto rec = [&](auto rec, int l, int r, int d) -> void {
      if(r - l <= 16) {
        for(int i = l; i < r; i++) {
          T sum = 0;
          for(int j = l; j < i; j++) sum += conv_arg[j] * conv_coeff[i - j];
          conv_ret[i] += sum;
          conv_arg[i] = i == 0 ? T(1) : conv_ret[i] / i;
        }
      } else {
        int m = (l + r) / 2;
        rec(rec, l, m, d + 1);
        P pre(r - l);
        for(int i = 0; i < m - l; i++) pre[i] = conv_arg[l + i];
        fft(pre);
        for(int i = 0; i < r - l; i++) pre[i] *= conv_ntt_coeff[d][i];
        ifft(pre);
        for(int i = 0; i < r - m; i++) conv_ret[m + i] += pre[m + i - l];
        rec(rec, m, r, d + 1);
      }
    };
    rec(rec, 0, n, 0);
    return conv_arg;
  }

  P exp_rec() const {
    assert((*this)[0] == T(0));
    const int n = (int) this->size();
    int m = 1;
    while(m < n) m *= 2;
    P conv_coeff(m);
    for(int i = 1; i < n; i++) conv_coeff[i] = (*this)[i] * i;
    return online_convolution_exp(conv_coeff).pre(n);
  }


  P inv_fast() const {
    assert(((*this)[0]) != T(0));

    const int n = (int) this->size();
    P res{T(1) / (*this)[0]};

    for(int d = 1; d < n; d <<= 1) {
      P f(2 * d), g(2 * d);
      for(int j = 0; j < min(n, 2 * d); j++) f[j] = (*this)[j];
      for(int j = 0; j < d; j++) g[j] = res[j];
      get_fft()(f);
      get_fft()(g);
      for(int j = 0; j < 2 * d; j++) f[j] *= g[j];
      get_ifft()(f);
      for(int j = 0; j < d; j++) {
        f[j] = 0;
        f[j + d] = -f[j + d];
      }
      get_fft()(f);
      for(int j = 0; j < 2 * d; j++) f[j] *= g[j];
      get_ifft()(f);
      for(int j = 0; j < d; j++) f[j] = res[j];
      res = f;
    }
    return res.pre(n);
  }

  P pow(int64_t k, int deg = -1) const {
    const int n = (int) this->size();
    if(deg == -1) deg = n;
    for(int i = 0; i < n; i++) {
      if((*this)[i] != T(0)) {
        T rev = T(1) / (*this)[i];
        P ret = (((*this * rev) >> i).log() * k).exp() * ((*this)[i].pow(k));
        if(i * k > deg) return P(deg, T(0));
        ret = (ret << (i * k)).pre(deg);
        if(ret.size() < deg) ret.resize(deg, T(0));
        return ret;
      }
    }
    return *this;
  }

  T eval(T x) const {
    T r = 0, w = 1;
    for(auto &v : *this) {
      r += w * v;
      w *= x;
    }
    return r;
  }

  P pow_mod(int64_t n, P mod) const {
    P modinv = mod.rev().inv();
    auto get_div = [&](P base) {
      if(base.size() < mod.size()) {
        base.clear();
        return base;
      }
      int n = base.size() - mod.size() + 1;
      return (base.rev().pre(n) * modinv.pre(n)).pre(n).rev(n);
    };
    P x(*this), ret{1};
    while(n > 0) {
      if(n & 1) {
        ret *= x;
        ret -= get_div(ret) * mod;
      }
      x *= x;
      x -= get_div(x) * mod;
      n >>= 1;
    }
    return ret;
  }
};
#line 8 "test/verify/yosupo-find-linear-recurrence.test.cpp"

#line 1 "math/fps/berlekamp-massey.cpp"
template< class T >
FormalPowerSeries< T > berlekamp_massey(const FormalPowerSeries< T > &s) {
  const int N = (int) s.size();
  FormalPowerSeries< T > b = {T(-1)}, c = {T(-1)};
  T y = T(1);
  for(int ed = 1; ed <= N; ed++) {
    int l = int(c.size()), m = int(b.size());
    T x = 0;
    for(int i = 0; i < l; i++) x += c[i] * s[ed - l + i];
    b.emplace_back(0);
    m++;
    if(x == T(0)) continue;
    T freq = x / y;
    if(l < m) {
      auto tmp = c;
      c.insert(begin(c), m - l, T(0));
      for(int i = 0; i < m; i++) c[m - 1 - i] -= freq * b[m - 1 - i];
      b = tmp;
      y = x;
    } else {
      for(int i = 0; i < m; i++) c[l - 1 - i] -= freq * b[m - 1 - i];
    }
  }
  return c;
}
#line 10 "test/verify/yosupo-find-linear-recurrence.test.cpp"

const int MOD = 998244353;
using mint = ModInt< MOD >;

int main() {
  int N;
  cin >> N;
  FormalPowerSeries< mint > A(N);
  cin >> A;
  auto C = berlekamp_massey(A);
  const int d = (int) C.size() - 1;
  cout << d << endl;
  for(int j = 1; j <= d; j++) cout << C[d - j] << " ";
  cout << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

