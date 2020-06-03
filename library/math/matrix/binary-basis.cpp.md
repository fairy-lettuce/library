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


# :warning: math/matrix/binary-basis.cpp

<a href="../../../index.html">Back to top page</a>

* category: <a href="../../../index.html#a9839e7477a4d9c748aee996b52a14d5">math/matrix</a>
* <a href="{{ site.github.repository_url }}/blob/master/math/matrix/binary-basis.cpp">View this file on GitHub</a>
    - Last commit date: 2020-06-03 21:22:34+09:00




## Code

<a id="unbundled"></a>
{% raw %}
```cpp
template< typename T >
struct BinaryBasis {
  vector< T > basis;
  bool update;

  BinaryBasis() : update(false) {}

  bool add(T bit) {
    for(auto &p : basis) {
      bit = min(bit, bit ^ p);
    }
    if(bit) {
      basis.emplace_back(bit);
      return update = true;
    } else {
      return false;
    }
  }

  bool check(T bit) const {
    for(auto &p : basis) {
      bit = min(bit, bit ^ p);
    }
    return bit == 0;
  }

  void normalize() {
    sweep();
    for(int i = (int) basis.size() - 1; i >= 0; i--) {
      for(int j = i - 1; j >= 0; j--) chmin(basis[i], basis[i] ^ basis[j]);
    }
  }

  void sweep() {
    if(exchange(update, false)) {
      sort(begin(basis), end(basis));
    }
  }

  bool operator==(BinaryBasis< T > &a) {
    normalize(), a.normalize();
    return basis == a.basis;
  }

  T get_kth(int64_t k) { /* 0-indexed */
    if((1LL << basis.size()) <= k) {
      return -1;
    }
    T ret = T();
    sweep();
    for(int i = (int) basis.size() - 1; i >= 0; i--) {
      if(k < (1LL << i)) {
        ret = min(ret, ret ^ basis[i]);
      } else {
        k -= 1LL << i;
        ret = max(ret, ret ^ basis[i]);
      }
    }
    return ret;
  }
};

```
{% endraw %}

<a id="bundled"></a>
{% raw %}
```cpp
#line 1 "math/matrix/binary-basis.cpp"
template< typename T >
struct BinaryBasis {
  vector< T > basis;
  bool update;

  BinaryBasis() : update(false) {}

  bool add(T bit) {
    for(auto &p : basis) {
      bit = min(bit, bit ^ p);
    }
    if(bit) {
      basis.emplace_back(bit);
      return update = true;
    } else {
      return false;
    }
  }

  bool check(T bit) const {
    for(auto &p : basis) {
      bit = min(bit, bit ^ p);
    }
    return bit == 0;
  }

  void normalize() {
    sweep();
    for(int i = (int) basis.size() - 1; i >= 0; i--) {
      for(int j = i - 1; j >= 0; j--) chmin(basis[i], basis[i] ^ basis[j]);
    }
  }

  void sweep() {
    if(exchange(update, false)) {
      sort(begin(basis), end(basis));
    }
  }

  bool operator==(BinaryBasis< T > &a) {
    normalize(), a.normalize();
    return basis == a.basis;
  }

  T get_kth(int64_t k) { /* 0-indexed */
    if((1LL << basis.size()) <= k) {
      return -1;
    }
    T ret = T();
    sweep();
    for(int i = (int) basis.size() - 1; i >= 0; i--) {
      if(k < (1LL << i)) {
        ret = min(ret, ret ^ basis[i]);
      } else {
        k -= 1LL << i;
        ret = max(ret, ret ^ basis[i]);
      }
    }
    return ret;
  }
};

```
{% endraw %}

<a href="../../../index.html">Back to top page</a>

