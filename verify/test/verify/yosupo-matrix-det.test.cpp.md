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


# :heavy_check_mark: test/verify/yosupo-matrix-det.test.cpp

<a href="../../../index.html">Back to top page</a>

* <a href="{{ site.github.repository_url }}/blob/master/test/verify/yosupo-matrix-det.test.cpp">View this file on GitHub</a>
    - Last commit date: 2019-12-12 22:16:00+09:00


* see: <a href="https://judge.yosupo.jp/problem/matrix_det">https://judge.yosupo.jp/problem/matrix_det</a>


## Depends on

* :warning: <a href="../../../library/math/combinatorics/mod-int.cpp.html">math/combinatorics/mod-int.cpp</a>
* :heavy_check_mark: <a href="../../../library/math/matrix/matrix.cpp.html">math/matrix/matrix.cpp</a>
* :warning: <a href="../../../library/template/template.cpp.html">template/template.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
#define PROBLEM "https://judge.yosupo.jp/problem/matrix_det"

#include "../../template/template.cpp"

#include "../../math/combinatorics/mod-int.cpp"

#include "../../math/matrix/matrix.cpp"

const int MOD = 998244353;
using mint = ModInt< MOD >;

int main() {
  int N;
  cin >> N;
  Matrix< mint > mat(N);
  for(int i = 0; i < N; i++) cin >> mat[i];
  cout << mat.determinant() << endl;
}

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "test/verify/yosupo-matrix-det.test.cpp"
#define PROBLEM "https://judge.yosupo.jp/problem/matrix_det"

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
#line 4 "test/verify/yosupo-matrix-det.test.cpp"

#line 1 "test/verify/../../math/combinatorics/mod-int.cpp"
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
#line 6 "test/verify/yosupo-matrix-det.test.cpp"

#line 1 "test/verify/../../math/matrix/matrix.cpp"
template< class T >
struct Matrix {
  vector< vector< T > > A;

  Matrix() {}

  Matrix(size_t n, size_t m) : A(n, vector< T >(m, 0)) {}

  Matrix(size_t n) : A(n, vector< T >(n, 0)) {};

  size_t height() const {
    return (A.size());
  }

  size_t width() const {
    return (A[0].size());
  }

  inline const vector< T > &operator[](int k) const {
    return (A.at(k));
  }

  inline vector< T > &operator[](int k) {
    return (A.at(k));
  }

  static Matrix I(size_t n) {
    Matrix mat(n);
    for(int i = 0; i < n; i++) mat[i][i] = 1;
    return (mat);
  }

  Matrix &operator+=(const Matrix &B) {
    size_t n = height(), m = width();
    assert(n == B.height() && m == B.width());
    for(int i = 0; i < n; i++)
      for(int j = 0; j < m; j++)
        (*this)[i][j] += B[i][j];
    return (*this);
  }

  Matrix &operator-=(const Matrix &B) {
    size_t n = height(), m = width();
    assert(n == B.height() && m == B.width());
    for(int i = 0; i < n; i++)
      for(int j = 0; j < m; j++)
        (*this)[i][j] -= B[i][j];
    return (*this);
  }

  Matrix &operator*=(const Matrix &B) {
    size_t n = height(), m = B.width(), p = width();
    assert(p == B.height());
    vector< vector< T > > C(n, vector< T >(m, 0));
    for(int i = 0; i < n; i++)
      for(int j = 0; j < m; j++)
        for(int k = 0; k < p; k++)
          C[i][j] = (C[i][j] + (*this)[i][k] * B[k][j]);
    A.swap(C);
    return (*this);
  }

  Matrix &operator^=(long long k) {
    Matrix B = Matrix::I(height());
    while(k > 0) {
      if(k & 1) B *= *this;
      *this *= *this;
      k >>= 1LL;
    }
    A.swap(B.A);
    return (*this);
  }

  Matrix operator+(const Matrix &B) const {
    return (Matrix(*this) += B);
  }

  Matrix operator-(const Matrix &B) const {
    return (Matrix(*this) -= B);
  }

  Matrix operator*(const Matrix &B) const {
    return (Matrix(*this) *= B);
  }

  Matrix operator^(const long long k) const {
    return (Matrix(*this) ^= k);
  }

  friend ostream &operator<<(ostream &os, Matrix &p) {
    size_t n = p.height(), m = p.width();
    for(int i = 0; i < n; i++) {
      os << "[";
      for(int j = 0; j < m; j++) {
        os << p[i][j] << (j + 1 == m ? "]\n" : ",");
      }
    }
    return (os);
  }


  T determinant() {
    Matrix B(*this);
    assert(width() == height());
    T ret = 1;
    for(int i = 0; i < width(); i++) {
      int idx = -1;
      for(int j = i; j < width(); j++) {
        if(B[j][i] != 0) idx = j;
      }
      if(idx == -1) return (0);
      if(i != idx) {
        ret *= -1;
        swap(B[i], B[idx]);
      }
      ret *= B[i][i];
      T vv = B[i][i];
      for(int j = 0; j < width(); j++) {
        B[i][j] /= vv;
      }
      for(int j = i + 1; j < width(); j++) {
        T a = B[j][i];
        for(int k = 0; k < width(); k++) {
          B[j][k] -= B[i][k] * a;
        }
      }
    }
    return (ret);
  }
};
#line 8 "test/verify/yosupo-matrix-det.test.cpp"

const int MOD = 998244353;
using mint = ModInt< MOD >;

int main() {
  int N;
  cin >> N;
  Matrix< mint > mat(N);
  for(int i = 0; i < N; i++) cin >> mat[i];
  cout << mat.determinant() << endl;
}

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

