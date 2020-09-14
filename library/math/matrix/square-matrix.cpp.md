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


# :question: Square-Matrix(正方行列) <small>(math/matrix/square-matrix.cpp)</small>

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#a9839e7477a4d9c748aee996b52a14d5">math/matrix</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/matrix/square-matrix.cpp">View this file on GitHub</a>
    - Last commit date: 2020-06-11 22:00:32+09:00




## Verified with

* :heavy_check_mark: <a href="../../../verify/test/verify/aoj-1254.test.cpp.html">test/verify/aoj-1254.test.cpp</a>
* :x: <a href="../../../verify/test/verify/yukicoder-650.test.cpp.html">test/verify/yukicoder-650.test.cpp</a>


## Code

<a id="unbundled"></a>
{% raw %}
```cpp
/**
 * @brief Square-Matrix(正方行列)
 */
template< class T, size_t N >
struct SquareMatrix {
  array< array< T, N >, N > A;

  SquareMatrix() = default;

  size_t size() { return N; }

  inline const array< T, N > &operator[](int k) const {
    return (A.at(k));
  }

  inline array< T, N > &operator[](int k) {
    return (A.at(k));
  }

  static SquareMatrix add_identity() {
    return SquareMatrix();
  }

  static SquareMatrix mul_identity() {
    SquareMatrix mat;
    for(size_t i = 0; i < N; i++) mat[i][i] = 1;
    return mat;
  }

  SquareMatrix &operator+=(const SquareMatrix &B) {
    for(size_t i = 0; i < N; i++) {
      for(size_t j = 0; j < N; j++) {
        (*this)[i][j] += B[i][j];
      }
    }
    return *this;
  }

  SquareMatrix &operator-=(const SquareMatrix &B) {
    for(size_t i = 0; i < N; i++) {
      for(size_t j = 0; j < N; j++) {
        (*this)[i][j] -= B[i][j];
      }
    }
    return *this;
  }

  SquareMatrix &operator*=(const SquareMatrix &B) {
    array< array< T, N >, N > C;
    for(size_t i = 0; i < N; i++) {
      for(size_t j = 0; j < N; j++) {
        for(size_t k = 0; k < N; k++) {
          C[i][j] = (C[i][j] + (*this)[i][k] * B[k][j]);
        }
      }
    }
    A.swap(C);
    return (*this);
  }

  SquareMatrix &operator^=(uint64_t k) {
    SquareMatrix B = SquareMatrix::mul_identity();
    while(k > 0) {
      if(k & 1) B *= *this;
      *this *= *this;
      k >>= 1LL;
    }
    A.swap(B.A);
    return *this;
  }

  SquareMatrix operator+(const SquareMatrix &B) const {
    return SquareMatrix(*this) += B;
  }

  SquareMatrix operator-(const SquareMatrix &B) const {
    return SquareMatrix(*this) -= B;
  }

  SquareMatrix operator*(const SquareMatrix &B) const {
    return SquareMatrix(*this) *= B;
  }

  SquareMatrix operator^(uint64_t k) const {
    return SquareMatrix(*this) ^= k;
  }

  friend ostream &operator<<(ostream &os, SquareMatrix &p) {
    for(int i = 0; i < N; i++) {
      os << "[";
      for(int j = 0; j < N; j++) {
        os << p[i][j] << (j + 1 == N ? "]\n" : ",");
      }
    }
    return os;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/matrix/square-matrix.cpp"
/**
 * @brief Square-Matrix(正方行列)
 */
template< class T, size_t N >
struct SquareMatrix {
  array< array< T, N >, N > A;

  SquareMatrix() = default;

  size_t size() { return N; }

  inline const array< T, N > &operator[](int k) const {
    return (A.at(k));
  }

  inline array< T, N > &operator[](int k) {
    return (A.at(k));
  }

  static SquareMatrix add_identity() {
    return SquareMatrix();
  }

  static SquareMatrix mul_identity() {
    SquareMatrix mat;
    for(size_t i = 0; i < N; i++) mat[i][i] = 1;
    return mat;
  }

  SquareMatrix &operator+=(const SquareMatrix &B) {
    for(size_t i = 0; i < N; i++) {
      for(size_t j = 0; j < N; j++) {
        (*this)[i][j] += B[i][j];
      }
    }
    return *this;
  }

  SquareMatrix &operator-=(const SquareMatrix &B) {
    for(size_t i = 0; i < N; i++) {
      for(size_t j = 0; j < N; j++) {
        (*this)[i][j] -= B[i][j];
      }
    }
    return *this;
  }

  SquareMatrix &operator*=(const SquareMatrix &B) {
    array< array< T, N >, N > C;
    for(size_t i = 0; i < N; i++) {
      for(size_t j = 0; j < N; j++) {
        for(size_t k = 0; k < N; k++) {
          C[i][j] = (C[i][j] + (*this)[i][k] * B[k][j]);
        }
      }
    }
    A.swap(C);
    return (*this);
  }

  SquareMatrix &operator^=(uint64_t k) {
    SquareMatrix B = SquareMatrix::mul_identity();
    while(k > 0) {
      if(k & 1) B *= *this;
      *this *= *this;
      k >>= 1LL;
    }
    A.swap(B.A);
    return *this;
  }

  SquareMatrix operator+(const SquareMatrix &B) const {
    return SquareMatrix(*this) += B;
  }

  SquareMatrix operator-(const SquareMatrix &B) const {
    return SquareMatrix(*this) -= B;
  }

  SquareMatrix operator*(const SquareMatrix &B) const {
    return SquareMatrix(*this) *= B;
  }

  SquareMatrix operator^(uint64_t k) const {
    return SquareMatrix(*this) ^= k;
  }

  friend ostream &operator<<(ostream &os, SquareMatrix &p) {
    for(int i = 0; i < N; i++) {
      os << "[";
      for(int j = 0; j < N; j++) {
        os << p[i][j] << (j + 1 == N ? "]\n" : ",");
      }
    }
    return os;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

